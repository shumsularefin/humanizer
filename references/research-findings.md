# Research findings on AI writing patterns, and the rules they imply

This file lists the research behind the academic-humanizer rules: what each study measured, what it found
about how LLM-written text differs from human writing, and which layer of `SKILL.md` turns that finding
into a rule. Figures are as reported by the authors. Check the cited version before quoting a number in
your own work.

Models covered across these studies: GPT-3.5, GPT-4, GPT-4o, GPT-5.4, o1-Pro, Claude 3.5 Sonnet,
Claude Sonnet 4.6, Gemini 3 Flash, Grok, DeepSeek V3.2, Kimi K2.5, Llama 3 and 3.1 (base and
instruction-tuned), InstructGPT.

## Summary table

| # | Study | Corpus / models | Key finding | Rule (layer) |
|---|---|---|---|---|
| 1 | Kobak et al., *Science Advances* 2025 | 15M+ PubMed abstracts, 2010–2024 | Abrupt rise of "excess" style words (*delves, showcasing, underscores, crucial, potential*); at least 13.5% of 2024 abstracts were LLM-processed, up to ~40% in some subcorpora | Excess-vocabulary list (L1) |
| 2 | Liang et al., 2024 ("Monitoring AI-Modified Content at Scale") | Peer reviews, ICLR/NeurIPS/CoRL/EMNLP 2023–24 | 6.5–16.9% of review text substantially LLM-modified; adjectives like *commendable, meticulous, intricate* surged; usage spikes near deadlines | Vocabulary (L1), empty praise (2.3) |
| 3 | Liang et al., 2024 ("Mapping the Increasing Use of LLMs in Scientific Papers") | ~950k papers, arXiv/bioRxiv/Nature, 2020–2024 | Steady growth of LLM-modified content, fastest in computer science | Scope of the problem |
| 4 | Geng & Trotta, 2024 | ~1M arXiv abstracts, 2018–2024 | Shifts in word frequency after ChatGPT; even function words like *is* and *are* decline | Vocabulary and copula avoidance (L1) |
| 5 | Juzek & Ward, COLING 2025 | Scientific abstracts; Llama tests; human study | 21 "focal words" (*delve, intricate, nuanced*...) overrepresented; RLHF/preference tuning is the best-supported (mixed) explanation | Why vocabulary tells exist (L1) |
| 6 | Reinhart et al., *PNAS* 2025 | Parallel human/LLM corpora; Llama 3, GPT-4o | Instruction-tuned models use present participial clauses at 2–5× and nominalizations at 1.5–2× the human rate; GPT-4o uses agentless passive at ~half the human rate; gaps larger after instruction tuning | Cut "-ing" tails and nominalizations (L1, 9.3); keep passives (L3) |
| 7 | Shaib et al., EMNLP 2024 | Instruction-tuned LLM outputs vs human text | LLMs produce repeated part-of-speech "syntactic templates" at higher rates than humans, especially in summaries; templates persist through fine-tuning and RLHF | Sentence-frame repetition (7.2) |
| 8 | Sun et al., ICML 2025 ("Idiosyncrasies in LLMs") | ChatGPT, Claude, Grok, Gemini, DeepSeek | Classifier names the source model at 97.1%; word choice alone gives ~85%; signal survives shuffling, paraphrase, translation; transition and emphasis phrases and markdown are distinctive | Connectives (2.6), emphasis (2.10), markdown in prose (L1) |
| 9 | Chakrabarty, Laban & Wu, CHI 2025 (LAMP) | 1,057 paragraphs (GPT-4, Claude 3.5 Sonnet, Llama 3.1 70B), 8,035 expert edits | Writers agree on seven problems: clichés, unnecessary/redundant exposition, purple prose, poor sentence structure, lack of specificity, awkward word choice, tense inconsistency; the three models did not differ | Redundant exposition (L7), specificity (2.3, L4), tense (9.3), clause stacking (2.11) |
| 10 | Russell, Karpinska & Iyyer, ACL 2025 | 300 non-fiction articles; GPT-4o, Claude 3.5 Sonnet, o1-Pro | Frequent LLM users detect AI text nearly perfectly (majority of 5 experts missed 1 of 300), even after paraphrasing or "humanizer" tools; they use vocabulary plus formulaic structure, originality, and tone | Surface fixes are not enough (L8) |
| 11 | Russell et al., COLM 2026 (StoryScope) | 61,608 stories; Claude Sonnet 4.6, GPT-5.4, Gemini 3 Flash, DeepSeek V3.2, Kimi K2.5 | Discourse features alone separate human from AI at 93.2% F1 and survive stylistic rewriting (93.9%); all models cluster together; AI over-explains themes, over-unifies, runs tidy causal chains, uses vague allusion; Claude's tell is flat intensity | Discourse-level tells, rarity rule (L8) |
| 12 | Padmakumar & He, ICLR 2024 | Essays written solo, with GPT-3, with InstructGPT | Writing with the instruction-tuned model reduces lexical and content diversity across authors | Voice matching (L5), avoid generic defaults |
| 13 | Paech et al., ICLR 2026 (Antislop) | Many open and closed models vs human baselines | Some "slop" patterns appear over 1,000× more often in LLM text than in human text; sentence-level structural patterns are a distinct target | Stock phrases (7.2), negative parallelism (L1) |
| 14 | Wikipedia: Signs of AI writing (WikiProject AI Cleanup) | Field guide from editors, 2023– | Inflated significance ("stands as a testament"), promotional tone, editorial commentary, vague attribution, section-ending summaries, rule of three, em-dash and bold overuse; recommends judging by combinations of signs | L1 catalog, summary echoes (7.1) |

## Consolidated pattern list

