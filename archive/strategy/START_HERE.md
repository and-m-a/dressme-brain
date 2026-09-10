---
created: 2026-08-31
updated: 2026-08-31
status: active
tags: [strategy, content, agent-context, editorial-window, storytelling, visual-direction, zametna]
---

# START HERE — ZAMETNA Content Strategy

> **Agent-facing canonical entry point. Read this file first before proposing, evaluating or generating ZAMETNA content.**
>
> The goal of this file is not to replace the detailed strategy docs. It gives a new agent the current architecture, current Editorial Window and the practical visual/storytelling rules that have already been decided, so we do not restart the same discussion from zero.

## 0. Canonical interpretation / precedence

When sources appear to conflict, use this order:

1. **Real current catalogue + stock + product photos** — source of truth for what can actually be sold and shown.
2. **Product references supplied to generation** — source of truth for exact garment appearance.
3. **Person identity anchors** — source of truth for the chosen recurring model identity.
4. **Current implemented Editorial Window snapshot** — current chapter/context for stylist and generation.
5. **This START_HERE file** — current strategy interpretation and practical content grammar.
6. Detailed strategy docs linked below — deeper rationale/history.
7. Old illustrative examples — do not treat them as current production truth if newer decisions exist.

Important example: older docs use `Back to Moscow / September` as an illustrative candidate. The currently implemented first Editorial Window is **September Soft Power**.

---

# 1. One-minute summary

ZAMETNA is a premium multi-brand women's fashion marketplace. The content goal is not to make isolated catalogue images prettier. The goal is to build a recognizable fashion world around **one ZAMETNA woman living different parts of her life**, while keeping every garment commercially readable and faithful to the real product.

Core architecture:

```text
PERSISTENT BRAND LAYER
Brand Narrative + Brand Policy + Master Story + Visual Language
                         ↓ constrains
CURRENT IN-STOCK CATALOGUE + Visual Passports
                         ↓
catalogue audit / supported editorial directions
                         ↓
human selects active Editorial Window
                         ↓
active Window + current stock
                         ↓
AI Stylist / VLM
                         ↓
approved outfit
                         ↓
Scene / Moment + Model + Visual Language + Environment
                         ↓
image / carousel / reel generation
                         ↓
product fidelity + editorial consistency evaluation
                         ↓
Content Pool
                         ↓
manual publication selection first
                         ↓
Instagram + analytics
```

**Critical rule:** story hierarchy is not production order. Never invent a beautiful Editorial Window first and then force the catalogue to fill it. The live catalogue determines which chapter is supportable now.

---

# 2. Persistent ZAMETNA world

## Brand feel

ZAMETNA should feel:

- premium;
- feminine;
- contemporary;
- polished;
- desirable;
- confident;
- metropolitan;
- sensual, but controlled rather than vulgar.

Working archetype mix:

- **Lover** — desire, beauty, femininity, sensuality;
- **Ruler** — status, confidence, control, refinement.

Occasional bold / rebel energy is allowed, but it must stay inside the same premium woman rather than create a new cheap/party/teenage brand personality.

North-star reaction:

> **“I want to look like this. I want this life / state / confidence.”**

---

# 3. Master Story

The Master Story is the life of a modern affluent woman in a big city.

She works, moves through the city, meets people, goes to dinners and dates, visits galleries/events, travels, spends time at home and has quieter everyday moments.

The important thing is that these are **not separate personas that require separate brands or feeds**. They are adjacent scenarios of one recognizable premium female audience.

Examples:

```text
morning / home
→ city / work / meeting
→ transition / after work
→ dinner / date / evening
→ weekend / gallery / relaxed city life
```

This is storytelling grammar, **not a required chronological publishing schedule**. Every post must still work independently in Feed / Reels / recommendations.

---

# 4. Editorial Window

**Editorial Window = temporary weighted editorial context / one current chapter.**

It is broader than “background” and narrower than the whole brand.

It may include:

- idea / chapter / emotional message;
- season;
- supported styles;
- scenario emphasis;
- formality / sensuality / boldness envelope;
- palette / material direction;
- product policy;
- model identity / visual-language context;
- location families / scene grammar;
- generation context.

