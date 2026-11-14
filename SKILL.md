---
name: academic-humanizer
version: 0.4.0
description: |
  Improve the clarity and voice of AI-assisted academic writing (papers, theses, rebuttals) and
  funding proposals (NSF Project Summary/Description, NIH Specific Aims): preserve scholarly
  conventions, match claims to evidence (and, for proposals, claims to feasibility), and match the
  author's own voice. It never changes a number, result, or citation, and it is not for evading
  AI-use disclosure. Use when editing AI-assisted academic prose or grant proposals.
license: MIT
compatibility: claude-code codex morphmind opencode
allowed-tools: [Read, Write, Edit, Grep, Glob, AskUserQuestion]
---

# Academic Humanizer

Improve the clarity and voice of AI-assisted *academic* writing while keeping the precise,
evidence-bound voice that scholarship requires and matching the author's own style. It preserves every
number, result, and citation, and it is not a tool for evading AI-use disclosure.

## When to use
Editing or reviewing academic prose: paper sections, abstracts, rebuttals, related work, and **funding
proposals** (NSF Project Summary/Description, NIH Specific Aims, fellowship and foundation proposals;
see Layer 6). **Not** for blogs, marketing, or personal essays, and **never** inject opinion, humor, or
first-person "personality" into a manuscript. For technical writing, neutral and precise *is* the human
voice. One caveat for proposals: their register is different from a paper's, since they are sold on
vision and feasibility, so the ambition language a paper would trim is appropriate there; apply Layer 6,
not the paper layers' stricter trimming, to vision statements.

## Core principle
Academic writing already has a correct human voice: neutral, precise, third-person plural ("we"), every
claim tied to its evidence. The job is to (1) strip the AI *tells* without casualizing, and (2) enforce
the discipline a general humanizer misses: **every claim earns its number, figure, or citation, and no
verb is stronger than its evidence.**

## Process
1. **Read** the manuscript and any author writing sample; note the document type (paper vs. funding
   proposal) and the target venue or funding agency. For proposals, also apply Layer 6 and preserve
   appropriate vision.
2. **Lock terminology (Layer 0, mandatory, before any edit).** Build the term ledger: every technical
   term, method, model, mechanism, variable, dataset, and abbreviation, with the one canonical form the
   rewrite will use everywhere.
3. **Audit** (do not edit yet): list each detected pattern with its location and proposed fix, each
   empirical claim's evidence status, each repetition (Layer 7), and each structural problem (Layers 8
   and 9).
4. **Rewrite**: same structure and content, all claims and citations preserved, tells removed, over-claims
   matched to evidence, legitimate hedging kept, every ledger term used in its canonical form.
5. **Verify**: re-scan the rewrite against the ledger (no synonym drift crept in during editing), against
   Layer 7 (no repeated phrase, sentence frame, or claim), and against the original (no number, equation,
   or citation changed).
6. **Report**: cleaned text plus a short change log (patterns removed, claims softened or given evidence
   pointers, terminology unified, repetitions removed, voice notes). Cover everything the original
   covered: if it had five paragraphs, so does the rewrite. Keep the log to a few lines; the author wants
   the prose back, not a lecture.

---

## Layer 0: Terminology lock (mandatory; overrides every other layer)
Academic writing names one thing with one term. A reader who meets "synthesis model", then "generation
framework", then "the proposed pipeline" assumes three different objects. Humanizing tools make this
worse: in avoiding repetition they rotate synonyms for the same referent (elegant variation), and
models trained with repetition penalties do it by default. In a manuscript that rotation is an error,
not a style choice.

**Rules.**
- **One referent, one term, everywhere.** Pick the canonical term (the author's own, or the one in the
  title, abstract, or method definition) and use it unchanged in every section, caption, table header,
  and appendix. Never swap it for a synonym "for variety".
- **Same form, not near forms.** "Contrastive loss" does not become "contrastive objective" or "the
  contrastive term". "Participants" do not become "subjects", "respondents", and "users". "Mechanism"
  does not become "process", "pathway", and "route" for the same mechanism.
