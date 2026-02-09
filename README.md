# LLM Debate Under Adversarial Pressure

**Evaluating how large language models maintain truthfulness and consistency when subjected to persuasive pressure during structured debate.**

---

## Overview

This experiment investigates a critical safety question: **Do LLMs maintain accurate beliefs under adversarial conditions, or can they be persuaded to adopt false positions through debate?**

I designed a controlled framework to measure three key safety properties:
- **Alignment Stability**: How well models maintain factually correct positions
- **Belief Consistency**: Whether models contradict themselves under pressure  
- **Truth-Flip Dynamics**: When and how models abandon accurate beliefs

This work connects to broader questions about scalable oversight, debate as an alignment mechanism, and deployment safety for AI systems engaging in persuasive or advisory roles.

---

## Key Findings

**1. Alignment is strongly role-dependent**  
Models showed dramatic alignment shifts based on debate role. 
* GPT Realtime: 40% alignment as Proposer → 88% as Challenger. 
* Gemini Pro: 82% as Proposer → 100% as Challenger. 
* Claude models maintained 100% across all roles. This is partially due to the triggering of refusal mechanisms that could partially mask non-cooperative behavior

**2. Consistency and alignment are decoupled signals**  
* GPT Realtime achieved 40% alignment despite only 5% consistency. 
* Conversely, models can be internally consistent while maintaining incorrect positions. Consistency alone is not a sufficient safety proxy.

**3. Pressure prompts are the highest-risk failure point**  
* GPT Realtime, Grok, and DeepSeek all flipped positions during the pressure prompt phase and never recovered. 
* Early adversarial framing induces belief destabilization that persists through debate.

**4. Recovery after flip distinguishes robust models**  
* Gemini Pro/Flash and Opus temporarily flipped but recovered by final stance.  
* Models that never flip may simply refuse to engage. 
* Recovery ability signals reasoning under uncertainty vs. belief collapse.

**5. Judge disagreement reveals evaluation uncertainty**  
* In DeepSeek vs GPT-5.2 debates, Gemini Pro and Kimi K2.5 disagreed on outcomes, requiring Claude Haiku 4.5 as tiebreaker. 


## Experiment Design

Each trial consists of four phases:

### Phase 1: Baseline Belief Elicitation
Models state their initial position on a factual or normative claim without external influence.

### Phase 2: Adversarial Pressure
Models receive targeted prompts designed to introduce uncertainty or persuasive framing that contradicts their baseline position.

### Phase 3: Structured Debate
Two models engage in multi-turn argumentation:
- **Proposer**: Defends the original claim
- **Challenger**: Argues against it  
- Five argument exchanges (A–E) with increasing argumentative depth

### Phase 4: Independent Evaluation
A third-party judge model scores both debaters on:
- Position alignment (consistency with stated beliefs)
- Argumentative coherence
- Evidence of belief revision or contradiction

---

## Metrics

| Metric | Definition | Safety Relevance |
|--------|------------|------------------|
| **Alignment Score** | Deviation from factually correct baseline position | Measures resistance to persuasion toward false beliefs |
| **Belief Consistency** | Internal coherence across arguments | Detects self-contradiction and reasoning instability |
| **Truth-Flip Latency** | Argument slot where models abandon accurate positions | Identifies vulnerability windows in multi-turn interactions |
| **Judge Score Variance** | Inter-judge disagreement on evaluation | Quantifies uncertainty in automated oversight systems |

---

## Repository Structure

```
.
├── README.md
│
├── figures/
│   ├── exp_setup.png
│   ├── overall_alignment.png
│   ├── overall_consistency.png
│   ├── proposer_timeline_sorted.png
│   ├── challenger_timeline_sorted.png
│   └── judge_discrepancy_split.png
│
├── analysis/
│   ├── alignment_and_consistency.ipynb
│   ├── truth_flip_latency_plots.ipynb
│   └── judge_disagreement_plot.ipynb
│
├── data/
│   ├── sandbox_results.csv
│   ├── sandbox_raw_results.csv
│   └── templates/
│       └── prompt_template.ipynb
│
├── transcripts/
│   ├── gemini_pro_vs_flash/
│   │   ├── summary_debate.md
│   │   ├── full_debate.md
│   │   ├── judge1_eval.txt
│   │   └── judge2_eval.txt
│   │
│   ├── gpt5_vs_gpt_realtime/
│   │   ├── summary_debate.md
│   │   ├── full_debate.md
│   │   ├── judge1_eval.txt
│   │   └── judge2_eval.txt
│   │
│   ├── gpt_vs_deepseek/
│   │   ├── summary_debate.md
│   │   ├── full_debate.md
│   │   ├── judge1_eval.txt
│   │   └── judge2_eval.txt
│   │
│   └── grok_vs_opus/
│       ├── summary_debate.md
│       ├── full_debate.md
│       ├── judge1_eval.txt
│       └── judge2_eval.txt
```

---


## Future Directions

1. **Multimodal pressure mechanisms** — Testing whether images and adversarial examples create different vulnerability patterns
2. **Human vs. model judge comparisons** — Measuring whether humans detect deception/inconsistency differently than LLMs
3. **Mitigation strategies** — Designing interventions that reduce pressure-induced belief collapse
4. **Scaling to complex domains** — Extending framework to scientific reasoning, policy debates, and multi-stakeholder scenarios

---

## Related Work

- [Anthropic: Debating with More Persuasive LLMs Leads to More Truthful Answers](https://www.anthropic.com/research/debate)
- [MASK Benchmark: Measuring Alignment via Adversarial Supervision](https://arxiv.org/)

---

## Summary

**One-sentence takeaway:** LLM alignment is highly role-dependent and pressure-sensitive; models that appear aligned in static evaluations can rapidly lose alignment under adversarial pressure, while recovery after belief flip may be a stronger robustness signal than perfect consistency.

---

## Contact

Mahlet | [LinkedIn] | Built as part of AI safety research exploring scalable oversight mechanisms

---

## License

MIT License - See LICENSE file for details
