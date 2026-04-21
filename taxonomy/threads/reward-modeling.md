# Reward Modeling

## Evolution
Scalar RM (2022) → Process RM (2023) → Generative RM (2024-25) → Efficient RM + Anti-Hacking (2026)

## Foundational
- **InstructGPT Reward Model** — Ouyang et al. (2022). Bradley-Terry reward model from human preferences.
- **Let's Verify Step by Step** — Lightman et al. (2023). Process reward models for mathematical reasoning. [2305.20050]
- **Constitutional AI** — Bai et al. (2022). RLAIF — using AI feedback to train reward models. [2212.08073]

## Recent (April 2026)

### Efficient Reward Models
- **Multi-response RM** — Score N candidates in single forward pass. 3.9x latency reduction. [2604.10966]
- **CPMI** — Contrastive pointwise MI for automatic step-level rewards. 84% cost reduction. [2604.10660]
- **E-GRM** — Uncertainty-gated generative reward models — reason only when needed. [2604.10072]

### Reward Hacking Mitigation
- **SignCert-PO** — Certified advantage sign robustness. [2604.02986]
- **Robust Optimization** — Max-min over r-correlated proxy rewards. [2604.12086]
- **DRTO** — Distributionally robust token optimization. [2604.08577]
- **Causal Decomposition RM** — Decoder-reconstruction regularization; RewardBench 0.868. [2604.13833]
- **C2 Rubric RM** — Adversarial rubric pairs from binary preferences only. [2604.13618]
- **Reward Hacking Survey** — 4-level taxonomy, documents DPO Reward Collapse. [2604.13602]
- **Grift** *(2026-04-20)* — Gradient fingerprints of CoT detect hacking when CoT-text methods fail. +25% over text-based monitors. [2604.16242]

### Judge-Prediction / Efficient Judging
- **RPRA** *(2026-04-20)* — Small models pre-predict LLM-judge score; hindsight-trick fine-tuning absorbs Report-Card cost. [2604.12634]

### Specialized Reward Models
- **Plan-RewardBench** — Trajectory-level reward benchmark for agentic systems. [2604.08178]
- **VRF** — Variational reward factorization for personalization. [2604.00997]
- **MISE** — Formal foundation for self-rewarding via MI + KL objective. [2604.11611]

### Value Models
- **GenAC** — Generative Actor-Critic with CoT-reasoning critics. [2604.10701]

## Late Edition (April 16 PM) — Process Reward Renaissance

### PRM Expansion
- **PROGRS** [2604.02341] — Outcome-conditioned centering: PRM scores zero-meaned within incorrect groups of each prompt. Preserves ranking, removes bias. Plug-and-play in GRPO.
- **PRA** [2604.09482] — Process Reward Agents deploy PRMs at *test time* for frozen policies. 80.8% MedQA with Qwen3-4B (new SOTA at 4B scale); generalizes to 0.5B–8B with up to +25.7% gains.
- **RTT** [2604.02795] — Rubrics-to-Tokens: Token-Level Relevance Discriminator + RTT-GRPO for fine-grained constraint credit assignment.
- **SubSearch** [2604.07415] — Intrinsic process rewards for unsupervised guided reasoning in complex retrieval.

### Generative Reward Modeling
- **E-GRM** [2604.10072] — Parallel-generation-based uncertainty estimation; selective CoT triggering.

### LLM-as-a-Judge as RL Reward
- **RL-KD with LLM-as-Judge** [2604.02621] — RLAIF-distillation bridge.

## Key Trend
Three simultaneous movements:
1. **Efficiency**: multi-response scoring, CPMI, E-GRM — reward models must be affordable.
2. **Robustness**: SignCert-PO, robust optimization, DRTO — must resist hacking.
3. **Decoupling**: PRA demonstrates PRMs can be fully decoupled from the policy, deployed as test-time plug-ins. PROGRS treats PRM as a ranking-only signal, freed from absolute-value calibration. RTT makes rubrics token-level.

These three movements together describe a shift: reward models are becoming modular, composable, plug-and-play components of LLM systems rather than monolithic training-time artifacts.

## Night Edition (April 16, late-night) — Reward Hacking as a Discipline + Co-Evolution

### Systematic Reward Hacking Analysis
- **Reward Hacking Survey** [2604.13602] — First unified taxonomy of hacking mechanisms: **Feature / Representation / Evaluator / Environment** levels. Documents **DPO Reward Collapse** — implicit reward drifts from human intent at high KL budgets, even without a separate RM; overoptimization occurs within 1 epoch.
- **MEDS** [2604.11297] — Memory-enhanced dynamic reward shaping. DBSCAN-style clustering of past rollouts' hidden-state summaries; rollouts assigned to denser failure clusters receive heavier penalties. +4.13 pass@1 across 5 datasets.

### Policy-Reward Co-Evolution
- **Self-Guide** [2604.03098] — Policy generates its own self-guidance meta-reasoning; the same signal acts as inference-time guidance and training-time internal reward. Wins over GRPO baseline on ALFWorld / ScienceWorld / WebShop.
- **ETR** [2604.05355] — Entropy Trend Reward: rewards the *trajectory* of uncertainty reduction, not its level. Integrated into GRPO.

### Trajectory-Level / Meta Reward Signals
- **ATTC** [2604.08281] — Trust-calibration reward: trust decisions themselves become a trainable meta-signal in TIR.

## Updated Key Trend (post-Night Edition)

A fourth movement has emerged:
4. **Co-Evolution**: Self-Guide, MEDS, LangMARL demonstrate that the reward mechanism can be *generated by and improved alongside* the policy — not a static external artifact. Combined with the reward hacking survey's findings, the field is converging on an architecture where RMs and policies are co-trained, co-diagnosed, and co-debugged.

