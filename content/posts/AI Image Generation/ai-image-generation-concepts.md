---
title: "AI Image Generation: A Beginner’s Cheat Sheet (Stable Diffusion & friends)"
date: 2026-01-04
draft: false
toc: false
images:
tags:
  - Generative AI
  - Diffusion Model Fundamentals
  - Model Components
  - Workflow Basics
  - ComfyUI
---

This is a short “initiation” guide to the most common terms you’ll see when generating images with modern diffusion models (Stable Diffusion, SDXL, etc.). You don’t need to memorise everything—just learn what each piece *does* and when you’d use it.

---

## Mental model: what happens when you generate an image?

You give the system:
- **A text prompt** (what you want),
- Optional **extra guidance** (pose, composition, depth, reference image, etc.),
- And some **settings** (steps, sampler, CFG, size, seed).

The generator starts from noise and “denoises” it into an image. The terms below are the main *building blocks* that affect that process.

---

## Checkpoint (the “base model”)

**What it is:** The main trained model file.<br>
**What it controls:** Overall style capability, knowledge, anatomy quality, aesthetics, and what it “knows how to draw”.<br>
**When you change it:** When you want a different *foundation* (photoreal vs anime, SD1.5 vs SDXL, etc.).

**Rule of thumb:** Pick a checkpoint that already leans toward your target style. Everything else is a modifier.

---

## VAE (Variational Autoencoder)

**What it is:** The component that converts between the model’s internal “latent” space and actual pixels.<br>
**What it controls:** Color richness, contrast, fine detail feel, and sometimes weird artifacts (washed-out, gray, banding).<br>
**When you change it:** When images look “off” (muted colors, muddy contrast) or a checkpoint recommends a specific VAE.

**Rule of thumb:** If your images look flat or odd-colored, VAE mismatch is a common culprit.

---

## CLIP / Text Encoder

**What it is:** The “language understanding” part that turns your prompt into something the model can follow.<br>
**What it controls:** How well prompt words map to visual concepts, prompt sensitivity, and token weighting behavior.<br>
**When you change it:** Usually you don’t—except with certain pipelines/models (some have custom text encoders).

**Rule of thumb:** If the model “doesn’t get” your prompt, it’s often the checkpoint/text-encoder combo, not you.

---

## LoRA (Low-Rank Adaptation)

**What it is:** A small add-on that nudges the checkpoint toward a specific style, character, outfit, technique, or subject.<br>
**What it controls:** Targeted changes without replacing the whole checkpoint.<br>
**How it’s used:** Loaded with a **weight** (strength), e.g. 0.4–1.0 commonly (varies a lot).<br>
**When you use it:** When you want a specific style/character/detail reliably.

**Rule of thumb:** LoRAs are “specialised lenses.” Great for consistency; too strong can distort or overpower.

---

## Embedding / Textual Inversion

**What it is:** A learned “new word” (token) that represents a concept/style.<br>
**What it controls:** Injects a concept via the prompt with a token like `myStyleToken`.<br>
**When you use it:** For small style nudges, specific looks, or negative embeddings (e.g., to reduce bad anatomy).

**Rule of thumb:** Embeddings are prompt-based mini-skills; LoRAs are usually stronger and broader.

---

## ControlNet (structure control)

**What it is:** A guidance system that forces the generation to follow a structural input.<br>
**What it controls:** Pose, composition, edges, depth, lineart, segmentation, etc.<br>
**Typical inputs:** A reference image processed into:
- **OpenPose** (body pose),
- **Canny/edges** (composition outlines),
- **Depth** (3D-ish structure),
- **Lineart** (drawing guidance).

**Rule of thumb:** Use ControlNet when you want the *layout* to be predictable, not just the style.

---

## Img2Img (image-to-image)

**What it is:** You start from an existing image instead of pure noise.<br>
**What it controls:** Keeps some composition while transforming style/details.<br>
**Key setting:** **Denoise strength** (how much it changes).
- Low denoise → preserves original more
- High denoise → more freedom / more change

**Rule of thumb:** Img2img is the easiest way to “iterate” on an idea without losing it.

---

## Inpainting (edit part of an image)

**What it is:** Img2img but only in a masked area.<br>
**What it controls:** Fix hands/face, change outfits, replace background objects, etc.<br>
**When you use it:** When “almost perfect” images need targeted repair.

**Rule of thumb:** Generate broadly → then inpaint to polish.

---

## Sampler (how denoising steps are taken)

**What it is:** The algorithm guiding the denoise process across steps.<br>
**What it controls:** Sharpness vs smoothness, consistency, speed, “feel” of results.<br>
**When you change it:** When results are too noisy, too soft, or inconsistent.

**Rule of thumb:** Sampler choice matters, but less than checkpoint + prompt + guidance.

---

## Steps

**What it is:** How many denoising iterations you run.<br>
**What it controls:** Detail, coherence, and compute time.<br>

**Rule of thumb:** Too few → messy; too many → diminishing returns (and can overcook).

---

## CFG Scale (prompt strength)

**What it is:** How strongly the model is forced to follow the prompt.<br>
**What it controls:** Literalness vs naturalness.
- Low CFG → more artistic/loose
- High CFG → more literal, but can cause artifacts or “burnt” look

**Rule of thumb:** If images look harsh or unnatural, try lowering CFG.

---

## Seed (repeatability)

**What it is:** The random starting point for noise.<br>
**What it controls:** Reproducibility.
- Same seed + same settings → similar image
- Change seed → new variations

**Rule of thumb:** Save seeds when you like a composition—then iterate with small changes.

---

## Negative prompt (what to avoid)

**What it is:** A prompt for undesired traits.<br>
**What it controls:** Reduces common artifacts (bad hands, extra limbs, text, watermark, etc.).

**Rule of thumb:** Keep it practical; huge negative lists can sometimes fight your positives.

---

## How these pieces fit together (fast recipes)

### 1) “I just want good images”
- Choose a solid **checkpoint**
- Use reasonable **steps + CFG**
- Add a minimal **negative prompt**

### 2) “I want this exact style/character”
- Checkpoint + **LoRA** (tune weight)
- Optional **embedding** token
- Fix mistakes with **inpainting**

### 3) “I want this exact pose/composition”
- Add **ControlNet** (OpenPose/Depth/Canny)
- Or do **img2img** from a reference

### 4) “My colors look wrong / washed out”
- Check **VAE** (use recommended VAE for the checkpoint)

---

## Mini-glossary

- **Checkpoint:** the main brain.
- **LoRA:** a strong, targeted add-on.
- **Embedding:** a learned token/keyword.
- **ControlNet:** structure/pose/composition control.
- **VAE:** how latents become pixels (colors/contrast).
- **CLIP/Text encoder:** how the prompt becomes guidance.
- **Img2img:** transform an existing image.
- **Inpainting:** edit a masked region.
- **Sampler/Steps/CFG/Seed:** the “how” of generation.
