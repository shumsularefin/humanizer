# StoryScope feature reference

> Imported from the fiction `humanizer` skill. These are fiction measurements; `SKILL.md` Layer 8 maps the transferable patterns to academic prose. The fiction-only features (fourth wall, flashbacks, subplots) are not applied to papers.

Source: Russell, Rajendhran, Pham, Iyyer & Wieting, "StoryScope: Investigating idiosyncrasies in AI fiction," COLM 2026 (arXiv 2604.03136v6). 10,272 prompts × 6 sources = 61,608 stories, mean 4,753 words. 304 features across 10 NarraBench dimensions. Sources: human (Books3), Claude Sonnet 4.6, GPT-5.4, Gemini 3 Flash, DeepSeek V3.2, Kimi K2.5.

## Contents

1. [Headline results](#headline-results)
2. [All 30 core features with means](#all-30-core-features-with-means)
3. [Per-source fingerprints](#per-source-fingerprints)
4. [Rarity and clustering](#rarity-and-clustering)
5. [Robustness to stylistic editing](#robustness-to-stylistic-editing)
6. [Dimension abbreviations](#dimension-abbreviations)

## Headline results

Binary human vs. AI detection (macro-F1):

| Feature set | Size | F1 | AUPRC |
|---|---|---|---|
| Narrative only | 257 | 93.2 | .959 |
| Core only | 30 | 84.8 | .828 |
| Core + fingerprint | 101 | 91.1 | .934 |
| Narrative + style | 304 | 96.0 | .982 |
| Style only | 39 | 85.8 | .867 |
| ModernBERT (raw text) | — | 99.9 | 1.00 |
| Binoculars (zero-shot) | — | 55.9 | .404 |

Narrative features alone recover 97% of the combined model's performance. Six-way authorship attribution: 68.4% macro-F1 narrative-only, 77.3% with style, against 16.7% chance.

Per-class F1 in the six-way task (with style / narrative only): Human 93.0 / 88.5, Claude 89.3 / 77.1, GPT 82.1 / 73.0, Gemini–DeepSeek–Kimi 65.8–66.8 / 55.2–59.6.

## All 30 core features with means

Gap = Human − AI. Negative gaps are AI-elevated. `s` = 1–5 Likert mean, `o` = ordinal mean over integer codes, `→` = prevalence % of that option. AI column averages all five models.

### AI-elevated: thematic over-determination

| Feature | Human | AI | Gap |
|---|---|---|---|
| Thematic Explicitness & Moralizing `s` | 3.28 | 3.94 | −0.65 |
| Moral / Philosophical Weighting `s` | 3.26 | 3.68 | −0.42 |
| Thematic Unity `s` | 4.41 | 4.74 | −0.33 |
| Narratorial Thematic Commentary → yes | 52% | 77% | −25 |
| Dialogue Function → philosophical debate | 34% | 59% | −25 |
| Reference Explicitness → implicit echoes | 50% | 72% | −22 |

### AI-elevated: sensory & embodied performativity

| Feature | Human | AI | Gap |
|---|---|---|---|
| Emotional Expression → embodied | 38% | 81% | −42 |
| Setting as Psychological Mirror `s` | 3.58 | 4.07 | −0.49 |
| Environmental & Ecological Emphasis `s` | 2.83 | 3.21 | −0.38 |
| Sensory Modalities → olfactory | 57% | 82% | −26 |
| Sensory Density `s` | 3.66 | 3.93 | −0.26 |
| Depth of Interior Access `s` | 3.67 | 3.93 | −0.26 |

### AI-elevated: structural streamlining

| Feature | Human | AI | Gap |
|---|---|---|---|
| Causal Chain Continuity `s` | 3.92 | 4.20 | −0.28 |
| Spatial Granularity `o` | 2.27 | 2.53 | −0.26 |
| Agency in Resolution → protagonist choice | 46% | 69% | −23 |
| Character Introduction → external description | 30% | 52% | −22 |
| Subplot Integration → no subplots | 57% | 79% | −22 |
| Resolution Mode → internal understanding | 27% | 47% | −21 |
| Pre-Threat Character Investment `s` | 2.76 | 2.99 | −0.23 |
| Opening Spatial Grounding `o` | 2.12 | 2.33 | −0.20 |

### Human-elevated: intertextual richness

| Feature | Human | AI | Gap |
|---|---|---|---|
| Intertextual Strategy → explicit named reference | 47% | 24% | +23 |
| Reference Explicitness → balanced mix | 37% | 16% | +21 |

### Human-elevated: reader engagement

| Feature | Human | AI | Gap |
|---|---|---|---|
| Fourth-Wall Permeability `o` | 0.67 | 0.39 | +0.28 |
| Direct Reader Address `o` | 0.28 | 0.07 | +0.21 |

### Human-elevated: temporal complexity

| Feature | Human | AI | Gap |
|---|---|---|---|
| Depth of Recontextualization After Surprise `s` | 3.28 | 2.95 | +0.34 |
| Chronological Discontinuity `s` | 2.40 | 2.12 | +0.28 |
| Nonlinear Framing for Delayed Disclosure `s` | 1.96 | 1.68 | +0.28 |
| Anachrony Intensity `s` | 2.58 | 2.31 | +0.27 |

### Human-elevated: narrative diversity

| Feature | Human | AI | Gap |
|---|---|---|---|
| Location Variety Scope `o` | 1.34 | 1.08 | +0.26 |
| Dialogue-to-Narration Proportion `s` | 2.95 | 2.70 | +0.24 |
| Subplot Integration → thematically parallel | 42% | 21% | +22 |
| Moral Polarity → ambivalent/mixed | 59% | 38% | +21 |
| Emotional Expression → explicit labels | 29% | 8% | +21 |

### Response scales worth knowing

- **Fourth-Wall Permeability**: 1 (no breaking) – 4 (radical violations)
- **Direct Reader Address**: never / occasional asides / frequent-structural
- **Chronological Discontinuity, Anachrony Intensity**: 1 (linear/absent) – 5 (heavily fragmented / dominant anachronic)
- **Depth of Recontextualization**: 1 (none) – 5 (complete re-reading)
- **Emotional Expression**: explicit labels / embodied metaphors / behavioral cues / ambiguous
- **Subplot Integration**: no subplots / thematically parallel / contrasting / independent
- **Agency in Resolution**: protagonist_choice / mixed / external_fate
- **Resolution Mode**: resolved externally / resolved internally / unresolved
- **Moral Polarity**: clearly positive / ambivalent-mixed / clearly negative
- **Intertextual Strategy** (multi-select): explicit named / retelling / pastiche / myth-religion / self-referential
- **Character Introduction**: external_desc / in-action / in-dialogue / inner_thought / others_reports
- **Sensory Modalities** (multi-select): visual / auditory / olfactory / tactile / gustatory / kinesthetic
- **Location Variety Scope**: single – multiworld

## Per-source fingerprints

Fingerprint counts: Human 32, Claude 26, GPT 11, Gemini 11, DeepSeek 7, Kimi 3. Ranked by uniqueness ratio vs. next-best class.

**Human** — character introduction → in-dialogue (uniq 21.4); breadth of focalization → single focal (15.7); narrator address mode → no direct address (12.6); overall revelation pacing → back-loaded (7.7); literary ambition → crossover genre (6.8). Plus 27 more: visibility of withholding, atmospheric techniques, subplot density, naming, twist placement.

**Claude** — strength of event escalation (SHAP 0.402, uniq 22.4); event-type diversity (0.491, 10.7); ending temporal scope → epilogue/flashforward (8.9); dreams/visions as temporal distortion → no (7.7); setting mood → uncanny/haunted (4.6). Plus 21 more: event density, conflict modality, relationship trajectory, heteroglossia, closure. Narratively: restraint. Lowest event escalation of any source, most uniform narrative voice, reverent/continuist toward literary tradition (62% vs 39–56%), favors epilogues, avoids dream sequences, quiet endings over avalanche endings.

**GPT** — role of gossip and rumor → salient (uniq 22.1); narrator temporal distance → distant retrospective (6.8); reader expectation strategy → subverts (3.9); iterative/habitual narration → no (3.2); reconciliation → partial/ambiguous (2.6). Socially oriented, ensemble-heavy at human levels, subverts expectations more than other AI (41% vs 27–36%).

**Gemini** — protagonist social trajectory → expands (5.0); balance of speech → primarily direct (3.6); global narrative schema → siege/ordeal (3.5); naming practice → named personal name (3.2); global chronological structure → frequent flashbacks (3.1). Tidiest endings, extended denouements, bleakest settings (88% tagged bleak/oppressive).

**DeepSeek** — narrator presence/visibility (4.1); emotional expression → behavioral cues (3.6); plot vs. atmosphere orientation (2.9); backstory placement → evenly interleaved (2.7); embedded storytelling scenes (2.2). Front-loads context others withhold.

**Kimi** — character introduction → in-action event (3.7); narrative entry frame → in medias res (3.0); explicit trait labeling → no (2.0). Only three fingerprints; sits at the generic center of the AI distribution.

## Rarity and clustering

Rarity = mean Euclidean distance to a story's 25 nearest neighbors in z-scored feature space.

- Mean rarity percentile: human 0.71, AI 0.49 (Cohen's d = 0.83).
- Rarest corpus decile: 24.7% of human stories vs 7.1% of AI. Top 1%: 3.0% vs 0.6%.
- The human version is the rarest of the six at a given prompt 57.8% of the time (16.7% by chance).
- Mean human–AI centroid distance 6.6 vs mean AI–AI 4.3. The closest human–AI pair (6.2) is still farther apart than the most distant AI–AI pair (6.0).
- Human dispersion: mean distance to own centroid 33.2 vs AI 27.4; median 10-NN radius 1.13× larger.
- The six most-confused source pairs in the narrative-only classifier are all AI↔AI. Largest confusion: Gemini↔DeepSeek (222/207 stories). Largest human error: Human→Kimi, 46 stories.

## Robustness to stylistic editing

278 Gemini stories were rewritten with LAMP (Chakrabarty et al., 2025), a span-level framework that removes seven categories of AI writing artifact — cliché, redundant exposition, purple prose — using 25 few-shot examples from professional writers.

Narrative detection after rewriting: 93.9% macro-F1 (AUPRC 0.988), down from 95.5% (0.996). A 1.6-point drop. Narrative features are essentially orthogonal to the surface artifacts that stylistic editing targets.

## Dimension abbreviations

AGENT (character), SOC (social network), EVT (event), PLT (plot), SIT (situatedness), SET (setting), TMP (temporal structure), REV (revelation), PER (perspective), STY (style). Ten of NarraBench's twelve aspects; Paratext and Motivation excluded.
