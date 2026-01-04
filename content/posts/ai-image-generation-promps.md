---
title: "AI Prompting 101: Natural Language vs Danbooru Tags (plus Negative Prompts)"
date: 2026-01-06
draft: false
toc: false
images:
tags:
  - Generative AI
  - Prompt Engineering
  - Prompt Design
---

Prompting is just *communicating intent* to the model. Different model families respond better to different “dialects”:
- **Natural language prompting** (plain English descriptions)
- **Danbooru-style prompting** (comma-separated tags, common in anime/illustration models)

This guide is short and practical. For the natural-language section, the core structure is based on [SergVidocq’s beginner guide](https://civitai.com/articles/16890/how-to-craft-perfect-prompts-for-image-generation-a-simple-guide-for-beginners). And if you want to see the kind of tagged images many anime models learn from, you can browse the Danbooru dataset [here](https://danbooru.donmai.us/).

---

## Part 1 — Natural language prompting (plain English)

### The basic prompt “recipe” (layered, not magical)
Build your prompt like a stack of clear layers (adapted from the referenced article):

1) **Main subject / scene**
   - “a young female wizard” (better than “girl”)

2) **Action + context** (what’s happening, where)
   - “sitting on a rock, reading an ancient spellbook in an abandoned castle”

3) **Descriptive adjectives** (shape, mood, quality, vibe)
   - “mysterious, detailed, cinematic”

4) **Appearance details** (clothes, pose, expression, unique traits)
   - “purple hooded cloak, leather outfit with ornaments, focused expression”

5) **Background / environment**
   - “floating magical particles, full moon behind ruined windows”

6) **Style / medium**
   - “digital illustration”, “photo”, “pencil sketch”, “oil painting”, “3D render”

7) **Lighting + color palette (optional but powerful)**
   - “dim moonlight, cool blue-purple tones”, “warm golden hour”

8) **Logic + clarity**
   - Avoid contradictions and ambiguity (“red cat and blue dog”, not “cat and dog, red and blue”)

> Tip from the referenced guide: English usually yields more predictable results, since a lot of training data and community prompting is English-first.

---

### “Good vs bad” examples (natural language)

**Too vague**
- `girl, castle`

**Clear and structured**
- `A young female wizard sitting on a rock, reading an ancient spellbook inside an abandoned castle. Purple hooded cloak, leather outfit with ornaments, calm focused expression. Floating magical particles, moonlight through broken windows. Digital illustration, high detail, cool blue-purple tones, soft rim lighting.`

---

### Small habits that improve results fast
- **Be specific about the subject** (age, role, species, object type)
- **Put the “story” in one sentence** (subject + action + place), then add details
- **Declare style explicitly** if you care about it
- **Use lighting words** when the mood matters (“candlelit”, “neon”, “overcast”, “studio lighting”)
- **Remove contradictions** before adding more tokens

---

## Part 2 — Danbooru-style prompting (tag prompts)

Danbooru-style prompts are typically:
- **comma-separated tags**
- often used by **anime/illustration checkpoints** trained on tag datasets
- very “keyword-y” rather than sentence-y

### What a tag prompt looks like
Example (anime-ish):
- `1girl, wizard, purple cloak, hood, spellbook, sitting, castle interior, moonlight, floating particles, detailed background, cinematic lighting, masterpiece`

### Common tag “categories”
You can think in buckets (you don’t need all of them):

- **Subject & count**: `1girl`, `1boy`, `2girls`, `solo`
- **Identity / archetype**: `wizard`, `knight`, `android`
- **Appearance**: `purple cloak`, `hood`, `long hair`, `gloves`
- **Pose / action**: `sitting`, `reading`, `looking at viewer`
- **Environment**: `castle interior`, `night`, `moon`
- **Lighting / mood**: `moonlight`, `rim light`, `dramatic lighting`
- **Composition / camera**: `close-up`, `full body`, `wide shot`, `from above`
- **Quality / style meta-tags** (model-dependent): `masterpiece`, `best quality`, `highly detailed`

### Tag prompting: practical rules
- **Use commas** to separate concepts.
- **Prefer known tags** (common words/tags the model likely learned).
- **Don’t overstuff**: 15–40 strong tags often beats 200 noisy tags.
- **Order is less critical than it used to be**, but you’ll still see people put “subject first, style/quality later.”

### Mixing styles: hybrid prompting
Many modern workflows do:
- a short **natural-language core** + a small set of **tags**
Example:
- `a wizard reading in an abandoned castle, moonlight,`
- `1girl, purple cloak, spellbook, castle interior, floating particles, cinematic lighting, detailed background`

This is especially useful if:
- you want the clarity of a sentence
- but your model responds well to tags

---

## Negative prompts (works for both styles)

A **negative prompt** says what you *don’t* want: artifacts, anatomy errors, unwanted styles, watermarks, etc.

### What negatives are best for
- Removing common junk: `watermark, text, logo`
- Avoiding anatomy issues: `extra fingers, extra limbs, bad hands`
- Preventing style drift: `blurry, lowres, jpeg artifacts`

### Two good negative strategies

**1) Minimal, focused negatives (recommended to start)**
- `low quality, blurry, watermark, text, extra fingers, bad hands`

Pros: less fighting with your positive prompt.

**2) Model-specific “negative packs”**
Some communities use longer lists tuned to a checkpoint/style.
Pros: can reduce common failure modes for that model.
Cons: can overconstrain or cause “samey” outputs.

### Negative prompt mistakes to avoid
- **Contradicting your positives**
  If you want “film grain” but negative includes “grain”, you’ll get weird results.
- **Trying to fix everything with negatives**
  If composition is wrong, use better positives, img2img, or ControlNet—negatives won’t invent structure.

---

## Quick choosing guide: which prompt style should you use?

- Use **natural language** when:
  - you’re on SDXL / photoreal / generalist checkpoints
  - you want clear scene descriptions

- Use **Danbooru tags** when:
  - you’re on anime/illustration checkpoints that “think in tags”
  - you want consistent character/illustration conventions

- Use **hybrid** when:
  - you want the best of both worlds and the model supports it

---

## Tiny templates you can copy

### Natural language template
`[Main subject], [action] in [setting]. [Appearance details]. [Background elements]. [Style/medium]. [Lighting]. [Color palette].`

### Danbooru template
`[count/subject], [identity], [appearance], [pose/action], [environment], [lighting/mood], [composition], [quality/style tags]`

### Negative template (starter)
`low quality, blurry, watermark, text, bad hands, extra fingers, extra limbs`
