# Tend (working name): dental routine planner

Product discovery and visual design. Nothing here is built as a real app yet.

## Decisions so far
- Direction C: self-serve first, dentist-confirmable (profile can later be confirmed by a dentist).
- Wedge: adults with restorations (implant, crown, bridge), braces or aligners, or gum disease history. Children are a separate product.
- Engine: deterministic, versioned YAML rules, each with evidence grade, named dentist reviewer and expiry. No LLM decides advice; an LLM may only reword approved text later.
- Safety gate first: red-flag answers stop the routine and point to a dentist.
- UI: bento tiles, one hero tile per screen, morning and night modes, no streaks (weeks and partial credit).
- Palette: still undecided. Samples (Withings, Ente, Oura, Fitbit, Headspace, Google Health styles) are on the artboard canvas. Do not copy any brand's logo, illustrations or wordmark.

## Layout
- `pages/tend-concept.html`: strategy page, first mockups, live rules demo.
- `pages/tend-v1-plan.html`: rule schema, draft v1 rule catalog, six-week prototype plan.
- `pages/tend-bento.html`: interactive bento mockup (original palette).
- `artboard/project/`: source of the "Tend Artboard" design canvas (`canvas.json` plus one `.dc.html` per screen). These files need the Design canvas runtime to render; they are a backup of what is published.

## Published copies (private, claude.ai)
- Concept: https://claude.ai/artifact/MoX7wFv47QJgaXn1WZTniB
- v1 plan: https://claude.ai/artifact/TDnrtBwxaVE6NtNFMinAoE
- Bento mockup: https://claude.ai/artifact/CdNfRXy61xhnypSrjXJpLa
- Artboard canvas: https://claude.ai/artifact/CxEZ8DRxFHUcuE2cHJtp85

## Caveats
- All clinical content is illustrative and not reviewed by a dentist.