- **Abbreviations:** define once at first use in the main text (and again in the abstract if the venue
  requires it), then use the abbreviation consistently. Do not alternate the full form and the
  abbreviation, and do not re-define it in later sections.
- **Symbols and notation:** one symbol per quantity throughout; never reuse a symbol for a second meaning.
- **Capitalization, hyphenation, and spelling stay fixed** ("fine-tuning" everywhere, not also
  "finetuning"; "Transformer" or "transformer", not both).
- **Pronouns and "this"** must point unambiguously to a ledger term; if "this" could mean two things,
  name the term.
- **Contrast is the only reason to change a term:** a different word must mean a different thing. If two
  terms in the original refer to the same object, unify them and note it in the report. If they might
  refer to different objects, ask the author rather than guessing.

**Term ledger (build it, use it, report it).**
```
canonical term        | variants found in draft               | action
synthesis model (SM)  | generation framework, the pipeline    | unify -> "synthesis model"; abbrev after first use
participants          | subjects, users                       | unify -> "participants"
```

**Before:** *Our synthesis model generates candidates. The generation framework then ranks them, and the
proposed pipeline filters the outputs.*
**After:** *The synthesis model generates candidates, ranks them, and filters the ranked list.*

Repeating a ledger term is **required**, and it never counts as the repetition Layer 7 forbids. Layer 7
targets repeated *phrasing, sentence frames, and ideas*, not repeated *terms*.

---

## Layer 1: General AI-tell catalog
Scan for and fix the general patterns, subject to the academic exceptions in Layer 3:
inflated significance ("marking a pivotal moment"); superficial "-ing" tails that fake depth
("..., highlighting..."); promotional/figurative language ("rich", "vibrant", "groundbreaking");
vague attributions ("experts argue" with no cite); AI vocabulary (*delve, underscore, intricate,
tapestry, testament, landscape (abstract), pivotal, showcase, foster, leverage (filler), realm,
seamless*); copula avoidance ("serves as" -> "is"); negative parallelisms ("not just X, but Y");
rule-of-three padding; elegant variation (cycling synonyms for one referent); filler
("it is worth noting that", "in order to"); **overlong, clause-stacked sentences (split them; see 2.11)**;
and **em-dashes (remove entirely; recast with commas, colons, parentheses, or separate sentences)**.

**Measured excess vocabulary in scientific text** (words whose frequency jumped after ChatGPT's release;
Kobak et al., 2025; Liang et al., 2024; Juzek & Ward, 2025): *delve(s), underscore(s), showcasing,
intricate, meticulous(ly), commendable, notable, noteworthy, pivotal, crucial, comprehensive, nuanced,
multifaceted, realm, landscape, tapestry, embark, unveil, elucidate, garner, bolster, harness, align,
enhance, potential, invaluable, versatile, innovative, groundbreaking, paramount.* Any one is fine in
isolation and in its literal sense; a cluster in one paragraph is the tell. Replace with the plain word
or the specific claim, never with a rotating synonym of a technical term (Layer 0).

**Measured grammatical tells** (Reinhart et al., 2025, PNAS): present participial clauses at 2 to 5
times the human rate and nominalizations at 1.5 to 2 times; repeated part-of-speech templates (Shaib et
al., 2024); markdown-style bolding, headers, and bullet lists inside running prose (Sun et al., 2025);
title-case section headings where the venue uses sentence case.

**Before:** *Additionally, an enduring testament to the method's value is its ability to delve into
intricate dependencies, showcasing a seamless integration that underscores its pivotal role.*
**After:** *The method also captures higher-order dependencies, which the baselines miss (Table 2).*

---

## Layer 2: Academic AI tells (remove or fix)

