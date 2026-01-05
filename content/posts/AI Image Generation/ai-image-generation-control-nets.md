---
title: "ControlNet 101 (with ComfyUI): types, use-cases, and practical node setups"
date: 2026-01-07
draft: false
toc: false
images:
tags:
  - Generative AI
  - ControlNet
  - Composition
  - ComfyUI
---

ControlNet is a way to **constrain** image generation using an extra “control signal” (a *hint image* like edges, pose skeleton, depth map, etc.) so your output follows a **pose / composition / structure** more reliably than prompt-only generation.

A useful mental model:
- **Preprocessor** converts your reference image → a **control image** (edges/pose/depth/etc.).
- **ControlNet model** reads that control image during sampling and nudges the generation to match it.

---

## 1) ControlNet types (what they control + when to use)

Below are the most common “control types” you’ll see. Most exist as **ControlNet v1.1 models** for SD1.5, and many have SDXL variants too—**you must match ControlNet to your base model family** (SD1.5 ControlNet with SD1.5 checkpoint, SDXL ControlNet with SDXL checkpoint, etc.).

### A) Edge / outline controls
Use these to “lock” composition while letting the model invent texture/style.

- **Canny (hard edges)**
  Best for: keeping silhouettes, object boundaries, scene layout.
  Great for: re-styling photos, keeping architecture outlines.

- **SoftEdge / HED (softer edges)**
  Best for: more natural guidance than canny (less “rigid”).

- **Lineart / Anime lineart**
  Best for: turning sketches / line drawings into finished art, comic/anime workflows.

- **MLSD (straight lines)**
  Best for: buildings/interiors with strong geometry (walls, perspective grids).

### B) Pose controls
- **OpenPose / DWpose**
  Best for: character pose replication (body + optional hands/face depending on preprocessor).

### C) 3D structure controls
- **Depth (MiDaS / Zoe / LeReS, etc.)**
  Best for: preserving scene depth and large forms without hard outlines.

- **Normal maps**
  Best for: guiding surface orientation/shape (useful for object renders).

### D) “Sketchy / semantic” controls
- **Scribble**
  Best for: rough doodles → coherent scenes; quick concept blocking.

- **Segmentation**
  Best for: “this region is sky / hair / skin / clothing” style control (semantic layout).

### E) Specialized controls (common in model packs)
- **Tile**
  Best for: adding detail while preserving the original image structure (popular in upscale/detail workflows).

- **Inpaint ControlNet**
  Best for: masked edits with better consistency; v1.1 includes an inpaint model.

---

## 2) Key concepts that matter in practice

### Control strength
In ComfyUI’s Apply ControlNet node, **strength ~0.5–1.5** is commonly recommended; too high can create strange results.

### Start / end percent (when ControlNet applies)
ControlNet doesn’t need to be active for the whole denoise process. You can:
- Apply strongly early to set structure, then fade out to let details resolve naturally.
ComfyUI’s Apply ControlNet includes `start_percent` and `end_percent` for this.

### Multiple ControlNets
You can stack multiple controls (e.g., Pose + Depth) by **chaining Apply ControlNet nodes** (layered).

### Preprocessor ↔ model pairing
Many ControlNets expect a specific kind of control image:
- OpenPose ControlNet needs OpenPose preprocessor output; Canny ControlNet needs Canny output, etc.

---

## 3) ComfyUI setup (models + preprocessors)

### A) Put ControlNet models where ComfyUI can load them
- ComfyUI detects ControlNet models in: `ComfyUI/models/controlnet`
- The ControlNet Loader node will also read extra paths configured in `extra_model_paths.yaml`.

If you need SD1.5 ControlNet v1.1 safetensors: there’s a common FP16 safetensors repo used by ComfyUI users.

### B) Install preprocessors (recommended)
Base ComfyUI doesn’t ship all preprocessors; the common extension is:
- **Fannovel16 / comfyui_controlnet_aux**

It provides many preprocessors and an **AIO Aux Preprocessor** node for quick setup (but if you want threshold controls, use the specific preprocessor node).

---

## 4) Minimal ComfyUI workflow (single ControlNet)

Here’s the standard node chain (SD1.5 or SDXL — just match models):

