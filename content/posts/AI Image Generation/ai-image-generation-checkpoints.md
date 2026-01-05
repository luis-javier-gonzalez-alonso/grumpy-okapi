---
title: "Checkpoints 101: Base models, fine-tunes, and merges (what to use, when)"
date: 2026-01-05
draft: false
toc: false
images:
tags:
  - Generative AI
  - Models
  - Checkpoints
---

A **checkpoint** is the “main brain” file that generates the image. Everything else (LoRA, ControlNet, etc.) sits on top of a checkpoint.

This guide focuses only on checkpoints:
- **Base models** (the foundations)
- **Trained models (fine-tunes)** vs **merge models**
- The **most commonly used base families** + their typical use-cases
- Practical pros/cons + notable restrictions/flaws

---

## 1) Base checkpoint vs fine-tuned checkpoint

### Base checkpoint
A general-purpose foundation released by a lab/vendor (or a large community release).
Examples: **SD 1.5**, **SDXL 1.0**, **Stable Diffusion 3.5**, **FLUX.1 [dev]**.

**Why you care:** the base decides *capabilities* and *ecosystem support* (tools, LoRAs, ControlNets, workflows).

### Fine-tuned checkpoint (trained model)
A base checkpoint that has been **further trained** on a dataset to specialize style/content (e.g., “anime portraits”, “product renders”, “cinematic realism”).
Example: **Pony Diffusion v6 XL** is an SDXL finetune.

**Why you care:** you get “the look” faster, often with shorter prompts.

---

## 2) Trained models vs merge models

### Trained model (fine-tune)
**How it’s made:** additional training updates the weights using examples (gradient descent).
**Typical result:** more coherent “personality” and consistent behavior.

**Pros**
- More reliable style/subject bias
- Often better consistency across prompts
- Usually easier prompting (less wrestling)

**Cons**
- Can overfit (repeating faces/compositions)
- Strong biases (e.g., “everything becomes glossy portraits”)
- Quality depends heavily on dataset curation

### Merge model
**How it’s made:** combines two+ checkpoints (weight blending) without extra training.
**Typical result:** a “cocktail” of traits (e.g., realism from one + lighting from another).

**Pros**
- Fast to create, lots of experimentation
- Can mix complementary strengths

**Cons**
- Can be less stable (odd artifacts, inconsistent prompt response)
- “Best of both” is not guaranteed; sometimes you get “worst of both”
- Lineage/licensing can get messy if merged components have restrictions

---

## 3) The most used base families (and what they’re good at)

Below are **widely used** foundations or foundation-like families you’ll see constantly across tools and community checkpoints.

### A) Stable Diffusion 1.5 (SD 1.5)
**Best for:** lightweight local generation, huge ecosystem, tons of fine-tunes/LoRAs.
**Pros**
- Runs on modest GPUs
- Massive community library (styles, characters, niches)
**Cons / common flaws**
- Weaker at text-in-image and complex compositions than newer bases
- Anatomy/hands often need extra help (inpainting, ADetailer-like workflows)
**License note:** released under **CreativeML Open RAIL-M**.

---

### B) Stable Diffusion 2.1 (SD 2.1)
**Best for:** “cleaner” general image generation compared to 1.5, some workflows prefer it.
**Pros**
- Solid general base; can feel less “muddy” than many old 1.5 blends
**Cons**
- Smaller community ecosystem than 1.5/SDXL
- Many users find it pickier with prompts than 1.5-style finetunes
**License note:** commonly distributed under **CreativeML Open RAIL++-M**.

---

### C) Stable Diffusion XL 1.0 (SDXL)
**Best for:** higher resolution, better prompt understanding, better typography than SD1.5 in many cases.
**Pros**
- Strong general-purpose base with modern “look”
- Great for: portraits, environments, design-ish images, better composition
**Cons**
- Heavier GPU/VRAM demands than SD1.5
- Many SDXL finetunes expect SDXL-specific workflows (refiners, SDXL VAEs, etc.)
**License note:** **CreativeML Open RAIL++-M** (official release).

---

### D) SDXL Turbo / SD-Turbo (distilled “fast” variants)
**Best for:** speed, quick ideation, real-time-ish exploration.
**Pros**
- Very fast generation (great for sketching ideas)
**Cons**
- Often lower fidelity than full SDXL at the same resolution
- Less “room” to refine details; can look a bit “compressed”
**License note:** SD-Turbo points to Stability’s licensing terms; commercial terms depend on the license path.

---

