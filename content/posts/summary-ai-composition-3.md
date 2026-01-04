---
title: "Intermediate Composition Tricks for AI Image Prompts"
date: 2025-07-08
draft: false
toc: false
images:
tags:
  - Generative AI
---

*Original article: [Intermediate Composition Tricks to Instantly Improve AI Images Using Prompts](https://civitai.com/articles/16712/intermediate-composition-tricks-to-instantly-improve-ai-images-using-prompts)*

This guide pushes beyond the fundamental composition rules into more advanced techniques.  Each section below outlines the core idea, why it works and how to translate it into AI‑prompt wording.  Citations refer back to the original article for further detail when needed.

## Implied motion & lead room

When a subject is moving or looking in a particular direction, leaving empty space in front of them creates an anticipatory feel.  Prompts should describe motion or gaze and explicitly mention the open space ahead—for example, “sprinter bursting from blocks, motion blur trailing behind her, **open track ahead**”.  This lead room helps the model position the subject off‑centre and suggests movement.

### Practical prompt tips

* Use verbs like *running*, *flying*, *charging* to convey motion.
* Mention “open road ahead,” “empty sky before him,” or similar to ensure space in front of the subject.
* Combine with motion blur for extra dynamism.

## Visual flow & eye movement

Visual flow guides the viewer’s eye through the scene using curves, lines or an S‑curve.  Prompts should describe paths or sequences of objects that lead to the subject, such as “a winding river curves toward a distant castle, drawing the eye through the landscape”.  Specifying foreground, middle and background layers helps the model arrange these elements appropriately.

### Prompt suggestions

* Include a leading element like a road, bridge or row of lanterns that guides the gaze.
* Describe the path’s curvature (“S‑shaped road”) or progression (“series of stepping stones”).
* Explicitly mention layers: “flowers in the foreground, a path in the mid‑ground, and mountains in the background.”

## Juxtaposition

Placing contrasting subjects together (large versus small, old versus modern, natural versus man‑made) creates tension and interest.  The prompt should clearly state the two elements and their relationship, e.g., “a tiny cottage dwarfed by a futuristic skyscraper towering behind it”.  This contrast encourages the model to render both elements and their scale difference.

### Prompt suggestions

* Pair opposites (fragile vs robust, bright vs dark) and describe their sizes.
* Use descriptive adjectives: “ancient stone temple beneath a gleaming glass dome.”
* Clarify the spatial relationship (behind, looming over, side by side).

## Colour balance & harmony

Colour choices affect mood and composition.  The article suggests using complementary colours (opposites on the colour wheel like blue/orange) or analogous schemes (neighbouring hues like green/teal).  Prompts should name the colours and where they appear, such as “a sunset scene with warm orange sky contrasting with a cool blue river”.  Hi‑Dream and SDXL models respond well when colour palettes are specified.

### Tips

* State the colour pairs and their placement (foreground, background, clothing).
* Mention light sources if relevant (“neon pink signs reflect on wet streets”).
* Use palette keywords like “complementary colours of orange and teal” or “analogous greens and teals”.

## Foreground interest & framing elements

Adding objects in the foreground creates depth and frames the main subject.  Prompts should specify what occupies the foreground and what appears in the background, like “wildflowers in the foreground frame a rustic cottage in the mid‑ground with mountains beyond”.  Overhanging branches, arches or windows can naturally frame the subject.

### Prompt guidelines

* Clearly separate foreground, mid‑ground and background elements.
* Use framing phrases: “framed by overhanging branches” or “seen through a gothic arch.”
* Combine with depth words (“layers of depth”) to encourage spatial separation.

## Scale & proportion

Contrasting sizes emphasise drama.  Describe one element as tiny or dwarfed by another, e.g., “a lone traveller dwarfed by towering canyon walls”.  Use adjectives like *gigantic*, *monumental* or *miniature* and specify the relationship (“at the base of”) to help the model depict the size difference.

### Tips

* Use words like *dwarfed by*, *looming*, *towering over* to emphasise disparity.
* Combine with wide‑angle or low‑angle prompts for added grandeur.
* Contrast not just physical size but conceptual scale (e.g., “a child reaching toward a colossal robot hand”).

## Framing with light & shadow

Lighting can frame a subject by isolating it against darkness or spotlighting it.  Prompts might mention “a single bright spotlight illuminating the dancer while the rest recedes into darkness” or “sunlight streaming through a window framing a cat”.  This high‑contrast lighting draws the viewer’s attention.

### Prompt suggestions

* Specify the light source: spotlight, shaft of light, sunset glow.
* Mention contrasting dark surroundings to enhance focus.
* Combine with chiaroscuro or rim lighting techniques from the light‑and‑shadow guide for further nuance.

## Overlapping & layered subjects

Partial occlusion of elements builds depth.  Prompts should describe scenes where objects overlap, such as “vendors in the foreground partially blocking shoppers behind them with market stalls receding into the background”.  Use position words (in front of, behind) to ensure the model arranges layers correctly.

## Framing through reflections & transparent surfaces

Reflections in water, mirrors or glass add symmetry and depth.  Prompt examples include “a snow‑capped mountain reflected perfectly in a still lake” or “a portrait seen through a rain‑streaked window with city lights reflecting”.  Mention the reflective surface and the subject to get accurate results.

### Tips

* Use words like *reflected*, *mirror*, *through glass*.
* Describe the texture of the reflective surface (rippling water, polished floor).
* Encourage symmetry if desired (“symmetrically reflected in calm water”).

## Framing with negative shapes & cut‑outs

Silhouettes and cut‑out shapes can frame the subject and create striking contrasts.  For instance, “view from inside a dark cave looking out to a bright beach” or “portrait silhouette against a fiery sunset sky”.  The dark foreground acts as a frame while the bright background contains the subject.

### Prompt guidance

* Specify the dark foreground element and the bright scene beyond.
* Use terms like *silhouette frame*, *cut‑out*, *negative shape*.
* Describe the contrast in lighting and colour to emphasise the framing.

## Final thoughts

The article encourages mixing these techniques once you’re comfortable.  Combining visual flow with scale or light‑framing can produce rich, story‑driven images.  Iterate on prompts and adjust language to guide the AI model effectively.