It is **not**:

- a rigid sequence of 9 posts;
- a quota system;
- one fixed location;
- one single style such as “only quiet luxury”;
- a reason to publish a weak outfit.

Weights are priorities, not quotas.

---

# 5. Current first Editorial Window — September Soft Power

Current implemented snapshot lives in:

`dressme-backend/docs/strategy/editorial_window_1.json`

Current definition:

- **name:** September Soft Power;
- **season:** early autumn;
- **story:** a polished, confident and feminine ZAMETNA woman returns to the structured rhythm of the city after summer;
- **editorial direction:** polished urban femininity, soft tailoring, strong silhouettes, expensive textures, restrained sensuality;
- **core scenarios:** city day, work & meetings, dinner;
- **adjacent scenarios:** date, gallery;
- **avoid:** boring corporate uniform, cheap party aesthetic, teenage casual, excessive theatricality.

The Window should be able to contain several modes of the same woman:

- quiet luxury / soft tailoring;
- feminine elegant;
- more sensual evening / date;
- occasional fashion-forward expression.

The glue is not one style label. The glue is **the same woman, same premium taste level and same visual/story world**.

---

# 6. Main storytelling correction: stop thinking “background”, think SCENE / MOMENT

A major failure mode discovered during test generations:

```text
look 1 → woman posing in apartment
look 2 → woman posing in another interior
look 3 → woman posing in another expensive place
```

This is still a catalogue with different backgrounds.

For lifestyle/editorial content, generation should think:

```text
OUTFIT
+
WHERE she is
+
WHY she is there
+
WHAT is happening / what she is doing
+
WHAT moment of her day/life this is
+
HOW the camera catches that moment
```

A location must have a narrative reason.

Examples:

- at home, getting ready to leave, taking a bag from the table;
- crossing / waiting / arriving in the city;
- coming down architectural steps after a meeting;
- moving through a hotel/private-club lobby;
- waiting for an elevator before dinner;
- entering / leaving a restaurant;
- sitting after dinner, not “posing in a restaurant”;
- gallery / design-space moment;
- editorial interruption / portrait when the feed needs visual rhythm.

**Storytelling is not “candid = good”.** Deliberate fashion posing is allowed and often desirable. The key is that the pose has energy, personality and a relationship with the scene.

---

# 7. Fashion energy / pose / emotion

Do not default to neutral e-commerce stance.

Bad default:

- centered full-body catalogue framing;
- both arms relaxed at sides;
- neutral face;
- generic “walking toward camera” shot;
- same eye-level distance every time;
- body posed independently from the location.

Desired direction:

- strong asymmetry;
- expressive silhouette;
- body tension or relaxed attitude appropriate to the scene;
- interaction with architecture / furniture / wall / stairs / car / elevator / table;
- varied camera distance and angle when useful;
- hair / gaze / hands / posture contributing character;
- controlled sensuality where appropriate;
- occasional intentionally strange / memorable fashion pose;
- scene-driven body position rather than mechanical catalogue instructions.

Useful prompt language:

> **Strong fashion-editorial body language with personality and controlled sensuality. The subject may deliberately pose, but never in a neutral e-commerce stance. Use asymmetry, body tension, interaction with the architecture and an expressive silhouette. The pose should feel charismatic and visually memorable rather than catalog-correct.**

Avoid overcorrecting into “do not pose / purely candid”. The reference feeds show that **fashion energy is often highly posed**, just not sterile.

---

# 8. Environment system: hard product, hard identity, soft world

For generation, separate reference roles clearly.

## Product references — HARD

Selected product references are hard constraints.

Preserve as close to 1:1 as possible:

- exact category;
- silhouette / cut;
- fit intention;
- proportions;
- colour / blocking;
- fabric texture / weight / shine / transparency;
- seams;
- neckline / collar / sleeves;
- waistband / rise;
- pockets;
- hem / length;
- closures / hardware / trims;
- distinctive design details.

**Product fidelity has priority over creative scene choices.**

Real product photos are the visual truth if metadata / Visual Passport conflicts.

## Person identity — HARD

The recurring model / identity anchor is the only identity source.