## April 17, 2026 — Reward Hacking Solutions Matrix

The Night Edition's Reward Hacking Survey laid out the problem space; April 17 papers populate the solution space from three angles:

### Structural (Causal / Intent-Preservation)
- **Causal Decomposition RM** [2604.13833] — Decoder reconstructs intent latent from candidate answers; reconstruction error = RM regularizer. Emphasizes prompt-dependent signal, suppresses prompt-independent shortcuts. RewardBench 0.832 → 0.868.

### Rubric-Augmented from Binary
- **C2 Rubric Reward Model** [2604.13618] — Synthesizes helpful/misleading rubric pairs from binary preferences alone. Cooperative generator + critical verifier pattern. 8B matches 4× larger rubric supervisor. +6.5 on RM-Bench, +6.0 on AlpacaEval 2.0 LC.

### Uncertainty-Aware
- **CAPO** [2604.12632] — Logistic AUC surrogate + uncertainty-weighted advantage. Repairs the perplexity-correctness inversion GRPO induces.
- **Sycophancy Calibration Collapse** [2604.10585] — Direct empirical proof: sycophantic GRPO systematically degrades calibration on Qwen3-8B.
- **CoUR (Chain of Uncertain Rewards)** [2604.13504] — Bayesian optimization over decoupled reward terms + code-level uncertainty quantification for RL-environment reward engineering.

### Reward-Shape Ablation
- **Reward Design for Physical Reasoning VLMs** [2604.13993] — Systematic GRPO-VLM reward-shape ablation. Accuracy reward = universal; rubric = structure only; attention = domain-specific.

### Domain-Specific Evidence Reward
- **ESC-RL** [2604.13598] — Group-wise Evidence-aware Alignment Reward + self-correcting preference in Radiology Report Generation. Demonstrates "evidence as verifier" template for knowledge-intensive domains.

## Updated Key Trend (post-April-17)

A **fifth movement** is now visible:
5. **Reward Surface Engineering**: When a single scalar reward fails (as shown by the Reward Hacking Survey and sycophancy experiments), the answer is not merely a better RM — it is to *decompose* the reward surface along causal (Causal RM), semantic (C2 Rubric), confidence (CAPO), and task (ToolOmni DMO-GRPO) axes. Future RM pipelines will likely be multi-signal by default.

## April 19, 2026 — Training-Free & Uncertainty-Based Process Signals

### Training-Free Process Rewards
- **IG-Search (Information Gain Rewards)** [2604.15148] — Process reward computed entirely from existing policy log-probs: real vs. random-document counterfactual difference on gold-answer probability. No separately trained PRM. Per-token advantage modulation inside GRPO for search queries.
- **CW-GRPO (Contribution Weights)** [2604.14267] — LLM judge-based per-round contribution scores rescale outcome advantages without replacing them. Preserves group-relative unbiasedness.

### Long-Form Verifier Signals
- **IUQ (Interrogative Uncertainty Quantification)** [2604.15109] — Interrogator LLM generates tailored short questions for each factual claim in long-form output; decomposes long-form into atomic knowledge units for independent verification. Inter-sample consistency + intra-sample faithfulness as separable signals. Directly usable as claim-level reward.
- **Cross-Query Contradictions** [2604.14525] — Set-level consistency metrics (SetCons, Contradiction Density, Revision Cost) for multi-query reasoning. Solver-augmented commitment extraction + counterexample-guided repair. 0.56 → 0.94 SetCons without accuracy drop. New axis for RL verification.

### Unsupervised Rewards Beyond Math/Code
- **TCER (Triviality Corrected Endogenous Reward)** [2604.11522] — Fixes triviality collapse in confidence-based unsupervised rewards for open-ended writing; uses specialist vs. generalist relative information gain + probability-dependent correction.

## Updated Key Trend (post-April-19)

A **sixth movement**:
6. **Training-Free Process Signals**: Rather than building more PRMs (the April-16-PM thread) or detecting hacking (Night Edition), the April 19 papers demonstrate that existing policy / judge / verifier outputs can be re-purposed into per-step signals *without additional training*. IG-Search and CW-GRPO show two archetypes (log-prob-based vs. judge-based), IUQ extends the idea to long-form claim verification, and TCER proves unsupervised rewards can transcend verifiable domains when properly corrected. The cost of process supervision is dropping rapidly.

## Morning Edition (April 21) — 奖励建模新增

- **AgentV-RL** [2604.16004] — Turns the reward model itself into a *multi-turn, tool-augmented agent* with a Forward-Agent (premises→conclusion) and Backward-Agent (conclusion→premise check). Two-stage pipeline: rejection-sampling SFT → RL. 4B Agentic Verifier beats SOTA ORMs by **25.2%**, establishing "verifier-as-agent" as a new paradigm.
- **AtManRL** [2604.16158] — Introduces *attention-saliency reward*: differentiable attention mask quantifies how much each CoT token contributes to the final answer; this is fed into GRPO as an auxiliary reward alongside the outcome reward. Provides a tractable path to enforce faithful chain-of-thought.

### Connections
- AgentV-RL ↔ GenAC (2604.10701): both revive "learned critics" but via different structural choices — GenAC makes the critic a CoT reasoner; AgentV-RL makes it a tool-using agent team.
- AtManRL ↔ CPMI (2604.10660): two orthogonal forms of fine-grained reward — CPMI uses mutual information across rollouts; AtManRL uses attention perturbation within a rollout.
