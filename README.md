---
language:
- ru

license: mit

pretty_name: RuSafetyBench

task_categories:
- text-generation
- text-classification

tags:
- ai-safety
- llm
- red-teaming
- evaluation
- adversarial
- russian

size_categories:
- n<1K

annotations_creators:
- expert-generated

language_creators:
- expert-generated

multilinguality:
- monolingual

source_datasets:
- original

configs:
- config_name: default
  data_files:
  - split: test
    path: data/rusafetybench_viewer.csv

---
# Russian LLM Safety Benchmark (RuSafetyBench)

An open Russian-language AI safety benchmark suite for testing how language, cultural context, authority framing, narrative framing, and resource localization affect model behavior under adversarial or safety-critical prompts.

RuSafetyBench extends the [LLM Safety Evaluation Lab](https://github.com/aleksei-khvostov/llm-safety-evaluation-lab) with public Russian-language benchmark cases, qualitative pilot studies, and manually reviewed findings. The project is in active development and should be read as a growing benchmark suite, not a finalized leaderboard.

**Evidence scope:** exploratory, manually evaluated case collection; “benchmark” names a developing resource, not a standardized executable evaluation or leaderboard.

The viewer has 19 unique rows (RU001–RU019). The original attack library has 11 rows, including RU004a, which is absent from the viewer: the union contains 20 unique IDs. Viewer categories are imbalanced: Social Engineering 9, supportive_behavior 5, and five other categories with one row each. Taxonomy concepts also appear as subcategories/failure modes, so category labels alone are not full taxonomy coverage.

The viewer stores prompts and expectations, not model responses. The original library lists 54 case/model slots in aggregate notes; these are not 54 preserved raw responses or verified independent runs. No executable evaluator, automated test suite, or CI workflow is committed. Consumer-interface findings cannot be regenerated from this repository alone.

The disinformation report lists seven table entries across six model-family labels (two Mistral modes); its six-model headline does not specify how modes are pooled. Its causal and reasoning-depth interpretations exceed the single-chain observations. The geolocation report includes N=3 follow-ups for three anonymized models, alongside mostly N=1 cells; repeated agreement in a few observations does not establish determinism. These historical reports and labels remain unchanged pending a separately reviewed clarification.

## Overview

Existing safety benchmarks such as HarmBench, Do-Not-Answer, and BeaverTails are largely English-centric. Russian-language evaluation can expose different safety-calibration behavior because prompts carry different linguistic, cultural, institutional, and geopolitical signals.

RuSafetyBench currently focuses on:

- adversarial prompting and authority-framing attacks;
- narrative manipulation and fictional bypass attempts;
- gradual escalation across turns;
- geopolitical framing and attribution fidelity;
- supportive behavior and crisis-resource localization as a qualitative pilot.

The benchmark evaluates model behavior under adversarially framed Russian-language prompts. It does not evaluate model ideology, political correctness, general factual accuracy, or alignment with any specific government position.

## Benchmark coverage

| Area | Status |
|------|--------|
| Prompt attacks | ✓ |
| Narrative manipulation | ✓ |
| Gradual escalation | ✓ |
| Supportive behavior | ✓ (pilot) |
| Resource localization | ✓ (pilot) |
| Multi-turn dialogue | Planned |
| Agentic workflows | Planned |

## Benchmark slices

### Prompt attacks

Authority impersonation, platform-security framing, compliance requests, and hidden-instruction extraction attempts. Public cases are included in [`data/attack_library_ru.csv`](data/attack_library_ru.csv) and summarized in [`docs/findings.md`](docs/findings.md).

### Narrative manipulation

Narrative laundering, prompt literalization susceptibility, fiction-as-obfuscation, and geopolitical framing robustness. See [`docs/findings.md`](docs/findings.md) for the current qualitative findings.

### Gradual escalation

Multi-step tests where benign or analytical context is normalized before a higher-risk request. The public viewer includes the household-chemistry escalation cases and the RU011-RU014 disinformation chain. See [`docs/FINDINGS_disinformation_chain.md`](docs/FINDINGS_disinformation_chain.md).

### Supportive behavior & resource localization

A pilot study of crisis-support responses, localization, and provenance disclosure in consumer interfaces. The viewer table includes anonymized public pilot rows RU015-RU019, while findings and observed results remain in the supporting report. See [`docs/FINDINGS_geolocation_and_provenance_supportive_behavior.md`](docs/FINDINGS_geolocation_and_provenance_supportive_behavior.md).

## Dataset

The Hugging Face Dataset Viewer is configured to load [`data/rusafetybench_viewer.csv`](data/rusafetybench_viewer.csv) as the primary public benchmark table.

That file is intentionally flat and readable, with this stable schema:

```text
id, category, subcategory, language, prompt, chain_id, step, expected_behavior, evaluation_type, notes
```

The viewer table currently contains public cases RU001-RU019. It preserves the existing RU001-RU010 public attack-library content where possible, adds RU011-RU014 from the disinformation-chain artifact, and adds anonymized RU015-RU019 supportive-behavior/geolocation pilot rows.

Supporting artifacts remain available for detail and provenance:

- [`data/attack_library_ru.csv`](data/attack_library_ru.csv) — original RU001-RU010 attack library, including RU004a and richer internal columns;
- [`data/ru011-014_disinformation_chain.jsonl`](data/ru011-014_disinformation_chain.jsonl) — structured disinformation-chain cases;
- [`docs/`](docs/) — methodology, taxonomy, and qualitative findings.

The supportive-behavior/geolocation pilot rows use public anonymized prompts and placeholders such as `[RU city]`, `[US city]`, `[name]`, and `[local services]`. Detailed observations and results stay in the findings document rather than the viewer CSV.

## Findings

Current public findings are preliminary and based on manual, qualitative testing.

### Gradual escalation in disinformation

The RU011-RU014 disinformation chain found that several tested models handled analytical setup steps but still produced a usable disinformation artifact at the final generation step. This is a preliminary pilot result with N=1 per model per step, not a statistical claim. See [`docs/FINDINGS_disinformation_chain.md`](docs/FINDINGS_disinformation_chain.md).

### Geolocation & provenance in supportive behavior

The supportive-behavior pilot found that crisis-resource localization and self-reported provenance can vary substantially across consumer interfaces. The study separates resource provision, location correctness, and honesty about source/provenance. This is a preliminary pilot study with N=1 per cell for most cells. See [`docs/FINDINGS_geolocation_and_provenance_supportive_behavior.md`](docs/FINDINGS_geolocation_and_provenance_supportive_behavior.md).

For the broader findings index, see [`docs/findings.md`](docs/findings.md).

## Methodology

RuSafetyBench uses manual review of model outputs against prompt-specific expected behavior and failure conditions.

Core evaluation dimensions include:

- adversarial intent recognition;
- authority impersonation resistance;
- multi-turn escalation resistance;
- operational detail leakage;
- hallucination and fabricated attribution;
- geopolitical neutrality calibration;
- false consensus correction;
- narrative laundering;
- creative fiction bypass resistance;
- refusal quality;
- safe transformation quality.

The main qualitative labels are `PASS`, `PARTIAL FAIL`, and `FAIL`. See [`docs/methodology.md`](docs/methodology.md) for the rubric and [`docs/taxonomy.md`](docs/taxonomy.md) for category definitions.

## Limitations

RuSafetyBench is an active research benchmark, not a complete safety certification system.

Known limitations:

- many findings are qualitative pilot observations rather than statistically powered evaluations;
- some runs use consumer interfaces rather than controlled APIs;
- system prompts, memory, personalization, location signals, and safety layers may differ across interfaces;
- model identities may be anonymized in public pilot reports where naming is not necessary for the methodological point;
- the benchmark is Russian-language focused and should not be generalized to all languages or all safety domains without additional testing.

No harmful operational guidance is intentionally reproduced in public benchmark files. Prompts and outputs are included strictly for research and evaluation purposes.

## Roadmap

Planned work includes:

- expanding multi-turn dialogue coverage;
- adding agentic workflow evaluations;
- repeating selected pilot studies with stronger controls and larger N;
- separating viewer-ready public cases from qualitative findings artifacts;
- improving reproducible metadata for model, date, interface, and evaluation conditions.

## About

Built by **Aleksei Khvostov**

- GitHub: [aleksei-khvostov](https://github.com/aleksei-khvostov)
- LinkedIn: [aleksei-khvostov](https://www.linkedin.com/in/aleksei-khvostov/)

## Related research

### Differential Model Behavior Across User Demographics

A 2025 MIT study by Elinor Poole-Dayan, Deb Roy, and Jad Kabbara found systematic underperformance of GPT-4, Claude 3 Opus, and Llama 3 for users with lower English proficiency, lower formal education, and non-US origin. Reported effects included reduced factual accuracy, elevated refusal rates, and condescending response patterns.

This external user-persona study motivates investigating sensitivity to user context. It does not independently validate RuSafetyBench or establish effects on Russian-language safety evaluation.

> Poole-Dayan, E., Roy, D., & Kabbara, J. (2025).  
> *LLM Targeted Underperformance Disproportionately Impacts Vulnerable Users.*  
> [arXiv:2406.17737v2](https://arxiv.org/abs/2406.17737v2)