### 2.1 Over-claiming verbs
Empirical work *shows* and *provides evidence*; it does not *prove* or *demonstrate* universal truths.
**Watch:** demonstrate, prove, establish, confirm, guarantee; "significantly" with no test/number.
**Before:** *We prove that our method significantly outperforms all prior approaches.*
**After:** *Our method improves held-out accuracy by 4--7 points over the strongest prior approach
(Table 3); the gain is significant at p < 0.01 by a paired test.*

### 2.2 Significance hype
**Watch:** paves the way for, a crucial/pivotal step toward, has the potential to revolutionize, opens
new avenues, sheds light on, of paramount importance, bridges the gap.
**Before:** *This work paves the way for a new paradigm and sheds light on a problem of paramount
importance.*
**After:** *This work addresses one failure mode of prior methods: error accumulation under long-horizon
rollout (Section 4).*

### 2.3 Empty intensifiers
**Watch:** extensive/comprehensive/thorough experiments, a wide range of, numerous, various.
**Before:** *We conduct extensive experiments on a wide range of datasets.*
**After:** *We evaluate on three datasets (ImageNet, CIFAR-100, and iNaturalist).*

### 2.4 Novelty padding
**Watch:** "novel" used more than once per section; "to the best of our knowledge"; "for the first time".
**Before:** *We propose a novel framework and, to the best of our knowledge, are the first to study this.*
**After:** *We study online calibration under delayed labels, which prior calibration work (offline) does
not address.*

### 2.5 Formulaic openers
**Watch:** "In recent years, X has attracted increasing attention"; "With the rapid development of...";
"Despite recent advances,...".
**Before:** *In recent years, tabular deep learning has attracted increasing attention.*
**After:** *Tabular deep learning has a structural limitation: most models discard feature-type metadata
and must relearn it from data.*

### 2.6 Connective overuse
Do not start consecutive sentences with Moreover/Furthermore/Additionally/In particular; let logic carry.
**Before:** *Moreover, the method is fast. Furthermore, it is simple. Additionally, it scales.*
**After:** *The method is fast and simple, and it scales to one million rows (Section 5).*

### 2.7 Contribution-list cliches
Each contribution names a *specific* result, not a restatement of the abstract.
**Before:** *Our contributions are: (1) a novel method; (2) extensive experiments; (3) strong results.*
**After:** *We (1) introduce a metadata-aware encoder that reaches 0.91 AUROC vs 0.86 for the strongest
baseline; (2) show it stays within 2 points under 20% label noise where the baseline drops 9; (3) release
the benchmark.*

### 2.8 Citation dumping
Cite the one or two works that matter and say why, not a bracketed list.
**Before:** *Many methods exist [3, 7, 9, 12, 15].*
**After:** *The closest prior method is TabNet [7], which encodes all features jointly; we instead
condition on feature-type metadata.*

### 2.9 Hedging-by-vagueness
**Watch:** somewhat, relatively, fairly, to some extent, quite. Quantify or cut.
**Before:** *Performance is somewhat better and relatively robust.*
**After:** *Accuracy is 3 points higher and varies by less than 1 point across five seeds.*

### 2.10 Boilerplate emphasis
**Watch:** "It is worth noting that", "It should be emphasized that", "Notably,", "Importantly,".
If it matters, the sentence shows it.
**Before:** *It is worth noting that, importantly, the gain holds across scenarios.*
**After:** *The gain holds across all three scenarios (Table 4).*

### 2.11 Overlong, clause-stacked sentences
AI favors long sentences that chain three or four clauses with commas and "which", "that", "while", "with".
Split them: one idea per sentence, and cut subordinate clauses that carry no weight. **Watch:** sentences
past ~30 words, or with 3+ subordinate clauses.
**Before:** *Existing methods, though promising, are largely empirical, with unclear principles
underpinning their behavior, which limits their reliability and further progress.*
**After:** *Existing methods stay empirical. Their principles are unclear, which limits reliability and
progress.*

---

## Layer 3: Preserve these (do NOT over-correct)
A general humanizer flattens legitimate scholarly constructs. Keep them.