Grouped by level. Each item points to the layer that handles it.

**Lexical**
- Excess style words (*delve, underscore, intricate, meticulous, pivotal, crucial, showcase*). L1
- Praise adjectives in evaluation (*commendable, innovative, notable*). L1, 2.3
- Fewer plain copulas ("serves as" for "is"). L1
- Transition and emphasis words at sentence start (*Moreover, Furthermore, Notably, Importantly*). 2.6, 2.10
- Vague quantifiers (*a wide range of, numerous, various*). 2.3, 2.9
- Synonym rotation for one referent (elegant variation), driven by anti-repetition habits. L0

**Grammatical**
- Present participial tails (", highlighting ...", ", enabling ..."). L1, 9.3
- Nominalizations ("an analysis was performed"). 9.3
- Too few agentless passives in model output; do not remove legitimate ones. L3
- Repeated part-of-speech templates and sentence frames. 7.2
- Uniform medium sentence length; long clause-stacked sentences. 2.11, 7.2
- Negative parallelism ("not just X, but Y") and rule-of-three lists. L1

**Discourse and structure**
- Over-explanation: interpreting every result as it appears. L8
- Section-ending summaries and restated claims (logical repetition). 7.1
- Over-unified narrative that hides negative results and loose ends. L8
- Single cause-to-effect explanations without alternatives. L8
- Equal emphasis on every finding. L8
- Vague allusion ("prior work has shown") instead of named citations. L8, 2.8
- Formulaic openers and significance framing. 2.2, 2.5
- Markdown formatting in running prose. L1

**Model-specific notes**
- GPT family: highest measured excess-vocabulary rates in scientific text (Kobak; Liang); low agentless passive (GPT-4o, Reinhart).
- Claude: most distinctive in StoryScope (89.3% attribution F1); restraint, flat intensity, uniform voice; low function-word frequency (Sun et al.).
- Gemini, DeepSeek, Kimi: close to the generic AI center; most confused with each other (StoryScope).
- All instruction-tuned models: larger gaps from human text than base models (Reinhart; Shaib; Padmakumar & He).

## What the research says *not* to do

- **Do not rely on word lists alone.** Discourse-level features survive vocabulary edits (StoryScope; Russell et al., 2025).
- **Do not invert every default.** Removing all passives or all hedges makes the text less like human scientific prose (Reinhart) and creates a new detectable pattern (StoryScope rarity analysis).
- **Do not treat any single sign as proof.** Every word on the lists has legitimate uses (Wikipedia guide; Juzek & Ward).
- **This skill is not a detector-evasion tool.** Supervised classifiers on raw text still reach 99.7–99.9% F1 (StoryScope). The goal is better academic prose, with any required AI-use disclosure kept.

## References

1. Kobak, D., González-Márquez, R., Horvát, E.-Á., & Lause, J. (2025). Delving into LLM-assisted writing in biomedical publications through excess vocabulary. *Science Advances*, 11(27), eadt3813. https://arxiv.org/abs/2406.07016
2. Liang, W., et al. (2024). Monitoring AI-modified content at scale: A case study on the impact of ChatGPT on AI conference peer reviews. *ICML 2024*. https://arxiv.org/abs/2403.07183
3. Liang, W., et al. (2024). Mapping the increasing use of LLMs in scientific papers. *COLM 2024*. https://arxiv.org/abs/2404.01268
4. Geng, M., & Trotta, R. (2024). Is ChatGPT transforming academics' writing style? https://arxiv.org/abs/2404.08627
5. Juzek, T. S., & Ward, Z. B. (2025). Why does ChatGPT "delve" so much? Exploring the sources of lexical overrepresentation in large language models. *COLING 2025*, 6397–6411. https://aclanthology.org/2025.coling-main.426
6. Reinhart, A., et al. (2025). Do LLMs write like humans? Variation in grammatical and rhetorical styles. *PNAS*, 122(8), e2422455122. https://arxiv.org/abs/2410.16107
7. Shaib, C., Elazar, Y., Li, J. J., & Wallace, B. C. (2024). Detection and measurement of syntactic templates in generated text. *EMNLP 2024*, 6416–6431. https://arxiv.org/abs/2407.00211
8. Sun, M., Yin, Y., Xu, Z., Kolter, J. Z., & Liu, Z. (2025). Idiosyncrasies in large language models. *ICML 2025*. https://arxiv.org/abs/2502.12150
9. Chakrabarty, T., Laban, P., & Wu, C.-S. (2025). Can AI writing be salvaged? Mitigating idiosyncrasies and improving human-AI alignment in the writing process through edits. *CHI 2025*. https://arxiv.org/abs/2409.14509
10. Russell, J., Karpinska, M., & Iyyer, M. (2025). People who frequently use ChatGPT for writing tasks are accurate and robust detectors of AI-generated text. *ACL 2025*, 5342–5373. https://arxiv.org/abs/2501.15654
11. Russell, J., Rajendhran, Pham, Iyyer, M., & Wieting, J. (2026). StoryScope: Investigating idiosyncrasies in AI fiction. *COLM 2026*. arXiv:2604.03136. (Details in `storyscope-features.md`.)
12. Padmakumar, V., & He, H. (2024). Does writing with language models reduce content diversity? *ICLR 2024*. https://arxiv.org/abs/2309.05196
13. Paech, S., Roush, A., Goldfeder, J., & Shwartz-Ziv, R. (2026). Antislop: A comprehensive framework for identifying and eliminating repetitive patterns in language models. *ICLR 2026*. https://arxiv.org/abs/2510.15061
14. Wikipedia contributors, WikiProject AI Cleanup. Wikipedia: Signs of AI writing. https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing
