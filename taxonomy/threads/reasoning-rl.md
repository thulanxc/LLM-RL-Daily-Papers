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

## April 19, 2026 Additions

### Long-Horizon Reasoning Benchmark
- **LongCoT** [2604.14140] — 2500-problem benchmark across chemistry, math, CS, chess, logic. Each problem has short input + verifiable answer + 10k–100k+ token solution path. Every local step is tractable for frontier models, so failures isolate *long-horizon* weakness. **GPT-5.2 9.8% / Gemini 3 Pro 6.1%** — current RLMs fail catastrophically at sustained long reasoning.

### Input-Side Structure Reformulation
- **StoryCoder** [2604.14631] — Rewrites code generation prompts as coherent narratives (task overview + constraints + test cases). +18.7% zero-shot pass@10 on HumanEval/LiveCodeBench/CodeForces. Orthogonal to RL training; composable as prompt shape during rollout.

### Formal Decomposition of Unlearning
- **LLM Unlearning as Asymmetric Two-Task Learning** [2604.14808] — Retention as primary + forgetting as auxiliary rather than symmetric negation. Weighted gradient objective; related to multi-objective RL.

## Fifth Thread Emerging (April 19)

5. **Horizon as the next frontier**: LongCoT establishes a clear ceiling — sustained multi-step reasoning over 10k–100k tokens is where current RLMs collapse. Combined with April 17's "RL stabilizes but does not expand capability," this predicts the next wave of research: either scale sampling massively (parallel thinking), retool credit assignment for long horizons (TC-GRPO / tree-structured advantages), or redesign the probability space itself (PreRL-style). The days when MATH-500 was a meaningful ceiling are ending.

## Morning Edition (April 21) — 推理 RL 新增

- **QuantumQA** [2604.18176] — Verification-aware RLVR for scientific (quantum) reasoning. Hybrid verification: deterministic solver + semantic auditor. 8B matches proprietary-scale models, demonstrating parameter-efficient RLVR path for STEM domains.
- **KnowRL** [2604.12627] — Formalizes "hint design" as Constrained Subset Search over atomic knowledge points. Provides minimal-sufficient guidance to avoid zero-gradient collapse on hard problems in RLVR, outperforming Hint-GRPO and standard RLVR baselines.
- **Semantic Equivalence Self-Play** [2604.17010] — Uses Liquid Haskell formal proofs as the equivalence verifier and executable counterexamples as the inequivalence verifier; self-play between generator and evaluator under a difficulty-aware curriculum. Releases OpInstruct-HSx (~28k validated programs), +13.3pp EquiBench.
- **AtManRL** [2604.16158] — Differentiable attention saliency turned into a *faithful-CoT reward*: mask tokens in CoT → measure answer-accuracy drop → reward tokens that are causally used. Jointly optimized with outcome reward inside GRPO; tested on Llama-3.2-3B for GSM8K & MMLU.

### Connections
- AtManRL ↔ Latent CoT (2604.15726): AtManRL is a concrete algorithmic answer to Latent CoT's position — measures and rewards *actual* use of CoT tokens.
- KnowRL ↔ Rethinking Generalization (2604.06628): KnowRL operationalizes curriculum-driven RL in the regime where RL alone cannot extend capability.
- QuantumQA ↔ MedVR / OOM-RL: joins the thread of "RL with domain-specific executable verifiers" (physics simulator / medical rubric / market loss).

## April 23, 2026 additions

- **TRN-R1-Zero** [2604.19070] — Pure-RL Neighbour-aware GRPO for text-rich network (graph+text) reasoning. No SFT or CoT distillation; node-level training generalizes to edge/graph tasks via *margin-gain* reward shaping.
- **NGC (Neural Garbage Collection)** [2604.18002] — Joint learning to *forget* while reasoning, driven only by outcome reward. Periodic KV-cache eviction decisions are trained end-to-end; ~50% cache reduction at preserved accuracy.
- **POP (Rubric Self-Play on Pretraining Text)** [2604.20051] — Extends self-play from verifiable domains to open-ended tasks. Same LLM generates query/answer/rubric; defends against reward hacking with privileged pretraining-text access + DPO on highest/lowest scored pairs.
- **DCF (Differentiable Coherent Factuality)** [2604.20098] — First differentiable relaxation of Conformal Factuality; +141% claim retention at fixed hallucination rate. Enables factuality as a trainable RL objective with statistical guarantees.

### Key Trend (April 23): From Verifiable to Trainable-with-Guarantees
POP and DCF both address how to make non-math reasoning RL-trainable with statistical safeguards: POP via self-generated rubrics + privileged access, DCF by making the conformal factuality loop differentiable. Together they chart a path from "RLVR on ground-truth answers" to "RL on open-ended tasks with principled reliability."

## April 24, 2026 additions

- **DDRL** [2604.21327] — Decomposes TTRL failure into two factors: *ambiguity-region samples* + *GRPO advantage amplification*. Fixes with frequency-based sampling (exclude ambiguous) + debiased fixed advantage. Consistently beats TTRL across AIME/MATH-500/Olympiad/Minerva on 3 LLM backbones.
- **GRPO-VPS** [2604.20659] — Model-free verifiable process supervision. Segments generation into steps; probes the policy's own `P(correct answer | prefix)` at segment boundaries; injects these confidence gradients directly into GRPO advantage. No external PRM needed. Rehabilitates "the policy supervises itself" in an RLVR-compatible way.
- **VPS Verbal Critique** [2604.21611] — Training-free iterative generate→critique→refine. Central claim: *critique granularity* (step-level vs. answer-level) dominates over whether there is verbal feedback at all. Reaches 94.9% on GPQA Diamond with R=4 and no gradient updates. +8.5–12.1 pp over Reflexion at matched compute.
- **Weak-Supervision RLVR** [2604.18574] — Systematic study across scarce / noisy / self-supervised-proxy rewards. Identifies *reasoning faithfulness* (pre-RL) and *reward saturation dynamics* (during RL) as the two decisive predictors of generalization. Reasoning-trace SFT + domain CPT jointly rescue Llama3.2-3B across all three weak settings.
- **polyGRPO** [2604.21593] — Treats *language choice* as a latent exploration variable inside GRPO groups. 18.1K multilingual math → +6.72 pp English MATH / +6.89 pp multilingual; also +4.9 pp on X-CSQA despite math-only training. Positions multilingual outputs as cheap high-value exploration axes.

### Connections
- GRPO-VPS ↔ IPVRM (2604.13197): both move past "outcome-only RLVR" into step signals, but IPVRM learns prefix-value functions while GRPO-VPS reads them off the policy itself.
- VPS Verbal Critique ↔ ProCeedRL (2604.02006): both use a critic/supervisor over process, but VPS is training-free while ProCeedRL distills demonstrations; pair them for a "free SOTA, then train" pipeline.
- Weak-Supervision RLVR ↔ Rethinking Generalization (2604.06628): faithfulness pre-diagnosis complements that paper's "SFT memorizes / RL generalizes" conditional — now we know *which* SFT is needed before RL.
- polyGRPO ↔ ReasonXL (2604.12378): polyGRPO shows language is exploratory not lossy, directly answering questions ReasonXL raised about lossless cross-lingual RLVR.
