---
name: research-text-to-figure
description: Turn user-provided biomedical, life-science, medical, or other research text into one publication-oriented conceptual mechanism figure by building an evidence-grounded visual plan and invoking the installed imagegen skill. Use when the user asks for 文生图、科研绘图、研究内容生成机制图、BioRender 风格图、graphical abstract, mechanism schematic, or supplies research notes or a summary and asks for a scientific figure. Do not use for extracting evidence from a paper file, DOI, or URL; use literature-to-mechanism-figure instead.
---

# Research Text to Figure

Generate exactly one final scientific image from research text supplied by the user. Default to a 16:9 landscape composition, white background, clean flat biomedical vector illustration, and a restrained BioRender-inspired visual language suitable for a manuscript or academic presentation.

## Input gate

- Require non-empty research content. If the request ends at `研究内容：` or otherwise omits the content, ask the user to provide it and stop.
- Accept optional constraints such as target journal, required labels, organisms, tissues, cell types, palette, or label language.
- Treat user-provided scientific statements as the only source of truth. Do not silently add literature knowledge.

## Workflow

1. Extract an internal fact sheet from the supplied text:
   - biological entities, compartments, interventions, exposures, inputs, and outputs;
   - temporal or spatial order;
   - explicitly stated activation, inhibition, transport, binding, differentiation, or outcome relationships;
   - uncertainty, association, hypothesis, and negative or null findings.
2. Separate explicit claims from plausible inference. Draw only explicit claims. If the text does not support a mechanism, create a conceptual summary or workflow rather than presenting speculation as a mechanism.
3. Build one internal visual plan with a single reading path. Prefer 3–6 major stages arranged left-to-right. Use inset panels only when compartment or scale changes are essential.
4. Keep visible wording minimal. Preserve requested labels verbatim. Otherwise use the language of the source text; when the source mixes languages, default visible scientific labels to English.
5. Load and follow `$imagegen`. Use its built-in `image_gen` route, not the CLI fallback, unless the user explicitly requests the CLI/API route.
6. Generate one candidate by default. If factual validation fails, make a targeted correction and show only the final accepted image.

## Image-generation brief

Adapt the following brief without weakening its scientific constraints:

```text
Use case: scientific-educational
Asset type: publication-oriented biomedical mechanism schematic
Primary request: You are an experienced scientific illustration designer. Based only on the research content and the evidence-grounded visual plan below, create one corresponding BioRender-inspired scientific mechanism figure suitable for research communication.
Research content: <user-provided research text>
Evidence-grounded visual plan: <explicit entities, relationships, direction and uncertainty>
Style/medium: clean flat biomedical vector illustration; polished scientific iconography; restrained professional BioRender-inspired aesthetic; not a photograph
Composition/framing: one coherent 16:9 landscape figure; left-to-right logical flow; generous whitespace; balanced hierarchy; no multi-option contact sheet
Scene/backdrop: pure white background
Color palette: restrained, colorblind-conscious scientific palette with consistent semantic colors
Text: short, legible sans-serif labels only; preserve the approved labels verbatim
Constraints: every node and arrow must be supported by the supplied text; distinguish activation, inhibition, association and hypothesis visually; keep anatomy, organelles and molecular direction scientifically coherent
Avoid: invented mechanisms, invented biomarkers, invented cell types, invented numerical values, unsupported causal arrows, decorative clutter, gradients, glossy 3D effects, dark background, figure number, caption, logo, watermark, citation text, illegible microtext
Output: exactly one image
```

## Validation

Before delivery, compare the image with the fact sheet and verify:

- every entity, arrow direction, compartment and outcome is supported;
- association is not depicted as causation and hypotheses are visibly tentative;
- labels are spelled correctly and no unwanted text appears;
- the result is one coherent 16:9 figure on a white background;
- no decorative element could be mistaken for data or evidence.

Render exactly one final image inline. Keep the accompanying message brief. If the user specified a destination, save the selected output there according to `$imagegen` rules.