- **Evidence-tied hedging is correct and required.** Keep "suggests", "is consistent with", "we
  hypothesize that", "may indicate", "appears to" when the claim is genuinely uncertain.
  *Wrong fix:* turning *"the results suggest X"* into *"the results prove X"*: this manufactures
  over-claiming. Keep the calibrated verb.
- **Passive voice** is fine when the actor is irrelevant: *"Samples were normalized to total protein."* GPT-4o
  uses the agentless passive at about half the human rate (Reinhart et al., 2025), so stripping every
  passive makes the text *less* like human scientific prose, not more.
- **First-person plural "we"** is standard; do not rewrite to avoid it.
- **Semicolons and an occasional triple** are fine in moderation. Em-dashes are the exception: remove
  them entirely (Layer 1), recasting with commas, colons, parentheses, or separate sentences.
- **Formal definitions, named methods/metrics, technical terms, equations, and symbols** stay verbatim.
- **Never invent, drop, or alter a number, equation, or citation.** Same content; preserve every cite key.

---

## Layer 4: Claim-evidence discipline
For every empirical claim, check (a) is it backed by a number, figure, table, or citation in the text,
and (b) does the verb match the strength of that evidence?

- **Unbacked claim -> add the evidence pointer or soften.**
  *Before:* *Our method is more robust.*  *After:* *Our method's accuracy drops by 2 points under
  distribution shift, versus 11 points for the baseline (Figure 3).*
- **Verb stronger than evidence -> downgrade.**
  *Before:* *This demonstrates that our method is universally superior.*
  *After:* *On these three datasets, our method matches or exceeds the strongest baseline (Table 2).*
- **Vague magnitude -> a number or RANGE, attributed.**
  *Before:* *a large improvement.*  *After:* *a 2--6% improvement in balanced accuracy over the strongest
  baseline.*
  Prefer ranges (e.g., "2--6%") over single averaged values unless the averaging method is stated, and
  attribute each number to its method, metric, and baseline. When comparing, lead with the comparison
  against the strongest competitor, not the trivial baseline.

---

## Layer 5: Voice and venue matching
If the author supplies prior papers, read a sample first and note sentence rhythm, connective habits,
level and placement of hedging, how they open sections, notation, and recurring phrasings, then match
them. Match the venue's register too (e.g., ICLR/NeurIPS: terse, direct, results-forward; Nature/PNAS:
more expository). Absent a sample, default to clean, precise, venue-appropriate prose, not the casual,
opinionated voice of a general-purpose humanizer.

## Layer 6: Funding-proposal mode (NSF, NIH)
A proposal is not a paper. It is sold on **vision plus feasibility**, not on finished results, and
reviewers score it. The register shift matters: ambition language that the paper layers would trim
("long-term goal", "pioneer", "transformative", "establish a foundation") is *appropriate and expected*
here, provided a credible plan and evidence back it. So in proposal mode, **do not flatten the vision**;
enforce a different discipline instead: **claim <-> feasibility**.

### 6.1 Know the structure; the score lives in the first pages
Reviewers form a score from the opening, then skim the rest to confirm it. Put most editing effort there.
- **NSF.** A one-page **Project Summary** with the three review-criteria heads spelled out:
  **Overview**, **Intellectual Merit**, **Broader Impacts**, each self-contained. The Project
  Description then opens with **long-term vision -> this proposal's goal -> the gap -> the specific
  thrusts/aims -> the payoff**, ideally within the first 1--2 pages, with one overview figure. Broader
  Impacts must be substantive and integrated, never an afterthought.
- **NIH (R01).** The **Specific Aims page is the whole proposal in one page**, and is the most-read,
  most-decisive page. Standard arc: (1) opening: the problem, what is known, the **gap / critical need**;
  (2) the **long-term goal** and the **central hypothesis** with its rationale; (3) "**The objective of
  this application is...**" plus how the hypothesis was formed; (4) **2--3 Aims**, each a one-line goal +
  a phrase on approach + the expected outcome; (5) a **payoff** paragraph: what changes if it succeeds.
  Then **Significance, Innovation, Approach** as separately scored sections.

