# Tend (working name): handoff for a new session

This file carries everything decided in the first session. Read it fully before doing anything. The user is not a developer by default; keep explanations plain and short.

## 1. What this project is
A personalized dental routine app. Patient information plus clinical rules produce a short daily oral-care routine. Phase 1 is product discovery and visual design only. The user said: do not build the complete application yet.

Guiding brief from the user: combine clinical intelligence (grounded in dental science, safe), personalization (not a generic checklist), and an exceptional, modern consumer-health experience. Think independently, challenge assumptions, avoid feature bloat, treat clinical accuracy and patient safety as foundational.

## 2. Decisions made
- **Direction C (approved by the user):** self-serve first, dentist-confirmable. Anyone can start in about five minutes. A profile can later be "confirmed by my dentist" through a code or shareable summary, which unlocks clinician-only rules (for example prescription-strength fluoride).
- **Wedge users:** adults whose mouths changed: implant, crown, bridge, braces or aligners, or gum disease history. Then people with diabetes, dry mouth or age 65+. Healthy adults later. **Children are a separate product** (different rules, buyer and consent).
- **Product thesis:** the value is subtraction. Pick the few actions that matter most for this person and fit them in a time budget (about 8 minutes a day ceiling). Show what was "left out on purpose".
- **Engine:** deterministic rules, not AI. Versioned YAML rules in git. Each rule has conditions, action, slot, priority, evidence grade (A, B, C, Consensus, Ask), sources, region tags, safety class, named dentist reviewers, review expiry and escalation triggers. Pipeline: profile, safety gate, match, supersede (specific replaces general), constrain (timing conflicts, for example fluoride rinse 30 minutes from brushing), budget, explain. An LLM may later reword approved text or answer questions constrained to approved rules. It never decides advice.
- **Safety gate first:** red-flag answers (swelling or pus, loose tooth or implant, mouth sore over 3 weeks, pain that wakes you, facial swelling with fever, trouble swallowing or breathing, recent oral surgery) stop the routine and point to a dentist or urgent care.
- **Hard guardrails:** no diagnosis language; no prescription product (chlorhexidine, 5000 ppm paste) shown as an instruction, only "ask your dentist"; same profile always gives the same output; no camera plaque detection in v1.
- **Habit design:** forgiving. Weeks and partial credit, no streaks. Finishing a routine unlocks one of 30 short "insights" (a collection, not a score). Weekly gum check-in (bleeding less, same, more) is the headline progress metric. Dentist visit loop with a shareable one-page summary.
- **UI direction:** bento tiles. Tile sizes 1x1, 2x1, 2x2. One hero tile per screen (the next action). Morning and night modes. Four tabs: Today, Routine, Progress, My mouth. Why-this sheet on every recommendation (reason, evidence label, reviewer, "ask my dentist"). Guided brushing timer with quadrant cues that mention the user's implant.
- **Platform suggestion:** responsive web app or PWA for the research prototype, native later if retention proves out.
- **Prototype plan:** about 6 weeks. Static research prototype (React and Vite, TypeScript engine reading YAML rules, 15 to 20 draft rules, local storage, no accounts), 12 participant sessions, 3 to 5 dentist reviews. Success: at least 10 of 12 finish intake in under 5 minutes, 9 of 12 can say why their top step matters, 8 of 12 would follow it a month, zero "unsafe" ratings from dentists on core rules.

## 3. Draft rule catalog (about 35 rules, unreviewed)
Groups and IDs: Safety RF-001 to RF-005; Base BR-001 to BR-003, IC-001, IC-002, TN-001; Restorations IM-001 to IM-003, CR-001, BG-001, DN-001; Ortho OR-001 to OR-004; Gums GM-001, GM-002, PD-001, PD-002; Risk FR-001, FR-002, DM-001, DM-002, CV-001, MW-001; Add-ons and systemic WF-001, SY-001 to SY-003. Full table with triggers, wording, priority and proposed evidence is in `pages/tend-v1-plan.html`. **All clinical content is illustrative and has not been reviewed by a dentist. Never present it as advice.**

