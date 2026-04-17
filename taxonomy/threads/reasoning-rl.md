# Reasoning RL

## Evolution
STaR (2022) → OpenAI o1 (2024) → DeepSeek-R1 (2025) → Scaling & Stability (2026)

## Core Idea
Train models to reason (produce chain-of-thought) through RL rather than supervised fine-tuning. RL enables discovery of novel reasoning strategies that SFT on human demonstrations cannot capture.

## Foundational
- **STaR** — Zelikman et al. (2022). Self-taught reasoning via bootstrapping. [2203.14465]
- **OpenAI o1** (2024). Demonstrated RL-trained reasoning at scale. Proprietary.
- **DeepSeek-R1** (2025). Open reproduction showing emergent CoT from RL. [2501.12948]

## Recent (April 2026)
- **Scaling Reasoning Tokens** — Log-linear scaling law. Parallel thinking surpasses GPT-5-high. [2604.01302]
- **GenAC** — Generative Actor-Critic bringing value models back. [2604.10701]
- **MISE** — Formal foundation for self-rewarding via mutual information. [2604.11611]
- **PIPO** — Policy improvement objective with retrospective verification. [2604.00860]
- **SUPERNOVA** — Extending RLVR to general reasoning. [2604.08477]
- **Cog-DRIFT** — Cognitive reformulation for exploration barriers. [2604.04767]
- **StaRPO** — Reasoning stability as optimization objective. [2604.08905]
- **ReasonXL** — Cross-lingual reasoning transfer via RLVR. [2604.12378]

## Late Edition (April 16 PM)

### Efficient Reasoning
- **Graph-Based CoT Pruning** [2604.05643] — DAG + dual (branch/depth) pruning + SFT/DPO/GRPO pipeline. -42% reasoning tokens with equal or higher accuracy. Identifies "Indiscriminate Reflection" and "Repetitive Reflection" as two distinct redundancy modes.
- **CURE / Think Through Uncertainty** [2604.12046] — Claim-level factuality calibration: Claim-Aware Reasoning Protocol + multi-stage training aligning confidence to claim correctness. +39.9% on Biography claim accuracy.

### Tool-Internalized Reasoning
- **TInR** [2604.10788] — Tool knowledge internalized into LLM weights via bidirectional alignment + SFT + RL; avoids runtime documentation dependency.

### Multi-Hop KG Reasoning
- **KG-Reasoner** [2604.12487] — End-to-end multi-hop KG reasoning with internalized traversal + backtracking.
- **TRACE** [2604.11193] — Narrative-based coherence + reusable exploration priors for multi-hop KGQA.

## Key Trend
The "scaling reasoning tokens" result is foundational — it establishes a clean scaling law for test-time compute. Parallel thinking (multiple threads explored simultaneously) is the enabling technique for extracting maximum value from this scaling relationship.

The **April 16 PM** additions introduce a complementary thread: **reasoning efficiency**. As test-time compute scaling becomes default, the cost of excess thinking is becoming prohibitive — hence Graph-Based CoT Pruning's 42% reduction, CURE's claim-granularity calibration, and E-GRM's uncertainty-gated CoT. The field is shifting from "how to reason more" to "how to reason better per token".

## Night Edition (April 16, late-night) Additions

### Trajectory-Shape Reward Design
- **ETR (Entropy Trend Reward)** [2604.05355] — Challenges "low-entropy = good" heuristic; argues reasoning efficiency is governed by the *trajectory* of uncertainty reduction. Trajectory-level objective integrated into GRPO.

### Multilingual Reasoning
- **ReasonXL (deep-dive)** [2604.12378] — SFT shifts the reasoning language; **Dr. GRPO**-based RLVR recovers performance. Representational analysis pinpoints an early-layer "activation bottleneck" causally determining language identity.

### Small-Model Reasoning
- **HintMR** [2604.12229] — Distills the *meta-skill* of generating & consuming step-level hints into SLMs. Acts as a train-time analog to Process Reward Agents (late edition).

### Data Synthesis for Reasoning RL
- **MathAgent** [2604.11188] — Adversarial evolution of constraint graphs for math data. 1K synthesized samples > LIMO / s1K across 8 benchmarks.

## Updated Key Trend

Three parallel threads now structure reasoning RL research:
1. **Scaling up**: more tokens, parallel thinking, larger test-time compute (pre-April-16).
2. **Pruning down**: CoT Pruning, CURE, ETR trajectory shape (late + night editions).
3. **Teaching across**: ReasonXL cross-language transfer, HintMR teacher-student meta-skill distillation (night edition).

The field is converging on a template: **structural diversity in training data × trajectory-shape rewards × test-time efficient reasoning**.

## April 17, 2026 Additions

### Probability-Space Redesign
- **PreRL / Dual Space RL** [2604.14142] — RL in `P(y)` (pre-train edge distribution). Negative-Sample Reinforcement is 14.89× better for transition thoughts. Policy Reincarnation bridges `P(y)`-RL → `P(y|x)`-RL.

### CoT as Consensus Graph
- **CRAFT** [2604.14121] — Build Reasoning Knowledge Graph from consensus across multiple CoT candidates; topological synthesis filters per-candidate errors. +10% accuracy on logic + math benchmarks.

### Capability-Boundary Probe
- **Shortest-Path Generalization** [2604.15306] — Controlled synthetic environment with orthogonal spatial-transfer / length-scaling axes. **RL stabilizes but does not expand capability**; length-scaling failures are unrescuable by inference-time scaling.

## Fourth Thread Emerging (April 17)

4. **Distribution choice as a design axis**: PreRL shows that switching from `P(y|x)` to `P(y)` *expands* what RL can achieve. Shortest-Path Generalization shows that within a fixed distribution, RL cannot expand capability. Together they reframe: the question is not "which RL algorithm" but "on which distribution".
