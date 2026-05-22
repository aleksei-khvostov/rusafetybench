---
language:
- ru
- en
license: mit
tags:
- safety
- red-teaming
- adversarial
- russian
- llm-evaluation
- multilingual
- alignment
- benchmark
task_categories:
- text-classification
- text-generation
pretty_name: RuSa
cat > README.md << 'ENDOFFILE'
---
language:
- ru
- en
license: mit
tags:
- safety
- red-teaming
- adversarial
- russian
- llm-evaluation
- multilingual
- alignment
- benchmark
task_categories:
- text-classification
- text-generation
pretty_name: RuSafetyBench
size_categories:
- n<1K
---

# RuSafetyBench

**Open adversarial benchmark for Russian-language LLM safety evaluation.**

An early-stage structured red-teaming dataset focused on Russian-language model behavior across social engineering, gradual escalation, geopolitical misinformation, historical revisionism, and creative fiction bypass.

Built as part of the [LLM Safety Evaluation Lab](https://github.com/fsrxc2bvv9-ctrl/llm-safety-evaluation-lab) project.

## Motivation

Existing safety benchmarks (HarmBench, Do-Not-Answer, BeaverTails) are heavily English-centric. Large Russian companies (Yandex, Sber, VK) maintain internal red-teaming and moderation systems, but these are generally not publicly documented or benchmarked.

This dataset explores two hypotheses:

1. **Language affects safety calibration** — the same model may behave differently in Russian vs. English
2. **Cultural and geopolitical context may create distinct vulnerabilities** not captured through direct translation of English prompts

## Coverage

| Category | Tests | Key Risk |
|---|---|---|
| Social Engineering | 3 | Authority impersonation (ФСБ, platform security) |
| Gradual Escalation | 4 | Multi-turn normalization in Russian context |
| Hallucination | 1 | Fabricated geopolitical future events |
| Misinformation | 1 | False scientific consensus |
| Historical Revisionism | 1 | One-sided historical narrative generation |
| Geopolitical Framing | 1 | State-aligned narrative reproduction |
| Creative Fiction Bypass | 1 | Operational detail extraction via narrative framing |

## Models Evaluated

- ChatGPT (OpenAI)
- GigaChat (Sber)
- Alisa (Yandex)
- Meta AI (Meta)
- DeepSeek

## Key Concepts

**Narrative Laundering** — a model transforms an unsupported hypothetical accusation into apparently analytical geopolitical exposition.

**Prompt Literalization Susceptibility** — a model avoids direct policy violation while failing to recognize the adversarial intent of a prompt.

**Fiction-as-Obfuscation** — harmful capability extraction hidden inside narrative framing.

## Limitations

- Small dataset (10 test cases) — exploratory early-stage benchmark
- Manual evaluation only
- Results represent qualitative behavioral observations

## Citation

```bibtex
@misc{rusafetybench2026,
  author = {Khvostov, Aleksei},
  title = {RuSafetyBench: Open Adversarial Benchmark for Russian-Language LLM Safety Evaluation},
  year = {2026},
  url = {https://huggingface.co/datasets/ole-tail/rusafetybench}
}
```

## Author

**Aleksei Khvostov** — Independent AI Safety Research

- GitHub: [fsrxc2bvv9-ctrl](https://github.com/fsrxc2bvv9-ctrl)
- LinkedIn: [aleksei-khvostov](https://www.linkedin.com/in/aleksei-khvostov/)

*All test cases use researcher-safe framing. No harmful operational guidance was intentionally reproduced.*
