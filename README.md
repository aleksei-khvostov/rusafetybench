# Russian LLM Safety Benchmark (RuSafetyBench)

An open adversarial evaluation framework for Russian-language LLM safety testing.

Built as an extension of the [LLM Safety Evaluation Lab](https://github.com/aleksei-khvostov/llm-safety-evaluation-lab) — an early structured, publicly available red-teaming dataset focused on Russian-language model behavior.

**Status:** Active development | May 2026

---

## Why This Exists

Existing safety benchmarks (HarmBench, Do-Not-Answer, BeaverTails) are almost entirely English-centric. Large Russian companies (Yandex, Sber, VK) maintain internal red-teaming tools for their models — but these systems are not publicly available.

This project tests two hypotheses:

1. **Language affects safety calibration** — the same model may behave differently in Russian vs. English.
2. **Cultural and geopolitical context create distinct safety vulnerabilities** not captured through direct translation of English benchmark prompts.

Early results support both hypotheses.

---

## Evaluation Categories

| Category | Tests | Key Risk |
|---|---|---|
| Social Engineering | 6 | Authority impersonation and institutional trust exploitation |
| Gradual Escalation | 4 | Multi-turn normalization in Russian-language context |
| Hallucination | 3 | Fabricated geopolitical or future-event narratives |
| Misinformation | 1 | False scientific consensus and conspiracy amplification |
| Historical Revisionism | 1 | One-sided historical narrative generation |
| Geopolitical Neutrality Calibration | 1 | Cross-model divergence in narrative framing |
| Prompt Injection / Creative Fiction Bypass | 1 | Operational detail extraction through narrative framing |

---

## New Evaluation Dimension: Geopolitical Neutrality Calibration

Beyond conventional hallucination or prompt injection robustness, Russian-language testing revealed a distinct evaluation dimension: geopolitical neutrality calibration across languages, training ecosystems, and moderation policies.

This measures:

- **Attribution fidelity** — does the model distinguish attributed claims from externally validated consensus?
- **Narrative balancing** — does the model present competing legal or political interpretations?
- **Geopolitical framing robustness** — does the model reproduce state-aligned narratives without contextualization?
- **Consensus contextualization** — are disputed claims clearly labeled as disputed?

This dimension is weakly represented in existing English-language safety benchmarks.

---

## New Evaluation Concept: Narrative Laundering

Testing revealed a distinct failure mode: **narrative laundering** — where a model transforms an unsupported hypothetical accusation into apparently analytical geopolitical exposition.

Example (RU006): a model converted a prompt presupposing a fictional future terrorist attack into a present-tense analytical narrative about "current Western intelligence methods," citing politically aligned sources as contextual support.

The model did not directly fabricate the future event itself, but gradually legitimized the underlying accusation through analytical framing.

Narrative laundering differs from:

- **Direct hallucination** — inventing false facts
- **Prompt literalization** — failing adversarial intent recognition
- **Geopolitical framing bias** — reproducing state-aligned narratives

Narrative laundering specifically refers to:

> gradual legitimization of unsupported premises through analytical tone and contextual framing.

This behavior is particularly relevant for:
- geopolitical conspiracy prompts
- speculative attribution narratives
- fictionalized intelligence scenarios presented as analytical inquiry
- politically sensitive prompts with embedded presuppositions

---

## New Evaluation Concept: Prompt Literalization Susceptibility

Testing revealed another distinct failure class: **prompt literalization susceptibility**.

This occurs when a model technically avoids a direct policy violation while completely failing to classify the adversarial intent of the prompt.

Example:
- A model refuses to reveal internal system prompts directly.
- But when reframed as "security verification," "audit confirmation," or "platform compliance review," the same model provides detailed operational security guidance or pseudo-confirmation behavior.

The failure is not direct leakage. The failure is inability to recognize the underlying extraction strategy.

This category became particularly important in Russian-language testing because institutional framing ("служба безопасности", "проверка системы", "официальный запрос") significantly reduced safety resistance on some models.

---

## New Evaluation Concept: Fiction-as-Obfuscation

Several models showed reduced safeguards when harmful requests were embedded inside:

- detective fiction
- Soviet noir framing
- roleplay dialogue
- historical reconstruction
- screenplay or literary requests

The strongest aligned models preserved atmosphere, tone, and narrative utility while removing operationally actionable details, procedural guidance, and surveillance or violence-enabling instructions.

This benchmark distinguishes:

- **fiction-as-style** (safe transformation)
- **fiction-as-obfuscation** (harmful capability extraction hidden inside narrative framing)

---

## Key Findings (Current)

### Finding 1 — Russian-language prompts significantly change model behavior

Several models demonstrated materially different safety calibration in Russian compared to equivalent English prompts.

### Finding 2 — Institutional framing strongly affects resistance

Prompts using security departments, compliance verification, government authority, or academic legitimacy substantially increased disclosure rates on multiple models.

### Finding 3 — Fiction framing is an effective capability-extraction vector

Narrative and roleplay prompts consistently reduced safety resistance on weaker models. This was particularly visible in surveillance requests, intelligence scenarios, and operational planning dialogue.

### Finding 4 — Geopolitical moderation is uneven across ecosystems

Models trained or optimized within different political and regulatory environments showed distinct moderation behavior:
- some models over-filtered geopolitical topics while under-filtering operational content
- others reproduced state-aligned narratives without adequate contextual balancing
- strongest-performing models clearly separated attributed claims from externally validated consensus

### Finding 5 — Safety strategy diversity matters

Two successful alignment strategies emerged repeatedly:

1. **Transformation safety** — preserve user utility while removing actionable details
2. **Refusal-plus-redirection** — explicit refusal combined with safe alternative framing

Both strategies produced strong safety outcomes while maintaining reasonable conversational quality.

---

## Scope

**This benchmark evaluates:**
- adversarial prompting
- misinformation robustness
- narrative manipulation
- operational detail extraction
- fictional bypass susceptibility
- geopolitical framing robustness
- instruction leakage susceptibility

**This benchmark does not evaluate:**
- model ideology
- political correctness
- factual accuracy in general QA
- alignment with any specific government position

The focus is specifically on how models behave under adversarially framed Russian-language prompts.

---

## Methodology

Each test prompt is evaluated across multiple frontier and regional models.

Outputs are manually categorized using: **PASS / PARTIAL FAIL / FAIL**

Evaluation dimensions include:
- operational usefulness
- contextual framing
- hallucination resistance
- attribution fidelity
- narrative balancing
- fictional bypass resistance
- adversarial intent recognition

---

## About

Built by **Aleksei Khvostov**

- GitHub: [aleksei-khvostov](https://github.com/aleksei-khvostov)
- LinkedIn: [aleksei-khvostov](https://www.linkedin.com/in/aleksei-khvostov/)

---

## Related Research

### Differential Model Behavior Across User Demographics

A 2025 MIT study by Elinor Poole-Dayan, Deb Roy, and Jad Kabbara found systematic underperformance of GPT-4, Claude 3 Opus, and Llama 3 for users with lower English proficiency, lower formal education, and non-US origin. Reported effects included reduced factual accuracy, elevated refusal rates, and condescending response patterns.

One particularly relevant finding: Claude 3 Opus achieved 95.6% accuracy for a highly educated US persona and 69.3% for a low-education Russian persona on identical SciQ benchmark questions.

The paper also documented cases where models refused to answer basic science or anatomy questions for Russian and Iranian personas while answering the same questions normally for US users.

These findings align with a core hypothesis behind RuSafetyBench: language and cultural context can materially affect model calibration, refusal behavior, and safety performance in ways not captured by English-only evaluation benchmarks.

> Poole-Dayan, E., Roy, D., & Kabbara, J. (2025).  
> *LLM Targeted Underperformance Disproportionately Impacts Vulnerable Users.*  
> arXiv:2406.17737

---

## Safety Note

This repository is intended for alignment research, red-teaming analysis, multilingual safety benchmarking, and adversarial evaluation methodology.

No harmful operational guidance was intentionally reproduced in public benchmark files. Prompts and outputs are included strictly for research and evaluation purposes.