Product-reference people must never replace the selected model identity.

Keep:

- face identity;
- hair identity;
- skin tone;
- body proportions.

Identity drift across posts damages the “one ZAMETNA woman” storytelling idea.

## Environment — usually SOFT

Background/location usually should **not** be copied 1:1.

Use three modes:

### `generative`
Describe the location family, mood, materials, light and scene. Model invents a new believable place.

### `reference_guided`
Use one or several environment images only for:

- atmosphere;
- material language;
- palette;
- light;
- spatial character;
- camera / editorial energy.

Create a **new** location in the same visual family. Do not copy the literal room or any person/outfit from that reference.

### `continuity`
Use when creating another shot from the **same shoot / same place**. Then preserve recognizable architecture, furniture/material arrangement and lighting direction.

This distinction is important: **environment reference is normally a vibe / world reference, not an exact product-like constraint.**

---

# 9. Location / scene families for September Soft Power

Do not use one background. Use recurring families inside one world.

## 1. City architecture

- stone facades;
- stairs;
- columns;
- restrained Moscow / European urban architecture;
- glass, concrete, granite, entry groups;
- Moscow should often be **felt rather than landmark-labeled**.

Good for: city day, work, meetings, tailoring.

## 2. Hotel / private club / elegant public interior

- lobby;
- corridor;
- staircase;
- wood;
- dark stone;
- restrained seating;
- expensive but no gold-heavy “luxury showroom”.

Good for: polished day → evening transition, dinner arrival, meeting.

## 3. Gallery / design space

- modern art;
- big surfaces;
- clean architecture;
- unusual framing / negative space.

Good for: fashion-forward / expressive moments.

## 4. Restaurant / bar / evening interior

- dark wood / stone;
- leather seating;
- pools of warm light;
- intimate but not nightclub.

Good for: dinner, date, controlled sensuality.

## 5. Editorial studio

- grey / warm-white / charcoal / almost black;
- hard light / shadow;
- chair / floor / graphic composition;
- occasional B&W.

**Never default to white e-commerce studio.**

Good for: statement frames and feed rhythm.

## 6. Modern apartment / home

- warm urban apartment rather than sterile white showroom;
- walnut / taupe / cream / brown;
- wood, stone, plaster, restrained textiles;
- lived-in but uncluttered.

Use only when there is a **real scene / action**: getting ready, leaving, phone call, bag, coffee, mirror, transition. Do not make the woman simply stand and pose in different apartments.

---

# 10. Instagram reference grammar

Reference accounts:

- https://www.instagram.com/abuladze.svetlana/
- https://www.instagram.com/gavrilovaal/

Use them as **Instagram / fashion-world references**, not exact locations or outfits to copy.

What we borrow:

- coexistence of quiet luxury, feminine and more sensual looks;
- premium feminine corridor;
- strong fashion posing;
- mix of city / studio / interior;
- occasional B&W / portrait / detail interruptions;
- real city energy;
- sunlight / imperfection / spontaneous-feeling frames;
- different scenes without losing one recognizable visual world.

Desired hybrid:

```text
fashion editorial coherence
+
real city / personal-diary liveliness
-
selfie/random-travel clutter
-
sterile catalogue feel
```

See `strategy/reference_analysis.md` for the fuller breakdown.

---

# 11. AI Stylist + Editorial Window

Editorial Window must be passed **inside** stylist reasoning, not only added after outfit selection.

Important stages:

- **SelectAnchor** → Window affects anchor weighting / acceptance;
- **DeriveDirections** → Window is in the prompt/context;
- **RankByPassports** → Window is in the prompt/context;
- **CompareImages** → VLM asks both “does this outfit work?” and “does it belong to this chapter?”;
- strong off-window candidate may go to Bench / future Content Pool rather than be forced into the current Window.

Current goal remains pragmatic: find approximately **1–2 genuinely strong publishable outfits/day**, not exhaustively score all combinations.

Visual Passport is a cheap structured retrieval/scoring layer. Real product photos are final visual truth.

---

# 12. Generation context after outfit approval

After the outfit is selected, build a **Generation Context** rather than sending only “make fashion photo”.

