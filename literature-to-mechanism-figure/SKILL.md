---
name: literature-to-mechanism-figure
description: Extract the abstract and/or conclusion from a scientific paper, identify source-supported claims, convert them into an evidence-grounded visual plan, and invoke the installed imagegen skill to return one 16:9 white-background scientific mechanism figure. Use when the user provides a PDF, DOI, article URL, title, abstract, conclusion, or pasted literature text and asks for 文献生图、论文摘要绘图、结论绘图、BioRender 风格机制图、graphical abstract, or a paper-to-figure visualization.
---

# Literature to Mechanism Figure

Turn a paper's abstract or conclusion into exactly one source-grounded scientific figure. Default to a 16:9 landscape composition, pure white background, clean flat biomedical vector illustration, and a restrained BioRender-inspired visual language suitable for research communication.

## Source handling

- Accept a local PDF, DOI, article URL, title, pasted abstract, pasted conclusion, or full text.
- Prefer author-provided or publisher text over search snippets. Use available PDF, web, literature, or local-library tools to obtain the requested section legally.
- For a full paper, extract both the Abstract and the final Conclusion when available. Treat `Discussion`, `Summary`, `Interpretation`, or the final discussion paragraphs as the conclusion only when the paper has no dedicated Conclusion section.
- If the user requests only the abstract or only the conclusion, honor that scope.
- If neither section can be accessed, ask for the PDF or pasted text. Do not generate from a title or search snippet alone.

## Evidence extraction

1. Confirm the paper identity and section provenance internally.
2. Extract only claims needed for the visual story:
   - research system and context;
   - intervention, exposure, comparison, or input;
   - key entities and compartments;
   - reported relationships and directionality;
   - principal outcomes;
   - uncertainty, limitations, associations, hypotheses, and null results.
3. Create an internal evidence map. For every proposed arrow, retain the supporting sentence and classify it as causal, associative, inhibitory, activating, temporal, spatial, or hypothetical.
4. Do not upgrade language. `Associated with`, `may`, `suggests`, and `could` must not become proven causal mechanisms. Depict proposed relationships with dashed arrows or uncertainty markers.
5. Use exact numerical values only when central to the conclusion and explicitly stated. Never fabricate sample sizes, effect sizes, pathways, biomarkers, doses, or time points.
6. If the abstract/conclusion reports outcomes but no mechanism, create a conceptual graphical abstract or result pathway instead of falsely labeling it a mechanism figure.

## Figure planning and generation

1. Plan one central message with 3–6 major stages in a left-to-right reading path. Use a multiscale inset only when the paper explicitly links organism, organ, cell, organelle, or molecular levels.
2. Keep labels minimal. Preserve author terminology. Default visible labels to the paper's language; for an English paper, use English labels.
3. Load and follow `$imagegen`. Use the built-in `image_gen` route unless the user explicitly requests the CLI/API route.
4. Generate one candidate by default. If the output contradicts the source, make a targeted correction and expose only the final accepted image.

## Image-generation brief

Adapt this brief using only the evidence map:

```text
Use case: scientific-educational
Asset type: literature-grounded graphical abstract or biomedical mechanism schematic
Primary request: You are an experienced scientific illustration designer. Using only the extracted abstract/conclusion evidence below, create one corresponding BioRender-inspired scientific figure suitable for research publication and communication.
Paper scope: <title and sections used>
Grounded research content: <concise abstract/conclusion synthesis>
Evidence-grounded visual plan: <approved entities, compartments, relationships, arrow types and outcomes>
Style/medium: clean flat biomedical vector illustration; polished scientific iconography; restrained professional BioRender-inspired aesthetic; not a photograph
Composition/framing: one coherent 16:9 landscape figure; left-to-right logical flow; generous whitespace; balanced hierarchy; no multi-option contact sheet
Scene/backdrop: pure white background
Color palette: restrained, colorblind-conscious scientific palette with consistent semantic colors
Text: short, legible sans-serif labels only; preserve author terminology verbatim
Constraints: every node and relationship must be supported by the extracted abstract or conclusion; visually distinguish association, causation, inhibition and hypothesis; preserve scientific direction and compartment logic
Avoid: invented mechanisms, invented biomarkers, invented cell types, invented numerical results, unsupported causal arrows, overstated certainty, decorative clutter, gradients, glossy 3D effects, dark background, title block, figure number, caption, logo, watermark, citation text, illegible microtext
Output: exactly one image
```

## Final audit and delivery

Compare the image against the evidence map and verify:

- each depicted relationship is traceable to the abstract or conclusion;
- uncertainty and association are not rendered as established causality;
- labels, arrows, compartments and outcomes are correct;
- the result is one coherent 16:9 image with a white background;
- nothing decorative could be mistaken for experimental data.

Render exactly one final image inline. State whether the figure was grounded in the abstract, conclusion, or both. Do not expose the full evidence map unless the user asks for it. If the user specified a destination, save the selected output there according to `$imagegen` rules.
