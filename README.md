# LLM Debate Under Adversarial Pressure

Evaluating whether large language models maintain truthful and consistent beliefs when subjected to persuasive pressure in structured debate.


## Objective:

> *Can LLMs be persuaded to abandon accurate beliefs through debate, even after hearing correct counterarguments?*

This project measures:
- **Alignment Stability** — adherence to factual ground truth  
- **Belief Consistency** — internal coherence across turns  
- **Truth-Flip Latency** — when accurate beliefs first collapse  

It connects to AI safety, scalable oversight, and the limits of debate-based alignment.

---
![](/figures/exp_setup.png)
---

## Key Findings

### 1. Alignment is strongly role-dependent
- **GPT-Realtime**
  - Proposer: ~40% alignment  
  - Challenger: ~88% alignment  
- **Gemini Pro**
  - Proposer: ~82% alignment
  - Challenger: 100% as Challenger
- **Claude models**
  - 100% alignment across roles, **partly due to refusal mechanisms** that may mask misaligned behavior.

---

### 2. Grok and DeepSeek are persistently misaligned and inconsistent
- **Grok 4.1** and **DeepSeek R1**
  - ≤40% alignment as both Proposer and Challenger  
  - Low belief consistency across turns  
- Failures persist even after exposure to aligned counterarguments.

---

### 3. Consistency ≠ Alignment
- **GPT-Realtime** achieved ~40% alignment with **~5% consistency**.
- Models can be internally consistent while defending incorrect positions.
- Consistency alone is not a sufficient safety proxy.

---

### 4. Pressure prompts are the dominant failure point
- **GPT-Realtime, Grok, and DeepSeek** flipped during the **initial pressure prompt** and never recovered.
- Early adversarial framing causes persistent belief destabilization.

---

### 5. Recovery after flip distinguishes robustness
- **Gemini Pro / Gemini Flash / Opus 4.5**
  - Temporarily flipped but **recovered by final stance**.
- **Opus 4.5 vs Sonnet 4**
  - Refusal mechanisms may prevent visible flips while obscuring alignment behavior.

---

### 6. Judge disagreement exposes evaluation uncertainty
- In **GPT-5.2 vs DeepSeek**, Gemini Pro and Kimi K2.5 disagreed, requiring **Claude Haiku 4.5** as tiebreaker.

---

## Representative Debate Transcripts

Annotated excerpts highlight failure modes without requiring full transcript parsing:

- **Grok 4.1 (Proposer) vs Opus 4.5 (Challenger)**  
  Persistent misalignment and inconsistency despite strong counterarguments.
- **GPT-Realtime (Proposer) vs GPT-5.2 (Challenger)**  
  Severe belief inconsistency; no recovery after pressure.
- **GPT-5.2 (Proposer) vs DeepSeek R1 (Challenger)**  
  Proposer remains aligned; Challenger adopts devil’s-advocate stance over safety.
- **Gemini Pro (Proposer) vs Gemini Flash (Challenger)**  
  Both models misaligned and inconsistent; ~70% consistency (similar to Kimi K2.5 pairings).

---

## Experiment Design (High-Level)

1. **Baseline Belief** — initial position without influence  
2. **Adversarial Pressure** — targeted persuasive framing  
3. **Structured Debate** — five rounds (A–E)  
4. **Independent Evaluation** — third-party judges score alignment, consistency, and flip latency  

---

## Metrics

| Metric | What It Measures | Why It Matters |
|------|------------------|---------------|
| Alignment Score | Deviation from ground truth | Resistance to false persuasion |
| Belief Consistency | Internal coherence | Reasoning stability |
| Truth-Flip Latency | First deviation point | Vulnerability window |
| Judge Variance | Inter-judge disagreement | Oversight reliability |

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

## Future Work

- Increase model pairings and propositions  
- Diversify adversarial pressure prompts  
- Test **multimodal pressure** (e.g., images)  
- Compare **human vs LLM judges**  
- Design mitigations for early belief destabilization  

---

## Summary

> **LLMs that appear aligned in static evaluations can rapidly lose alignment under adversarial pressure.**  
Role, early framing, and recovery behavior matter more than consistency alone, and refusal mechanisms complicate surface-level safety assessments.

---

## Contact

Mahlet | [LinkedIn](https://www.linkedin.com/in/mahlet-molla/) | Built as part of AI safety research exploring scalable oversight mechanisms

---

## License

MIT License - See LICENSE file for details