Useful fields/concepts:

```text
Editorial Window snapshot
+ model identity
+ product references
+ scene / chapter moment
+ location family
+ environment mode
+ environment mood reference(s), if any
+ visual language / preset
+ lighting
+ camera behavior
+ framing
+ fashion energy / pose language
+ aspect ratio
```

Important: scene/action and pose should be designed together.

A pose should not be specified as a generic fixed template such as `body turned 20–30° left, relaxed arms` for every lifestyle shot. That language repeatedly produces plastic e-commerce posing.

---

# 13. Evaluation after generation

At minimum keep two separate checks:

## Product fidelity

Did generation reproduce the real selected products correctly?

## Editorial consistency / creative quality

Does the image feel like part of the current ZAMETNA chapter?

Check:

- identity consistency;
- scene plausibility;
- fashion energy / charisma;
- pose quality;
- realism;
- premium taste level;
- location/story coherence;
- no sterile catalogue feel;
- no cheap/vulgar aesthetic;
- garment remains readable.

A beautiful frame with incorrect products is rejected. A perfectly faithful but dead/plastic frame can be regenerated.

---

# 14. Human-in-the-loop rule

The current strategy deliberately keeps human editorial control where taste is still hard to automate.

Human should currently be allowed to:

- select the Editorial Window;
- approve/reject outfit candidates;
- choose among generation variants;
- reject low-charisma / plastic / boring frames;
- choose publication from approved Content Pool.

Log these decisions so evaluation layers and approval rate can improve later.

Do not build a complex automatic publication router before enough real decisions/performance exist.

---

# 15. Things a new agent should NOT do

Do not:

- reinvent the whole strategy unless explicitly asked;
- treat Editorial Window as a calendar / fixed sequence;
- force weak outfits to satisfy scenario percentages;
- treat four audience labels as four totally separate women by default;
- choose a Window without catalogue support;
- use product-reference people as model identity;
- sacrifice product fidelity for creative composition;
- make every frame a white/beige studio catalogue shot;
- make every lifestyle frame “woman standing in expensive interior”;
- interpret storytelling as “no posing / only candid”;
- use generic safe poses with no charisma;
- copy an environment mood reference literally unless mode is `continuity`;
- let a dramatic background overpower the products;
- drift into teenage casual, cheap party, vulgarity or theatrical luxury.

---

# 16. Detailed sources to read when needed

## dressme-brain

- `strategy/content-strategy.md` — full content architecture and rationale.
- `strategy/storytelling.md` — Master Story / one-woman storytelling model.
- `strategy/reference_analysis.md` — Instagram reference-feed analysis.
- `strategy/content-factory-reference-pool.md` — approved visual reference pool direction.
- `strategy/brand-dna-draft.md` — brand DNA.
- `strategy/archetypes.md` — Lover / Ruler and supporting archetypes.
- `strategy/ии-стилист.md` — stylist strategy.
- `strategy/ии-контент-завод.md` — content-factory business / product context.
- `strategy/Human in the Loop.md` — manual steps to retain/log/automate gradually.

## dressme-backend

- `docs/strategy/Content Direction.md` — compact AI-facing architecture.
- `docs/strategy/AI Content Factory.md` — operational content-factory architecture.
- `docs/strategy/editorial_window_1.json` — current implemented `September Soft Power` snapshot.

---

# 17. Default behavior for a new agent

If a user asks to work on ZAMETNA content strategy, Editorial Window, AI stylist, generation direction, Instagram feed or visual consistency:

1. Read this file first.
2. Preserve the architecture unless the task explicitly asks to challenge it.
3. Load only the linked detailed docs relevant to the specific task.
4. If choosing content direction, start from current catalogue support.
5. If generating an image, distinguish hard product / hard identity / soft environment roles.
6. Think in **scene + moment + fashion energy**, not simply background + pose.
7. Keep the same recognizable ZAMETNA woman and premium world across different life scenarios.
8. Prefer a smaller number of strong publishable results over exhaustive enumeration.

The objective is not “AI-looking luxury content”. The objective is **real-feeling, commercially faithful fashion content with a recognizable woman, narrative life and editorial taste.**