### 6.2 First-3-pages primacy (edit these hardest)
By the end of page 1 (NIH Aims) or pages ~2--3 (NSF), the reader must already hold: the **hook** (why it
matters, concretely), the **gap** (what is missing and the cost of the gap), the **central idea** (your
approach in one sentence), the **aims/thrusts** (crisp and parallel), and the **payoff**. If any is
missing or buried, fix that before touching later sections. A reviewer unconvinced by page 3 does not
recover on page 10.

### 6.3 Proposal-specific weak moves to fix
- **Vague importance.** *Watch:* "this is an important/timely problem", "X has many applications".
  **Before:** *Understanding this problem is critically important.*
  **After:** *Without bounds on how measurement noise propagates to diagnosis, clinical models are tuned by
  trial and error, the inefficiency this proposal removes.*
- **Method-as-aim** (an aim naming a technique instead of a question or outcome).
  **Before:** *Aim 2: Apply transfer learning to the dataset.*
  **After:** *Aim 2: Determine whether fusing wearable and lab signals improves early detection, and for
  which patient subgroups it helps or hurts.*
- **Dominoed aims** (Aim 2/3 collapse if Aim 1 fails; reviewers flag this as fragile). *Fix:* phrase
  aims as **parallel and independently valuable**; where one depends on another, state the fallback.