### E) Stable Diffusion 3.5 (SD 3.5 suite)
**Best for:** modern prompt-following and high quality on consumer hardware (where supported).
**Pros**
- Designed as a newer generation; positioned as customizable and consumer-hardware friendly
**Cons**
- Tooling/workflow compatibility can be more variable than SDXL/1.5 depending on your stack
**License note:** Stability states SD 3.5 models are free for commercial + non-commercial use under the **Stability AI Community License**.

---

### F) Stable Cascade
**Best for:** experimentation with the Würstchen-style pipeline; some people like its aesthetic/efficiency traits.
**Pros**
- Different architecture approach; interesting training/fine-tuning characteristics
**Cons / restrictions**
- Released under a **non-commercial** license (research preview) per Stability’s announcement.
- Smaller ecosystem vs SDXL/1.5 (fewer community assets/workflows)

---

### G) FLUX.1 [dev] (Black Forest Labs)
**Best for:** high-quality generations and strong modern results (where supported).
**Pros**
- Strong general image quality and “modern” rendering (popular momentum in 2024–2025+)
**Cons / restrictions**
- The **model** is under a “Non-Commercial License” for the weights, but the license explicitly states users can use **outputs** broadly (with caveats) and forbids using outputs to train/fine-tune a competing model.
- Heavier compute requirements than SD1.5; best experience depends on your tooling

---

### H) “Pony” (as a foundation-like community base: Pony Diffusion XL)
**Best for:** anime/cartoon/anthro ecosystems, Danbooru-tag-style prompting culture, huge LoRA scene around it.
**Pros**
- Very strong community “content + LoRA” ecosystem in its niche
- Often excellent for stylized characters and illustration workflows
**Cons / quirks**
- Prompting style can differ from “plain SDXL”: many users lean into tag-like prompting
- Can bias outputs toward the dataset’s dominant styles
**Evidence note:** Pony Diffusion v6 XL is explicitly an SDXL finetune in its model card.

---

### I) “Anything” (SD1.5 anime finetune family, e.g., Anything V5)
**Best for:** classic SD1.5 anime look, fast stylized portraits/characters.
**Pros**
- Easy to get anime-style results with short prompts
- Lightweight (SD1.5 base)
**Cons**
- Less flexible outside its core aesthetic vs newer SDXL-based anime finetunes
**Evidence note:** Anything V5 is described as an anime-focused fine-tuned SD checkpoint.

---

### J) “Illustrious XL” (SDXL illustration-focused checkpoint family, OnomaAIResearch)
**Best for:** high-resolution illustration/anime-style images (notably **native 1536×1536**) with a mix of **natural-language + Danbooru/tag** prompting.
**Pros**
- **Native 1536px** support (and wide resolution range without extra hi-res tricks)
- Works well with **plain English prompts, tags, or both** (hybrid prompting)
- Strong as a **foundation** for training/using add-ons (the model card highlights compatibility with common extensions like LoRA/ControlNet)
**Cons**
- **Version behavior can vary**; the authors publish a **v2.0 “STABLE”** checkpoint specifically for more stable generation behavior
- **Knowledge cutoff** noted on v1.0 (trained July 2024; knowledge up to June 2024)
- **Licensing differs by release**: v1.0 is marked **sdxl-license**, while v2.0 is marked **creativeml-openrail-m**—so always check the exact version you download before commercial use/distribution
**Evidence note:** On Hugging Face, Illustrious XL v1.0 is described as an SDXL-based model with **native 1536×1536** plus **NLP + tag-based prompting**, and v2.0 is presented as a **more stabilized** checkpoint.

---

## 4) Practical selection guide (fast)

- **I want maximum compatibility + huge community assets:** SD 1.5 or SDXL.
- **I want a modern all-rounder at higher quality:** SDXL 1.0 (and then pick a finetune like a realism/art variant).
- **I want speed for brainstorming:** SDXL Turbo / SD-Turbo.
- **I want strong modern results and my tooling supports it:** FLUX.1 [dev] (but check license constraints for your use case).
- **I want anime/stylized character pipelines:** Pony (SDXL finetune) or Anything-style (SD1.5 finetune).
- **I need explicitly non-commercial research experimentation:** Stable Cascade fits that framing (license-limited).

---

## 5) A quick warning about “restrictions” (two layers)

1) **Base model license** (from Stability/BFL/etc.) – governs the weights and sometimes distribution/usage thresholds.
2) **Creator-added terms** (some community checkpoints add extra conditions, especially around redistribution/merging). These are common in the wild, so always read the model page terms before using it commercially or redistributing.