1) **Load Image** (your reference)
2) **Preprocessor** (e.g., Canny / OpenPose / Depth) → produces control image
3) **ControlNet Loader** (loads the ControlNet model)
4) **CLIP Text Encode (Positive)** + **CLIP Text Encode (Negative)**
5) **Apply ControlNet** (feeds control into positive+negative conditioning)
6) **KSampler** (uses the modified conditioning to generate a latent)
7) **VAE Decode** → **Save Image**

### “Apply ControlNet” settings to start with
From ComfyUI Wiki:
- `strength`: start around **0.8–1.0** (typical useful range 0.5–1.5)
- `start_percent`: **0.0**
- `end_percent`: **0.8–1.0** (try ending early if it’s too rigid)

---

## 5) Practical recipes (ComfyUI node + config examples)

### Recipe 1 — Keep composition (photo → stylized) with Canny
**Use-case:** “Same layout, new style”
- Preprocessor: **Canny Edge**
- ControlNet model: **canny**
- Apply ControlNet:
  - strength: 0.7–1.1
  - start: 0.0
  - end: 0.7–0.9 (lower end = more freedom for final details)
Evidence: Canny preprocessor + canny control model pairing is a core mapping in controlnet_aux docs.

### Recipe 2 — Lock a character pose (OpenPose)
**Use-case:** “Same pose, different character/outfit”
- Preprocessor: **OpenPose** or **DWpose**
- ControlNet model: **openpose**
- Apply ControlNet:
  - strength: 0.8–1.2
  - start: 0.0
  - end: 0.6–0.85 (ending earlier can reduce “stiff” anatomy)
OpenPose estimator options are listed in the aux preprocessor docs.

### Recipe 3 — Preserve 3D structure without harsh outlines (Depth)
**Use-case:** “Keep scene depth / camera structure”
- Preprocessor: **Depth** (MiDaS / Zoe / LeReS)
- ControlNet model: **depth**
- Apply ControlNet:
  - strength: 0.6–1.0
  - start: 0.0
  - end: 0.8–1.0
Depth estimators and typical pairing are documented in the aux list.

### Recipe 4 — Sketch → finished art (Lineart / Scribble)
**Use-case:** “I drew it, render it”
- Preprocessor: **Lineart** (or **Scribble** if very rough)
- ControlNet model: lineart / scribble
- Apply ControlNet:
  - strength: 0.9–1.4 (sketch workflows often need stronger adherence)
  - start: 0.0
  - end: 0.9–1.0
Lineart/anime lineart and scribble preprocessors are listed in the aux docs.

---

## 6) Mixing multiple ControlNets (ComfyUI “stacking”)

**Why:** One control is rarely enough for complex scenes (e.g., pose + environment layout).
ComfyUI supports mixing by **chaining Apply ControlNet nodes** (layered).

Example: **Pose + Depth**
- Apply ControlNet #1: OpenPose (strength ~1.0, end ~0.8)
- Apply ControlNet #2: Depth (strength ~0.7, end ~1.0)
Then feed the final conditioning to KSampler.

---

## 7) Advanced options (optional, power-user)

### Scheduling + masks (Advanced ControlNet)
If you want ControlNet strength to vary across timesteps or apply only to regions via masks, there’s a popular extension:
- **Kosinkadink / ComfyUI-Advanced-ControlNet**, with nodes like **Apply Advanced ControlNet** and **Load Advanced ControlNet Model**, including `start_percent` / `stop_percent` and mask inputs.

---

## 8) Common pitfalls (fast troubleshooting)

- **Wrong model family:** SD1.5 ControlNet with SDXL checkpoint (or vice versa) → weak or broken control. (Match families.)
- **Wrong preprocessor:** feeding a raw image to a ControlNet that expects a specific control map → poor adherence.
- **Strength too high:** “weird / distorted / overconstrained” results. ComfyUI wiki explicitly warns too-high strength can look strange.
- **Too many stacked controls at high strength:** controls fight each other; lower strengths or shorten end_percent.

---

## 9) Quick reference: ComfyUI nodes you’ll actually search for

Core:
- **ControlNet Loader**
- **Apply ControlNet** (has strength + start_percent + end_percent)

Preprocessors (via comfyui_controlnet_aux):
- **AIO Aux Preprocessor** (fast, fewer knobs)
- Individual preprocessors: **canny / hed / lineart / openpose / depth** etc.