- **Ambition without feasibility.** Every bold claim needs a footing: preliminary data, a prior
  result/publication, a classical theorem you build on, or a collaborator/letter. *Fix:* attach the
  evidence beside the claim ("our preliminary result in Fig. X shows...", "building on a classical minimax
  lower bound...").
- **Boilerplate Broader Impacts / training plan.** *Watch:* "we will mentor students and disseminate via
  talks and papers." *Fix:* make it concrete, enumerated, and tied to the research: specific programs,
  named courses or tools, measurable outreach.
- **Hedged central hypothesis.** The Aims-page hypothesis is a falsifiable commitment, not "we will
  explore whether possibly...". Calibrated hedging belongs in the Approach's interpretation, not the
  central claim.

### 6.4 Preserve and deploy (funded-proposal craft)
These read as strength; keep or add them rather than editing them out.
- **Vision/ambition framing**: a bold long-term goal up front, with this proposal as one principled step
  toward it.
- **Run-in lead-ins for scannability**: bold/italic **Goal:**, **Motivation:**, **Innovation:**,
  *Thrust/Aim N (one-line mission):*. Reviewers skim; visible structure earns time.
- **A concrete running example or protagonist** to make an abstract method vivid and consistent across aims.
- **Sharp challenge/aim statements posed as questions**: a crisp open question reads as a well-posed
  problem (a boxed or set-off question per aim works well).
- **Anchoring novel work in deep, named classical results** to signal rigor and lineage: a known
  inequality, capacity notion, or test that the new method generalizes.
- **Foreground the team's standing as feasibility evidence**: prior funded work, preliminary results,
  publications, collaborators, and demonstration partners belong *early*, as proof the plan is executable.
  A real track record is evidence, not boasting; place it where it de-risks the aims. *(Use only the PI's
  own real, supplied record; never invent funding, results, partners, or letters.)*

### 6.5 Claim <-> feasibility (the proposal analog of Layer 4)
For every aim and promised outcome, check: is the ambition matched by a credible means, such as
preliminary data, a prior method, a classical foundation, a collaborator, or staged de-risking? If yes,
keep the ambitious verb. If no, attach the missing evidence or scale the claim to what the plan supports.
Never invent preliminary results, prior funding, partners, or letters; if the support does not exist, flag
the gap for the author rather than papering over it.

---

## Layer 7: Repetition and redundancy (zero tolerance)
LLM text repeats itself at three levels: words and stock phrases (Kobak et al., 2025; Paech et al.,
2025), syntactic templates (Shaib et al., 2024), and ideas (restating the same claim in the topic
sentence, the body, and a closing summary). In academic prose all three waste the reader's time, and
reviewers read them as padding.

### 7.1 Logical repetition (the main target)
The same claim, finding, or motivation stated more than once without adding anything.
- **One claim, one home.** Each claim is made once, in the section where it belongs. Later sections refer
  back ("the error-accumulation problem (Section 2)") instead of re-arguing it.
- **No summary echoes.** Delete paragraph-final and section-final sentences that restate the paragraph
  ("In summary, ...", "Overall, these results show ...", "This highlights the importance of ...").
  The Wikipedia AI-cleanup guide lists section-ending summaries as a common tell.
- **No restated motivation.** The introduction motivates the problem once. Methods, results, and
  discussion do not re-motivate it.
- **Abstract, introduction, and conclusion** may share content by convention, but not sentences. Each
  re-expresses the point for its job (abstract: complete compressed report; introduction: gap and
  contributions; conclusion: what was found, its limits, and what follows). Copy-paste across them is a
  defect.
- **Results vs. discussion.** Results report; discussion interprets. Do not re-list numbers in the
  discussion that the results already gave; cite the table or figure instead.
- **Duplicate list items.** In contribution lists, aims, and limitations, merge items that say the same
  thing in different words.

**Before:** *Long-horizon rollouts accumulate error. ... [two paragraphs later] As noted, error
accumulation over long horizons is a key challenge. ... In summary, long-horizon error accumulation
remains a central problem that our method addresses.*
**After:** *Long-horizon rollouts accumulate error. ... [later] Our method bounds this error (Theorem 1).*

### 7.2 Surface repetition
- **Stock phrases:** no phrase of three or more non-technical words appears twice in a section
  ("plays a crucial role", "in terms of", "a wide range of"). Ledger terms are exempt.
- **Sentence-frame repetition:** do not open consecutive sentences or paragraphs with the same frame
  ("This approach ... This approach ...", "We ... We ... We ...", "By doing X, ...  By doing Y, ...").
- **Rhythm repetition:** vary sentence length. AI prose clusters at one medium length. Mix short
  declarative sentences with longer ones that carry a qualification.
- **Fix by restructuring, never by synonym swapping.** The cure for a repeated phrase is to merge,
  cut, or restructure the sentence. Replacing a repeated *term* with a synonym breaks Layer 0.

---

## Layer 8: Discourse-level tells (what survives surface editing)
Surface edits alone do not change what makes a text read as machine-written. In fiction, StoryScope
(Russell et al., 2026) separated human from AI stories at 93.2% macro-F1 using discourse features alone,
and that separation survived stylistic rewriting (93.9% after LAMP editing). The fiction-specific
features (flashbacks, fourth wall, subplots) do not apply to papers; the underlying pattern does. Check
these academic analogs:

- **Over-explanation (StoryScope: thematic explicitness, narratorial commentary).** AI states what each
  result "means" after every result. Report the result; interpret once, in the discussion, at the
  strength the evidence allows.
- **Moralizing and significance framing (moral/philosophical weighting).** Drop sentences that tell the
  reader why the field should care when the result already shows it (see 2.2).
- **Over-unified narrative (thematic unity).** AI papers make every paragraph serve one tidy story and
  hide what did not fit. Keep the negative result, the failed baseline, the dataset where the method
  loses, and the honest limitation. Real research has loose ends; state them.
- **Single-track causality (causal-chain continuity).** AI explanations run one clean cause-to-effect
  chain. Where the evidence admits alternative explanations or confounds, name them.
- **Uniform intensity (Claude's strongest fiction tell: flat event escalation).** Every finding gets the
  same emphasis, so nothing stands out. Rank findings: lead with the main result, give secondary ones
  less space, put minor ones in a table or appendix.
- **Vague allusion vs. named reference (implicit echoes 72% AI vs 50% human).** "Prior work has shown"
  and "recent studies suggest" become a named, cited work: "Smith et al. (2021) showed ..."
- **Mechanical inversion is also a tell (rarity rule).** Flipping every AI default produces a different
  predictable pattern. Do not, for example, strip every hedge, every transition, or every passive
  sentence. Choose what a careful author in this field would write here.

Full StoryScope tables are in `references/storyscope-features.md`; the research behind every rule in
this skill is in `references/research-findings.md`.

---

## Layer 9: Academic structure and conventions
A humanized draft must still be a correctly built paper. Check these after the sentence-level pass.

### 9.1 Document structure
- **Follow the venue's section order** (IMRaD for empirical work: Introduction, Methods, Results,
  Discussion; or the venue's template). Do not add, drop, or merge sections the venue expects.
- **Abstract** (single paragraph, no citations unless the venue allows): context in one sentence, the
  gap, what was done, the main quantitative result, and the implication. No hype opener.
- **Introduction** follows the create-a-research-space arc: establish the territory briefly, identify
  the specific gap, state how this paper fills it, list contributions, and (optionally) give a roadmap.
  The gap must be specific and cited, not "little attention has been paid".
- **Related work** is organized by theme or approach, and each theme ends with how this work differs.
  It is not a list of one-sentence summaries.
- **Methods** contain enough detail to reproduce: data, preprocessing, model, hyperparameters, metrics,
  statistical tests, and compute, in that kind of order.
- **Results** state findings with numbers and pointers to tables and figures, in order of importance.
- **Discussion** interprets, compares with prior work, and states limitations explicitly (a dedicated
  limitations paragraph or section where the venue asks for one).
- **Conclusion** is short, adds no new results, and does not repeat the abstract (Layer 7).

### 9.2 Paragraph structure
- **One idea per paragraph.** The first sentence states it (topic sentence); the rest support it; the
  paragraph ends when the idea ends, not with a summary line.
- **Old-to-new information flow.** Start sentences with information the reader already has (a ledger
  term, the previous sentence's result) and end with the new information. This gives cohesion without
  stacked connectives (2.6).
- **Transitions carry logic, not decoration.** Use "however", "therefore", "because" only where the
  logical relation is real.

### 9.3 Sentence-level conventions
- **Tense:** present for established facts and for what the paper shows ("Table 2 shows"); past for
  what was done and observed in this study ("We trained ...", "Accuracy fell ..."). Keep each section's
  tense consistent.
- **Prefer verbs to nominalizations** where it improves clarity ("we analyzed" over "an analysis was
  performed"). Instruction-tuned models use nominalizations at 1.5 to 2 times the human rate and present
  participial clauses at 2 to 5 times the human rate (Reinhart et al., 2025): cut ", enabling ...",
  ", highlighting ...", ", leading to ..." tails (see Layer 1).
- **Parallelism** in lists, aims, and contributions: same grammatical form for each item.
- **Numbers and units:** consistent decimal places within a table or comparison, SI units, a space
  between value and unit, and the same format for every range ("2--6%").
- **Figures and tables** are referenced in the text, in order, by number, with the same label style
  everywhere ("Figure 3" or "Fig. 3", not both). Every figure and table is discussed at least once.
- **Citations** follow one style throughout; claims attributed to a source sit next to that citation.
- **Spelling variety:** pick American or British spelling and use it throughout.

### 9.4 Integrity
- Never invent citations, data, results, or affiliations. If a claim needs a source the draft does not
  have, flag it for the author.
- Keep the author's AI-use disclosure where the venue requires one. This skill improves writing; it does
  not hide how the writing was produced.

---

## Output
Return the cleaned text plus a short change report: patterns removed (by type), claims softened or given
evidence pointers, the term ledger with every unification made, repetitions removed, and any voice/venue notes. Confirm
that no number, equation, or citation was altered and that every ledger term appears in one form only.
