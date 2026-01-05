---
title: "ComfyUI Tools Workflow"
date: 2026-01-03
draft: false
toc: false
images:
tags:
  - Generative AI
  - ComfyUI
  - Tools
---

## Download Workflow

[ComfyUI Tools Json](/attachments/comfyui-tools.json)

---

## What tools does it contain

1. LoRA Tag Extractor
    - Input: checkpoint + LoRA
    - Output: extracted tags

2. Image to control map (for ControlNets)
    - Input: an image
    - Output: one or more control maps (edge, depth, pose)

---

## How to use (quick)

1. Copy the JSON from the block above.
2. In ComfyUI, Load → Paste (or import the workflow JSON file, depending on your setup).
3. Confirm the required custom nodes are installed.
4. Select inputs and run each tool node group (some nodes may be bypassed, enable as desired).
