---
title: "Notes on Generative AI 1"
date: 2025-07-20T19:52:31+01:00
draft: true
toc: false
images:
tags: 
  - Generative AI
  - Stable Diffusion
---

This post will be a collection of links and information to begin on this world and understand how it works.

One of the first clarifications I want to make here, about the components you will find while using Stable Diffusion to generate content.
- Checkpoint
- LoRA
- Embedding
- VAE
- ...

## Composition tips and tricks

From [this](https://civitai.com/articles/16602/simple-composition-tricks-to-instantly-improve-ai-images-with-prompts) article.

- rule of thirds composition
- leading lines
- symmetrical composition
- negative space
- foreground, middle ground, background
- dutch angle
- frame within a frame / framed by
- shallow depth of field / blurred background / bokeh background / f/1.4 / background out of focus / ...
- golden ratio composition / fibonacci spiral composition
- high-angle / bird’s eye view / low-angle / worm’s eye view

## LoRAs Usage

### SD 1.5

#### Details slider
https://civitaiarchive.com/models/153562?modelVersionId=171989&is_nsfw=true
weight: -5.0 to 5.0
positive: more detail
negative: less detail
#### Hair length slider
https://civitaiarchive.com/models/114215?modelVersionId=123434&is_nsfw=true
weight: -8.0 to 8.0 (or more)
positive: longer hair
negative: shorter hair
#### Weight slider
https://civitaiarchive.com/models/112552?modelVersionId=126824&is_nsfw=true
weight: -3.0 to 3.0
positive: more weight
negative: less weight
#### Skin tone slider
https://civitaiarchive.com/models/112594?modelVersionId=121575&is_nsfw=true
weight: -5.0 to 5.0
positive: darker
negative: lighter

### Resources:
- https://civitai.com/
- https://huggingface.co/

### Advanced resources (this articles describe the innards of Stable Diffusion):
- https://theaisummer.com/diffusion-models/
- https://huggingface.co/blog/annotated-diffusion