## 4. Visual design status
- Three early pages (concept, v1 plan, original bento mockup) use the first palette: enamel #EEF1F0 ground, ink #101C25, blue #3547D9, mint, coral, with Bricolage Grotesque, DM Sans and JetBrains Mono.
- The user did **not** like the first Headspace-inspired recolour and asked for colour samples from established health apps instead. **No palette has been chosen yet.**
- The canvas has a "Palette samples" board showing the Today screen in six palettes. Hex values:
  - Withings-style (sampled from withings.com): ground #FFFFFF, card #F2EEEA, ink #0F0F0F, periwinkle #6784FE, alert #D93421.
  - Ente-style (sampled from ente.com): ground #FFFFFF, ink #282828, yellow #FBCF00, green #08C225 (tints are invented).
  - Oura-style (sampled from ouraring.com): ground #F7F1E8, text #4A4741, navy #27455C, blue #2A72DE.
  - Fitbit-style: teal #00B0B9 **recalled from memory, not sampled** (fitbit.com redirects to the Google store). Verify before relying on it.
  - Headspace-style (sampled from headspace.com): ground #FFFFFF, blush #F9F4F2, charcoal #2D2C2B, yellow #FFCE00, blue #0061EF, orange #FF7A1A, pink #FFA1CC, navy #27455C.
  - Google Health-style (sampled from health.google): ground #F8F9FA, ink #202124, blue #1A73E8 and #0B57D0, tonal #D3E3FD, grey #5F6368. Error red #B3261E is a Material default, not sampled.
- **Brand rule:** take colour and layout inspiration only. Do not copy any company's logo, illustrations, wordmark or name. "Replicate exactly" was declined for that reason; the user then asked for samples instead.
- The artboard files currently contain stacked palette blocks (v1 base, "v2", "v3 supersedes v2") in each file's `<style>`. When a palette is chosen, collapse them into one clean token block.

## 5. Files in this repo
- `pages/tend-concept.html`: strategy, users, three directions, phone mockups, live rules demo, scope, risks. Open it in a browser.
- `pages/tend-v1-plan.html`: rule schema, full rule catalog, test approach, prototype plan, decisions list.
- `pages/tend-bento.html`: interactive bento mockup (tap steps, guided brushing at 6x speed, morning and night, four tabs, set-up screens).
- `artboard/project/`: source of the "Tend Artboard" design canvas. `canvas.json` is the index (positions, order, notes). Screens: Main (Today), Routine, Progress, Mouth, Brushing, Why, Intake, Plan, Safety, Palettes. Each `.dc.html` has two tweaks, Night mode and Tile radius (16, 24, 32). Tab icons on the first four link to each other. These files need the Design canvas runtime (`support.js`, supplied by the artifact host) and do not render on their own.
- Published private copies on claude.ai (may be unavailable in a different account): concept https://claude.ai/artifact/MoX7wFv47QJgaXn1WZTniB, v1 plan https://claude.ai/artifact/TDnrtBwxaVE6NtNFMinAoE, bento https://claude.ai/artifact/CdNfRXy61xhnypSrjXJpLa, canvas https://claude.ai/artifact/CxEZ8DRxFHUcuE2cHJtp85.

## 6. Open decisions
1. Region for the prototype (US, UK or EU), so fluoride and guideline sources stay consistent.
2. Dentist advisors: a periodontist, a prosthodontist and an orthodontist, or plan recruitment.
3. Who sources the 12 participants.
4. Build scope: static research prototype (recommended) or a real app shell with accounts.
5. The name. "Tend" is a placeholder; check trademark and domain before showing it to participants.
6. The final colour palette.
7. Business model (consumer subscription, dentist-paid, or free with referral).

## 7. Known risks
Clinical liability; medical-device regulation if triage drifts toward diagnosis; health-data privacy (HIPAA, GDPR); guideline differences between countries; retention of habit apps; and whether users trust an app over their own dentist.

## 8. Working preferences observed
- The user wants to see things visually, not read long documents. Deliver mockups and tweakable canvases.
- Keep the look clean, premium, intuitive, and habit-forming.
- Be concrete and short. Recommend one option rather than listing many.
- Ask before publishing, deleting or pushing anything outward-facing. The user decided to keep the project local-only for now and removed git metadata from the project folder.
- The user may work from an iPad; published pages are the easiest way to review.

## 9. Suggested next steps
1. User picks a palette from the samples; collapse palette blocks and apply it to all artboards and the interactive bento page.
2. Polish pass on icons, spacing, tile hierarchy and motion (the user said they would give specifics).
3. Design the missing screens: reminders and notifications, the dentist summary (PDF or link), the clinician console, empty and first-run states.
4. Answer open decisions 1 to 5, then build the research prototype per the v1 plan.
