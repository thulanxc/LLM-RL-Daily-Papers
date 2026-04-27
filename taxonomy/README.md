# LLM RL Research Taxonomy

A living map of research directions in Reinforcement Learning for Large Language Models, showing how ideas connect and evolve.

## Research Direction Map

```
                          LLM Reinforcement Learning
                                    │
                 ┌──────────────────┼──────────────────┐
                 │                  │                   │
          Training Methods    Reward Systems      Applications
                 │                  │                   │
        ┌────────┼────────┐   ┌────┼────┐        ┌────┼────┐
        │        │        │   │         │        │         │
    On-Policy  Off-Policy  Hybrid  Reward    Process  Reasoning  Agentic
        │        │        │   Models   Rewards      │         │
     ┌──┼──┐   ┌─┼─┐    ┌┼┐  │         │      ┌───┼───┐  ┌──┼──┐
     PPO GRPO  DPO KTO  TPO  ORM      PRM    Math  Code  Tools  Multi-
      │   │     │       DDO   │         │     Logic  Gen   Use   Agent
    DAPO SKPO SimPO     RM  GenRM     CPMI     │         │
      │  TEPO  IPO           MISE      │    CoT/R1   SEARL
    SPPO StaRPO              VRF            Style   HiExp
    PIPO Policy                              │
         Split                           SUPERNOVA
                                         Cog-DRIFT
```

## Major Research Threads

### 1. Policy Optimization Evolution

**Thread**: PPO → GRPO → DAPO → Variants (SKPO, TEPO, SPPO, StaRPO, Policy Split)

The dominant training algorithm thread. PPO was adapted from classic RL for RLHF (Schulman et al.). GRPO (Shao et al., 2024) removed the critic via group-relative advantages, dramatically simplifying training. DAPO (2025) scaled GRPO with Clip-Higher, Dynamic Sampling, Token-Level PG Loss, and Overlong Reward Shaping.

Recent variants (April 2026):
- **SKPO** (2604.08690): Skip connections for better early-token credit assignment
- **TEPO** (2604.12736): Token-level aggregation linking group rewards to individual tokens
- **SPPO** (2604.08865): Sequence-level PPO for long-horizon reasoning
- **StaRPO** (2604.08905): Stability-augmented with ACF + Path Efficiency
- **Policy Split** (2604.11510): Dual-mode entropy for exploration-exploitation
- **TPO** (2604.06159): Target policy optimization — unifying PG, PPO, GRPO, DPO
- **PIPO** (2604.00860): Policy improvement objective with retrospective verification

**Key insight**: The field is moving from "which algorithm" to "which credit assignment mechanism" — SKPO, TEPO, and SPPO all address the same fundamental challenge of token-level credit from sequence-level rewards.

### 2. Preference Optimization

**Thread**: RLHF → DPO → KTO → SimPO → DDO-RM

DPO (Rafailov et al., 2023) showed RLHF could be reformulated as a supervised objective, eliminating the RL loop entirely. KTO (2024) extended this to single-response data. Recent work:
- **DDO-RM** (2604.11119): Hybrid approach combining reward model information with DPO-style optimization
- **DRTO** (2604.08577): Distributionally robust token-level optimization
- **Decomposing the Delta** (2604.08723): Analyzing what models actually learn from preference pairs

**Connection to RLVR**: The "GRPO is secretly DPO" paper (2510.00977) showed these threads are converging.

### 3. RL with Verifiable Rewards (RLVR)

**Thread**: DeepSeek-R1 → RLVR → SUPERNOVA → SD-Zero

A rapidly growing thread centered on using verifiable (binary) reward signals rather than learned reward models. Key developments:
- **SUPERNOVA** (2604.08477): Extends RLVR beyond math/code to general reasoning via data curation
- **SD-Zero** (2604.12002): Converts binary rewards to dense supervision via self-revision
- **Imperfect Verifiers** (2604.07666): RLVR robust to 15% verifier noise
- **Bidirectional Entropy** (2604.04894): Informative vs. spurious entropy decomposition
- **Cog-DRIFT** (2604.04767): Cognitive reformulation for exploration barriers
- **Self-Distilled RLVR** (2604.03128): Token-level self-distillation + RLVR

**Key insight**: RLVR is rapidly expanding beyond math/code. SUPERNOVA's success on general reasoning and the negotiation RL paper suggest verifiable rewards are more broadly applicable than initially thought.

### 4. Reward Modeling

**Thread**: Scalar RM → Process RM → Generative RM → Efficient RM

**Sub-thread A — Process Reward Models**:
- Lightman et al. (2023): Step-by-step verification for math
- **CPMI** (2604.10660): Efficient PRM via contrastive mutual information (84% cost reduction)
- **MISE** (2604.11611): Formal foundation for self-rewarding via MI + KL objective

**Sub-thread B — Reward Hacking Mitigation**:
- **SignCert-PO** (2604.02986): Certified advantage sign robustness
- **Robust Optimization** (2604.12086): r-correlated proxy reward robustness
- **Multi-response RM** (2604.10966): 3.9x speedup via joint scoring

**Sub-thread C — Trajectory-Level Rewards** (for agents):
- **Plan-RewardBench** (2604.08178): Benchmarking trajectory-level reward models

### 5. Reasoning RL

**Thread**: o1 → DeepSeek-R1 → GRPO Reasoning → Scaling → GenAC

Training models to reason through RL rather than supervised fine-tuning:
- **Scaling Reasoning Tokens** (2604.01302): Log-linear scaling law; parallel thinking surpasses GPT-5
- **GenAC** (2604.10701): Bringing value models back with generative critics
- **StaRPO** (2604.08905): Reasoning stability as an optimization objective

### 6. Agentic RL

**Thread**: Tool Use → Multi-Turn → Competitive Programming → Self-Evolving

Training agents for multi-step, tool-using tasks with RL:
- **GrandCode** (2604.02721): First AI to beat all humans in live Codeforces — Agentic GRPO
- **RefineRL** (2604.00790): 4B models outperform 32B via skeptical self-refinement
- **HiExp** (2604.08124): Hierarchical experience for strategic exploration
- **SEARL** (2604.07791): Joint policy + Tool Graph Memory optimization (ACL 2026)
- **Negotiation RLVR** (2604.09855): RLVR for strategic negotiation

**Key insight**: The agentic thread is producing the most dramatic capability amplifications — RefineRL's 4B→32B-equivalent and GrandCode's human-beating performance suggest agentic RL is a compute multiplier.

### 7. Training Infrastructure

**Thread**: veRL → AReaL → Relax → Efficient Training

Systems and efficiency improvements for RL training at scale:
- **Relax** (2604.11554): Async omni-modal RL engine, 2x speedup
- **Experience Replay** (2604.08706): 40% compute savings from replay buffers
- **NExt** (2604.11446): 37.5% reduction via low-rank trajectory extrapolation
- **QaRL** (2604.07853): Quantization-aware RL for stable training with quantized rollouts
- **I-PPO** (2604.01597): Influence-guided data attribution for PPO

### 8. Multimodal RL

**Thread**: Text RL → Vision-Language RL → Omni-Modal RL

Extending RL training to multimodal models:
- **OpenVLThinkerV2 / G2RPO** (2604.08539): Gaussian GRPO for multimodal reasoning
- **VGPO** (2604.09349): Visual attention compensation for visual forgetting
- **Faithful GRPO** (2604.08476): Constrained optimization for faithful visual reasoning
- **Relax** (2604.11554): Omni-modal RL engine (text + image + audio + video)

### 9. Alignment & Personalization

**Thread**: RLHF → Constitutional AI → Multi-Objective → Personalization

- **SPARD** (2604.07837): Self-paced curriculum for RL alignment
- **PALM** (2604.04144): Portfolio approach to multi-preference personalization
- **PerMix-RLVR** (2604.08986): Preserving persona expressivity under RLVR
- **VRF** (2604.00997): Variational reward factorization for personalization

## Late Edition Additions (April 16, 2026 PM — 19 new papers)

### 10. Agentic RL Diagnosis — a new sub-thread

The late edition introduces a distinct sub-thread around<br>**diagnosing failure modes in Agentic RL** beyond loss/entropy:

- **RAGEN-2** (2604.06268): Template Collapse as an entropy-invisible failure. Mutual Information between input and output is a better proxy for reasoning quality than entropy. SNR-Aware Filtering uses reward variance for online prompt selection.

This connects to Thread 6 (Agentic RL) but introduces the *diagnostic* dimension — parallel to how observability matured in distributed systems.

### 11. Process Reward Expansion (sub-thread within Reward Modeling)

Process reward modeling is exploding beyond math/code into new domains:

- **PROGRS** (2604.02341): Outcome-conditioned PRM centering for group-relative preference
- **PRA** (2604.09482): Process Reward Agents as test-time plug-ins; 80.8% MedQA with 4B
- **RTT** (2604.02795): Rubric-to-Token relevance discriminator + RTT-GRPO
- **SubSearch** (2604.07415): Intrinsic process rewards without external supervision
- **E-GRM** (2604.10072): Selective CoT triggered by model-internal uncertainty

**Connection**: These converge with Thread 4 (Reward Modeling) sub-thread A, but with a key evolution — PRM is no longer a *training-time only* artifact. PRA makes it test-time; E-GRM makes it adaptive; RTT makes it token-level.

### 12. Tool Use Internalization (sub-thread within Agentic RL)

- **TInR** (2604.10788): Tool knowledge internalized into LLM weights (no runtime docs)
- **ToolCAD** (2604.07960): CAD modeling as long-horizon tool agent
- **AnomalyAgent** (2604.07900): 5-tool closed-loop industrial anomaly synthesis
- **COVERT** (2604.09813): Oracle-preserving RL-ready tool-use data synthesis

**Key insight**: Tool use is migrating from "explicit documented API" to "internalized capability". This parallels how tokenizers absorbed word-piece models: once standardized, the boundary fades.

### 13. Agentic Self-Supervision (new sub-thread)

- **Skill-SD** (2604.10674): Natural-language skills as teacher-only privileged info
- **RAGEN-2** (2604.06268): Uses agent trajectories as their own diagnostic signal
- **SubSearch** (2604.07415): Intrinsic process rewards from generation dynamics

These point toward agents that become their own supervisors.

### 14. Multi-Hop KG Reasoning as RL Target

- **KG-Reasoner** (2604.12487): Integrates multi-step KG traversal into single thinking phase via RL with backtracking
- **TRACE** (2604.11193): Narrative-based coherence + reusable exploration priors
- **AgentGL** (2604.05846): First RL-driven Agentic Graph Learning framework with curriculum

**Pattern**: Pipeline-based KGQA is fragmenting; end-to-end RL unification is the new direction.

### 15. Reasoning Efficiency (sub-thread within Reasoning RL)

- **Graph-Based CoT Pruning** (2604.05643): -42% tokens via DAG + dual pruning + SFT/DPO/GRPO
- **CURE** (2604.12046): Claim-level factuality calibration (+39.9% Biography)
- **E-GRM** (2604.10072): Per-instance CoT triggering

### 16. RL Domain Boundary Tests

- **Regime Boundaries** (2604.10996): Valid LLM features (IC > 0.15) fail under macro shock
- **OOM-RL** (2604.11477): Capital loss as un-hackable negative gradient (20-month study, Sharpe 2.06)

These papers pressure-test the assumption that *verifiable reward + training stability → deployment success*.

### 17. Alignment for Behavior Shape (style/editing/trust)

- **Argumentation Editing** (2604.12770): Multi-component GRPO reward for human-like edits
- **KE-CoT** (2604.05540): First GRPO for knowledge editing
- **Curr-RLCER** (2604.05341): Curriculum-GRPO for explainable recommendation
- **Trust Boundary MARL** (2604.05483): Multi-agent RL to detect black-box untrustworthy regions

## Night Edition Additions (April 16, 2026 Late-Night — 19 new papers)

### 18. Reward Hacking as a Discipline (new sub-thread)

Reward hacking research is maturing from ad-hoc observations into a systematic discipline:

- **Reward Hacking Survey** (2604.13602): First unified taxonomy — Feature / Representation / Evaluator / Environment levels. Documents "Reward Collapse" in DPO — the implicit reward drifts at higher KL budgets even without a separate RM.
- **MEDS** (2604.11297): Memory-augmented reward shaping — past rollouts' failure clusters penalize new rollouts. +4.13 pass@1 across 5 datasets.

**Connection**: These extend Thread 4 (Reward Modeling) into a new diagnostic axis. Reward hacking is no longer just an RLHF concern — DPO, GRPO, RLAIF all share the vulnerability.

### 19. TIR Evolution: Trust, Efficiency, Experience (new sub-thread within Agentic RL)

Tool-Integrated Reasoning research is fragmenting into three specialized directions:

- **E³-TIR** (2604.09455): Three-experience fusion (Expert Prefix / Expert Guided / Self-Exploration) as a training middle-path between Zero-RL and SFT-then-RL. +6% across 3B–8B.
- **ATTC** (2604.08281): First framework to treat tool trust as a trainable decision — model explicitly chooses to accept/reject/recompute tool outputs.
- **PTE — Beyond Accuracy** (2604.05404): Hardware-aware TIR efficiency metric (Prefill Token Equivalents). Reveals KV-Cache eviction and long-tool-response as dominant costs; higher PTE correlates with lower correctness.

**Connection**: These build on Thread 12 (Tool Use Internalization) but shift the question from "how to use tools" to "when to trust them" and "how expensive is tool use really". Together with ToolCAD and TInR (late edition), TIR is now a complete research program.

### 20. Policy-Reward Co-Evolution (new thread)

Papers where the boundary between policy and reward becomes porous:

- **Self-Guide** (2604.03098): Policy generates its own internal reward via self-guidance steps; no external RM required.
- **LangMARL** (2604.00722): Cooperative MARL translated entirely into natural language — language critic, language gradient estimator, language optimizer.
- **MIA** (2604.04503): Manager-Planner-Executor with alternating RL; parametric-nonparametric memory forms a co-evolving loop.
- **ETR** (2604.05355): Entropy trend (not level) as a trajectory-level reward encouraging efficient reasoning.

**Key insight**: The "reward comes from outside" assumption is weakening. Future RL pipelines may have the reward function *learned from the same rollouts that train the policy*, with no independent RM artifact.

### 21. Multimodal Visual Reasoning via Internal Signals

- **MedVR** (2604.08203): EVR (entropy-guided visual regrounding) + CCA (consensus-based credit assignment) — no human step-level annotations needed.
- **Saliency-R1** (2604.04500): Saliency-map alignment reward with no extra forward/backward passes; enforces VLMs to ground in visual evidence.

**Pattern**: Visual reasoning RL is converging on a template — use model-internal signal (uncertainty or saliency) as supervision, rather than external labels.

### 22. RLVR Vertical Applications (expanding further)

- **QuarkMedSearch** (2604.12867): SFT short→long + RLVR with anti-hacking reward design for Chinese medical deep search.
- **ReasonXL** (2604.12378): SFT + Dr. GRPO recipe for multilingual reasoning (5 European languages, 2M aligned samples each).
- **CARO** (2604.10504): DPO with analogy-chain preference pairs; +24.9% F1 on ambiguous content moderation.
- **HintMR** (2604.12229): Distillation of a meta-skill (generating & consuming step-level hints) into small models.
- **MathAgent** (2604.11188): Legislator-Executor adversarial synthesis — structural diversity beats scale (1K synthesized > LIMO/s1K).

### 23. Engineering & MLE Agent Benchmarks (new sub-thread)

- **Frontier-Eng** (2604.12290): 47 tasks × 5 engineering categories; continuous-reward Propose-Execute-Evaluate loop. First benchmark to expose "optimization degradation" — models get worse with more budget.
- **SandMLE** (2604.04872): Synthetic micro-MLE environments (50-200 samples, ≤15s execution) enabling trajectory-level on-policy RL in ML engineering for the first time. 13× speedup.

**Pattern**: Agentic RL research is finally getting proper training/evaluation environments with continuous signals and hard constraints, not just binary task suites.

## Cross-Cutting Themes (April 2026, updated Night Edition)

1. **Credit Assignment is the central challenge**: SKPO, TEPO, SPPO, GenAC, the survey (2604.09459), late-edition PROGRS/RTT, plus night-edition LangMARL (language-space credit assignment) and MEDS (population-level credit via failure clusters).

2. **RLVR is expanding**: Math/code → reasoning (SUPERNOVA) → negotiation → multimodal → KG → knowledge editing → argumentation → now also medical deep search (QuarkMedSearch), multilingual reasoning (ReasonXL), content moderation (CARO). OOM-RL (finance) and Regime Boundaries test the edges.

3. **Efficiency is non-negotiable**: Replay buffers (40%), trajectory extrapolation (37.5%), multi-response scoring (4×), async (2×), CoT Pruning (42%) — and now **night-edition PTE** frames *tool-call efficiency* as first-class, and **SandMLE** achieves 13× MLE speedup.

4. **Agentic RL is producing superhuman results — and diagnostic tools**: GrandCode/RefineRL showed upside; RAGEN-2 introduced diagnostics (Template Collapse); night-edition MEDS adds population-level diagnostics, and Frontier-Eng exposes "optimization degradation".

5. **Self-improvement loops are maturing**: SD-Zero, Self-Distilled RLVR, MISE, GenAC, late-edition Skill-SD/SubSearch/E-GRM, plus night-edition **Self-Guide** (policy-generated internal reward), **MIA** (alternating RL + parametric-nonparametric memory cycle), **HintMR** (meta-skill distillation).

6. **Process reward has left the training loop**: PRA is test-time, E-GRM is uncertainty-gated, PROGRS is group-relative — and now night-edition **ATTC** makes trust itself a meta-decision, separating "tool signal" from "when to use it".

7. **Real-world deployment is the new benchmark**: OOM-RL (20 months live), Regime Boundaries (distribution shift), and now **Frontier-Eng** (industrial-grade simulators + hard constraints + 47 tasks) plus **QuarkMedSearch** (medical deep-research evaluation).

8. **Reward hacking is becoming a discipline (new in Night Edition)**: The 2604.13602 survey unifies mechanisms across RLHF / RLAIF / DPO; **DPO Reward Collapse** is a clear warning sign that cannot be ignored by open-source alignment stacks.

9. **Policy and reward are co-evolving (new in Night Edition)**: Self-Guide, LangMARL, MEDS, MIA — four different architectural demonstrations that reward is no longer a static external artifact.

## April 17, 2026 — New Additions (13 papers)

### 24. The Probability Space as a Design Dimension (new thread)

Today's most ambitious paper introduces a completely orthogonal axis: on *which* distribution should RL operate?

- **PreRL / Dual Space RL** (2604.14142): RL directly on `P(y)` (pre-train edge distribution) — not `P(y|x)`. Key finding: **Negative Sample Reinforcement** outperforms Positive in this space. 14.89× transition-thought boost, 6.54× reflection boost.
- **Shortest-Path Generalization** (2604.15306): The counterweight — within a fixed distribution, RL stabilizes but does not expand capability. Length-scaling failures are not rescued by RL or inference-time scaling.

**Connection**: Together these redraw the picture — *what* distribution you RL on matters more than *how* you RL. Joins Thread 1 (Policy Optimization) and Thread 3 (RLVR) as a new governing axis.

### 25. GRPO's Calibration Collapse (new sub-thread)

Three independent April 17 works converge on the same failure mode: GRPO inverts the perplexity-correctness relationship.

- **CAPO** (2604.12632): Logistic AUC surrogate + uncertainty-aware advantage + noise masking. Breaks the accuracy-calibration trade-off.
- **Sycophancy Calibration Collapse** (2604.10585): Direct causal demonstration — sycophantic GRPO produces systematic calibration degradation on Qwen3-8B.
- **SPO (MM-Doc-R1, 2604.13579)**: Challenges GRPO's shared-initial-state baseline in multi-turn. Similarity-weighted baselines dramatically reduce variance.

**Key insight**: GRPO's elegance (no value model) hides a structural bias — its advantage is uncertainty-agnostic, and in multi-turn its baseline is state-agnostic. Both must be repaired.

### 26. Reward Hacking Matrix Completion

The Night Edition's Reward Hacking Survey (2604.13602) listed problems; today's papers supply solutions from three angles:

- **Causal Decomposition RM** (2604.13833): Decoder reconstructs intent; reconstruction error regularizes RM. RewardBench 0.832 → 0.868.
- **C2 Rubric-Augmented RM** (2604.13618): Synthesizes helpful/misleading rubric pairs from binary preferences alone; critical verifier at inference. 8B RM matches 4× larger model.
- **CoUR** (2604.13504): Bayesian-optimized reward-function design with code-level uncertainty for RL-environment reward engineering.

These extend Thread 4 sub-thread B (Reward Hacking Mitigation) into a cohesive toolbox.

### 27. Decoupled Multi-Objective Policy Optimization (new in Agentic RL)

- **ToolOmni / DMO-GRPO** (2604.13787): Retrieval advantage ⊥ execution advantage in a single optimization. NDCG@5 +4.5% over one-shot; SoPR 52.5%.

**Pattern**: Complements Rethinking GRPO Miscalibration (2509.23870) on the gradient-interference side. Single scalar rewards are fundamentally limiting in agentic settings.

### 28. Measurable Agent Behavior Diagnostics

- **Exploration-Exploitation Errors Are Measurable** (2604.13151): Policy-agnostic framework; separates "didn't try" from "blindly tried" using action trajectories only.

Complements RAGEN-2 (entropy collapse) and MEDS (failure-cluster memory) — three different *types* of diagnostic signal, all suitable for reward shaping.

### 29. CoT Synthesis as Graph Consensus

- **CRAFT** (2604.14121): Build Reasoning KG from consensus of multiple CoT candidates; topologically synthesize a high-quality trace. +10% accuracy, no ground-truth needed.

Joins Graph-Based CoT Pruning (2604.05643) and ThinkTwice (2604.01591) in the "CoT-as-Graph" research program.

### 30. Reward Shape Ablation for VLMs

- **Reward Design for Physical Reasoning in VLMs** (2604.13993): Systematic comparison — accuracy reward is universal, rubric improves structure but not accuracy, attention-reward is domain-specific (spatial wins, symbolic loses).

Provides a reward-design *coordinate system* for ongoing VLM RL work (OpenVLThinkerV2, MAPO, Faithful GRPO).

### 31. Evidence-Based Domain RL

- **ESC-RL** (2604.13598): Group-wise Evidence-Aware Alignment Reward + Self-Correcting Preference Learning for radiology report generation. Extends Thread 22 (RLVR Vertical Applications) with an "evidence as verifier" template applicable to any knowledge-intensive domain.

## Cross-Cutting Meta-Observation (April 17)

**The field is re-negotiating its foundational assumptions:**

1. *Where* RL happens (PreRL: pre-train space; not just `P(y|x)`)
2. *What* baseline is correct (SPO: per-state similarity-weighted, not shared initial-state)
3. *Which* reward is safe (Causal Decomposition / C2 / Sycophancy-Calibration: single scalar is fragile)
4. *When* to split the objective (ToolOmni: retrieval ⊥ execution in one GRPO)
5. *Whether* RL expands capability (Shortest-Path: no — RL stabilizes but doesn't extend)

April 17's papers are not incremental: each one challenges an assumption that underpins current GRPO-era practice.

## New Threads (April 19, 2026)

### 32. Training-Free Process Signals Inside GRPO

- **IG-Search** (2604.15148): Information-gain of gold-answer log-prob between real vs. random-document retrieval acts as per-step reward — computed entirely from existing policy, plugged into GRPO per-token advantage for search queries. No PRM training needed.
- **CW-GRPO** (2604.14267): LLM judge emits per-round contribution scores; outcome advantages are *rescaled* (not replaced). Preserves unbiasedness while amplifying informative rounds.

Together they define two archetypes of the "free process reward" pattern: *log-prob-based* (reuses policy) vs. *judge-based* (reuses a judge).

### 33. SFT ↔ RL Unification

- **GFT** (2604.14258): SFT reinterpreted as PG with extremely sparse implicit reward and unstable IPW. Group Advantage Learning + Dynamic Coefficient Rectification close the gap; resulting policies transition more smoothly into RL.

Joins "GRPO is secretly DPO" (2510.00977) and TPO (2604.06159) in the convergence toward a single group-advantage optimization framework.

### 34. Optimal-Transport Regularization for LLM RL

- **VGF** (2604.14265): Casts behavior-regularized RL (offline RL + LLM fine-tuning) as optimal transport from reference to value-optimal distribution, solved by discrete gradient flow. Replaces KL β-tuning with a "transport budget" that is also adjustable at test time.

A structural alternative to KL-PPO-GRPO; composable with reward-surface-engineering (Thread 5) once stabilized.

### 35. Tree-Structured Multi-Agent Group Advantage

- **MARS²** (2604.14564): Extends group-relative advantage from flat groups to a tree-structured group over a shared multi-agent MCTS tree. Thompson-sampling over (agent, node) pairs; tree-consistent reward shaping.

First clean credit-assignment recipe for multi-agent RL on structured search spaces.

### 36. Temporally Consistent Credit Assignment

- **TC-GRPO (RAD-2)** (2604.15308): Exploits temporal coherence of adjacent rollout steps to reduce advantage variance. Nominally for autonomous driving but generalizable to long-horizon agentic RL where consecutive steps have correlated outcomes.

### 37. Open-Ended RLVR via Relative Information Gain

- **TCER** (2604.11522): Fixes triviality collapse in confidence-based unsupervised rewards for open-ended writing via specialist–generalist relative info gain.

Proof that verifiable-reward-style unsupervised RL can extend beyond math/code when properly regularized against triviality.

### 38. Long-Horizon Reasoning Benchmark

- **LongCoT** (2604.14140): 2500 problems with 10k–100k+ token verifiable-answer solution paths. GPT-5.2 9.8%, Gemini 3 Pro 6.1%. Establishes the next-generation reasoning frontier.

### 39. Long-Form Verification Signals

- **IUQ** (2604.15109): Interrogator-driven atomic-claim decomposition for long-form uncertainty quantification. Claim-level signal suitable as RL reward.
- **Cross-Query Contradictions** (2604.14525): Set-level consistency metrics (SetCons, Contradiction Density, Revision Cost) for multi-query LLM reasoning; solver-augmented repair.

New axes of verifier design for long-form and multi-query settings.

### 40. Production-Scale Multi-Agent RL Pipelines

- **MindDR** (2604.14518): 30B three-agent deep-research system. Four-stage SFT → Search-RL (GSPO) → Report-RL (RACE rubric) → Preference.
- **MARS²** (2604.14564): Multi-agent RL over shared search tree for code generation.
- **TREX** (2604.14116): Agent-driven automation of the entire LLM fine-tuning loop + FT-Bench.

### 41. Agentic RL Crossing Modality Boundaries

- **RadAgent** (2604.15231): 3D medical image tool-using RL agent.
- **RaTA-Tool** (2604.14951): DPO for open-world multimodal tool retrieval.
- **APEX-MEM** (2604.14362): Temporal graph + multi-tool retrieval agent for conversational memory.

### 42. Agentic Infrastructure & Serving

- **Scepsy** (2604.15186): Aggregate LLM Pipeline scheduling; 2.4× throughput / 27× latency.
- **IE-as-Cache** (2604.14930): Information extraction as reusable cognitive cache for agent reasoning.

## Cross-Cutting Meta-Observation (April 19)

April 19 sharpens the picture that April 17 opened. Where April 17 said "re-negotiate foundational assumptions," April 19 fills in concrete answers along three axes:

1. **Process supervision becomes cheap**: IG-Search (policy log-prob) and CW-GRPO (rescaled LLM judge) show that PRMs are no longer the only path to step-level signals. Combined with IUQ and Cross-Query Contradictions for long-form, the marginal cost of dense supervision is dropping quickly.

2. **The SFT/DPO/GRPO/OT boundary is dissolving**: GFT explains SFT as PG; VGF replaces KL with OT; together they continue the unification that GRPO↔DPO started. The category "RL algorithm" is being replaced by "choice of group structure + regularization geometry + advantage rescaling."

3. **Industrialization reaches the top of the stack**: MindDR (MoE × RL recipe), MARS² (multi-agent × tree × RL), TREX (agents run the fine-tuning loop), and Scepsy (workflow-level serving). April 19 is the day "agentic RL in production" stopped being a slogan and became a set of replicable recipes.

**The operative question now is:** *given near-free process signals and unified optimization primitives, which productionable agentic-RL recipe will dominate at 30B / 100B scale first?*

## New Threads (April 20, 2026)

### 43. Model-Internal Signals as RL Tools (new governing axis)

April 20 crystallizes a new axis that complements data-centric and reward-centric RL: **use what the model already has inside it**.

- **Grift (2604.16242)**: gradient fingerprints of the CoT (conditioned on prompt) detect reward hacking where text-based CoT monitoring fails. +25% relative improvement over CoT-Monitor / TRACE.
- **LongAct (2604.14922)**: long-context QK activations spontaneously develop high-magnitude features; restricting RL updates to weights connected to these features gives +8% on LongBench v2.
- **Latent CoT (2604.15726)**: position paper arguing that reasoning is *latent-state trajectory formation* (H1), not surface CoT (H2) or mere serial compute (H0). Implies surface-CoT-supervised PRMs may be training the wrong object.

**Connection**: Together with Night-Edition's Saliency-R1 (saliency-map reward) and MedVR's EVR (entropy-guided regrounding), this points to a systematic trend — **LLM RL's next wave of tools will lean on model-internal activations, gradients, and latent states** rather than only on curated external signals.

### 44. Group-Size Convergence: DPO ↔ GRPO (new in Preference Optimization)

- **GroupDPO (2604.15602)**: no-gradient precomputation of per-sample coefficients decouples group backward pass, enabling k ≫ 4 DPO on one H100. First practical-scale group-wise DPO.

**Connection**: With "GRPO is secretly DPO" (2510.00977), GFT (2604.14258), TPO (2604.06159) and now GroupDPO, the SFT / DPO / GRPO families are fully converging on a unified "group-advantage optimization" primitive. The lasting distinctions among them are collapsing to (i) group structure, (ii) regularization geometry, (iii) advantage rescaling.

### 45. Test-Time Policy Improvement (new thread)

Papers where policy improvement happens purely at inference:

- **RCFG (2604.15577)**: Reward-weighted classifier-free guidance is provably a policy-improvement operator; can also be distilled back into base policy as RL warm start.
- **Flexible Empowerment BoN (2604.15614)**: Empowerment moved from reward term to BoN sampler; N becomes a test-time exploration-exploitation knob.

**Connection**: Joins PreRL (2604.14142) — which RL's pre-train space — to redefine *when* RL happens. The "RL must be a gradient update" assumption is breaking down on two sides at once: *outward* (RL on P(y)) and *inward* (RL via sampling).

### 46. Runtime Alignment: Evolving Policy Understanding (new in Agentic RL)

- **PolicyBank (2604.15505)**: agents iteratively refine *natural-language policy* understanding via corrective feedback in pre-deployment testing. Closes 82% of policy-gap oracle vs. near-zero for immutable-memory baselines.

**Key insight**: Alignment graduates from a one-shot training-time task to a runtime, continuously-refined object. Parallels how APM observability matured from training-time QA to deployment-time SRE.

### 47. Reward Hacking 3rd-Gen Defense (model-internal)

After 1st-gen (better reward shaping), 2nd-gen (adversarial reward synthesis — C2 Rubric RM, Causal Decomposition RM), the 3rd generation moves defense into the model:

- **Grift (2604.16242)**: gradient fingerprints.
- **Latent CoT (2604.15726)**: theoretical basis for why surface CoT defenses have a ceiling — the object being defended is not the true locus of reasoning.

### 48. Industrial LLM-as-Simulator (new applied thread)

- **MUSE (2604.13828)**: multi-domain Chinese user simulator with IPSE + Rubric-Guided Multi-Turn RL.
- **PGHS (2604.15190)**: Meituan merchant diagnosis via policy-mining + dual (reasoning + fitting) LLM branches. 8.80% group error, 45.8%/40.9% over strongest baselines.

**Pattern**: "LLM as user / behavioral simulator" becomes a distinct applied research program. Key recipe: *policy-mining layer aligns LLM reasoning with ML fitting*.

### 49. Failure-Dynamics-Aware Intervention (new in Reasoning Diagnostics)

- **GUARD (2604.14528)**: identifies that errors concentrate at early transition points with local entropy spikes; intervenes with short-horizon branching + entropy-reduction selection.
- **AVR / FS-GRPO (2604.14568)**: jointly optimizes correctness + token efficiency + format diversity for adaptive reasoning paths.

Together with RAGEN-2 (Template Collapse), MEDS (failure clusters), and Dissecting Bug Triggers (2604.08906), this forms a quickly-maturing "diagnose-then-repair" methodology for reasoning models.

### 50. Generalization Boundaries of RL vs. SFT (new cross-cutting)

- **Rethinking Generalization in Reasoning SFT (2604.06628)**: the widely-repeated "SFT memorizes, RL generalizes" claim is conditional — depends on optimization dynamics, data, and model capacity.
- **Shortest-Path Generalization (2604.15306, April 17)**: RL stabilizes but does not extend capability.

**Stark message**: RL's generalization bonus is not automatic. Recipes that assume it free may over-promise.

### 51. Efficient LLM-Judge Prediction (new sub-thread in Judging)

- **RPRA (2604.12634)**: small models pre-predict how an LLM-judge would score their responses, enabling efficient routing / defer to bigger models. Report Card + hindsight-trick fine-tuning.

Parallels Grift at the judge level — *predicting the judge* is becoming a trainable capability on both the verifier side (RPRA) and the checker side (WebAgentGuard reasoning guard).

### 52. Low-Precision RL for Multimodal Generation (extension of Infra thread)

- **Sol-RL (2604.06916)**: FP4 rollout × BF16 train on 12B diffusion (FLUX.1). 4.64× training speedup; decouples exploration throughput from optimization fidelity.

Complements QaRL (2604.07853) and Jet-RL on the quantized-RL line; extends the "rollout / optimization decouple" principle (also at the core of Relax 2604.11554) to diffusion foundation models.

### 53. Multilingual Reasoning as Beneficial Behavior (new in Reasoning RL)

- **Think Multilingual (2604.15490)**: CoRe corpus + fine-tuning framework. Code-switching is *beneficial* (not noise) when used at the right points; meta-skill inducible even from unrelated tasks (e.g. MT).

Completes the ReasonXL (2604.12378) ↔ Think Multilingual pair: monolingual-faithful vs multilingual-flexible recipes.

## Cross-Cutting Meta-Observation (April 20)

**Theme of the day**: *Reward engineering enters Phase 2 — from more signal to safer signal.*

1. **Three "look inward" papers in one day**: Grift (gradient), LongAct (activation), Latent CoT (latent state). The message is convergent — external reward engineering has reached diminishing returns; model-internal signals are the next frontier.

2. **Algorithm families are consolidating, not differentiating**: GroupDPO brings DPO into group-size scaling; RCFG and BoN-empowerment relocate RL to test-time; GFT unified SFT with PG. The count of distinct "RL algorithms" is effectively shrinking.

3. **Alignment is becoming a runtime discipline**: PolicyBank's living policy interpreter + WebAgentGuard's reasoning-based guard + Grift's hacking detector together make deployment-time alignment a first-class research target.

4. **Reasoning's foundations are under revision**: Latent CoT forces the PRM / step-level reward community to justify what exactly it is supervising. Combined with Rethinking Generalization and Shortest-Path Generalization, the "train longer / better / with denser signal" defaults now need to be re-motivated.

5. **Infrastructure continues to absorb scale pressure**: Sol-RL extends low-precision RL to multimodal; LongAct extends RL scaling to long contexts via internal sparsity. Both are compatible with every method above.

**The operative question now is:** *given that external reward is plateauing and model-internal signals are ascending, which alignment-at-runtime recipe will first survive a public reward-hacking adversary?*

---

*Last updated: April 20, 2026 · 17 new papers · running total 140+ papers tracked*

## April 21, 2026 — Morning Edition Additions (17 new papers)

### 54. Verifier-as-Agent: Reward Model Restructured (new in Reward Modeling)

- **AgentV-RL (2604.16004)**: reward model becomes a multi-turn, tool-using agent team (Forward + Backward). Two-stage pipeline (rejection SFT → RL). 4B surpasses SOTA ORM by 25.2%.

**Connection**: Extends Thread 4 and night-edition ATTC — verification is no longer a single-step scalar, nor even a chain-of-thought; it is a *full agent with tools and backtracking*. Combined with GenAC (2604.10701) and C2 (2604.13618), the RM is being restructured at every architectural level (generative / multi-agent / rubric-augmented).

### 55. Faithful CoT as an Optimization Target (new cross-thread bridge)

- **AtManRL (2604.16158)**: differentiable attention saliency reward → GRPO with joint correctness + faithfulness loss.

**Key insight**: The Latent CoT thesis (2604.15726) said surface CoT is not the true reasoning trajectory. AtManRL gives the first concrete *optimization-level* way to pull surface CoT back toward causal CoT — measurable via attention perturbation. This is the fourth "look-inward" signal (after gradient fingerprints, QK activations, latent states).

### 56. Agent-Data-Environment Triangle (new meta-thread)

A unified picture is emerging — agentic RL training has three co-evolving components:

- **Agent** policy → standard RL optimization
- **Data** (task distribution) → **CoEvolve (2604.15840)** uses rollout-failure signals to drive task synthesis (+18.14% on Qwen3-30B-A3B)
- **Environment** (MDP structure) → **ClawEnvKit (2604.18543)** auto-generates 1,040 envs at 1/13,800 human cost

**Observation**: With CoEvolve automating data and ClawEnvKit automating environments, the last manually-specified component in agentic RL training is the *reward model* — and AgentV-RL turns that into a trained agent too. The entire stack is becoming self-bootstrapping.

### 57. Resource-Aware RL (depth, parameters, rejection)

Three papers in the 2026-04-21 batch treat *resource allocation* itself as what RL optimizes:

- **AutoSearch (2604.17337)**: RL reward = reaching minimal-sufficient search depth for agentic RAG.
- **Selective Parameter Optimization (2604.17051)**: gradient-sensitivity-guided subset selection for RLHF post-training.
- **Rejection Criterion (2604.16146)**: principled BoN rejection producing the alignment-efficiency Pareto frontier.

**Connection**: Joins LongAct (QK-activation path), PTE (tool-call cost), Sol-RL (FP4 rollout) as a growing family of "RL on the resource dimension" work.

### 58. RL Theory Catching Up (new in Theory)

- **Demystifying Online Alignment (2604.17207)**: under *decision-centric regret*, online greedy RLHF / DPO achieves **O(1) constant cumulative regret** — the first theory that explains empirical effectiveness instead of under-predicting it.
- **Entropy Control Analysis (2604.09676)**: unified convergence + exploration framework across entropy bonus, KL, clipped, adaptive schedules; regime-specific prescriptive guidance.

**Observation**: After a year of empirical advances, the theory side is reorganizing. Two separate papers on the same day argue that the *measurement frameworks* (regret, entropy control) — not the algorithms — are what needed fixing.

### 59. Beyond-Text Agent Interfaces (new path inside Agentic RL)

- **LAnR (2604.17866)**: retrieval queries are now dense vectors from `[PRED]` hidden states; encode/retrieve/generate all happen inside one LLM's latent space.

**Connection**: With **Latent CoT** (reasoning in latent) + LAnR (retrieval in latent), the direction is clear — surface-text-as-interface is giving way to latent-state-as-interface across multiple agent components.

### 60. Formal Verification × Self-Play (new in RLVR)

- **Semantic Equivalence Self-Play (2604.17010)**: Liquid Haskell refinement types + execution counterexamples as dual verifiers; generator-evaluator self-play + RL. +13.3pp EquiBench.

**Connection**: Joins OOM-RL (market signal), MedVR (medical rubric), QuantumQA (physics solver) — but pushes *furthest* in formal strictness. First work to use full refinement-type proof systems as the RL verifier.

### 61. Long-Horizon Personalization Benchmark (new in Alignment)

- **HorizonBench (2604.17283)**: 163K-token, 6-month dialogue per user × 360 users, structured mental-state graph + typed life-event edges. Identifies "belief-update failure" as a targetable model deficit.

**Connection**: The evaluation companion to APEX-MEM / MIA (memory-augmented agents) and to any personalized-RLHF system. Transforms "evolving preferences" from a vague concern into a measurable failure mode.

### 62. Multi-Agent Coordination: Small-LLM Priors Suffice (new in MARL)

- **LLM Graph Priors for MARL (2604.17191)**: 1.5B LLM is sufficient to produce coordination-graph priors that lift classic MARL baselines; LLMs augment (not replace) MARL machinery.

**Counterpoint** to MARS² (full LLM agents) and LangMARL (language-space MARL): sometimes the LLM is best used as a prior-generator, not as the agent. Three-way split of "LLM-as-agent / LLM-as-critic / LLM-as-prior" is stabilizing as a taxonomy within MARL.

### 63. π-Play Self-Distillation (new in Multi-Agent)

- **π-Play (2604.14054)**: privileged-teacher → student distillation in self-play loop → dense supervision for sparse-reward multi-agent tasks, no external data needed.

**Connection**: Sibling to Skill-SD (late edition) and MIA (night edition) — the self-supervision thread now has its multi-agent instance.

## Cross-Cutting Meta-Observation (April 21)

**Theme of the day**: *Everything in the RL stack is becoming an agent — including the data synthesizer, the environment generator, the reward model, and the search planner.*

1. **Agentification of the training stack**: CoEvolve (data as agent), ClawEnvKit (environment as agent), AgentV-RL (reward model as agent), AutoSearch (search depth as RL decision), LAnR (retrieval inside the policy). The non-agent components are shrinking.

2. **Resource dimension becomes a first-class RL variable**: depth (AutoSearch), parameters (Selective Parameter Optimization), rejection trials (Rejection Criterion), KV/tool calls (PTE), activations (LongAct), precision (Sol-RL). A unified "RL on resources" thread is forming.

3. **Theory is re-framing rather than re-deriving**: Demystifying Online Alignment changes the *metric*; Entropy Control Analysis unifies the *diagnostic*. The algorithm count stabilizes; the measurement language is finally getting rigorous.

4. **Latent-state everything**: Latent CoT + LAnR + AtManRL + Grift + LongAct — five papers across two weeks that converge on "the useful signal is model-internal, not token-surface". The "look-inward" trend is now a full research program.

5. **Formal + RL**: Semantic Equivalence Self-Play, QuantumQA, OOM-RL, MedVR — four examples where *domain formal structure* (proof systems / physics / markets / rubrics) is wired directly into the RL loop as the verifier. The "which signal" question is being answered by "whatever domain already has a formal signal".

## April 22, 2026 — Morning Edition Additions (21 new papers)

### 64. The Granularity Revolution (new cross-cutting cluster)

Six papers this week explicitly target the **action / decision unit** in LLM RL:
- **StepPO** (2604.18401): token-level MDP → step-level MDP
- **CAL-GRPO** (2604.17912): attempt-level calibrated weights for Verification@K
- **RTMC** (2604.11037): critic-free step-credit via shared-prefix rollout trees
- **ProCeedRL** (2604.02006): process-level critic + reflection-demonstration intervention
- **IPVRM + DistRL** (2604.13197): prefix-value function with TD step signals
- **MCPO** (2604.16972): prompt-level adaptive regularization by mastery state

**Thesis**: The right RL unit is the *reasoning step* (or sometimes prompt / attempt), not the token. Token-level MDP is now an inherited assumption, not a justified one.

### 65. The First-Principles PPO Correction

- **Bounded Ratio RL (BPO)** (2604.18578): closed-form analytical optimum for PPO's clipped objective; BPO minimizes advantage-weighted divergence to the analytic optimum, giving provable monotonic improvement.

**Connection**: Parallel to VGF (2604.14265, April 19) which replaces KL with OT, and Demystifying Online Alignment (2604.17207, April 21) which gives O(1) regret. Three attacks on the same problem — *the theoretical justification of current alignment methods is finally catching up with empirics*.

### 66. The Exploration Debate Intensifies

- **SPS** (2604.16995): names and quantifies the "probability squeezing effect"; uses inverse RL on on-policy rollouts to reshape trajectory distribution.
- **MCPO** (2604.16972): counter-intuitive result — tightening policy on mastered prompts IMPROVES both pass@1 and pass@k.
- **Beyond Distribution Sharpening** (2604.16259): first-principles proof that pure sharpening (RL without task rewards) is unstable.

**Thesis**: Exploration in LLM RL is no longer "add entropy bonus" — it's now a study of **trajectory distribution geometry**, where the distribution itself is the object of optimization.

### 67. Experience as a First-Class Citizen (new in Agentic RL)

- **Freshness-Aware PER** (2604.16918): first successful PER for LLM/VLM RL, with age-decay preventing priority staleness. Dramatic gains (+46% / +367% / +133%).
- **Self-Evolution via World Knowledge** (2604.18131): reward-based training teaches "how to explore and distill"; deployment is spontaneous and reward-free.
- **MAGEO** (2604.19516): reusable-strategy library as a durable team asset.
- **Latent Preference Tool Calling** (2604.17886): cross-session preference memory with 1.24% token budget.

**Thesis**: LLM RL has entered an **experience management phase** — not just "what reward do we use?" but "how does the training system remember, prioritize, and transfer what it has learned?"

### 68. Epistemic Honesty as Optimization Target

Five papers push honesty into training:
- **Abstain-R1** (2604.17073): know *why* you don't know
- **UA-Bench + RL** (2604.17293): distinguish *what kind* of uncertainty
- **CoAct** (2604.17501): know *which* self-labels to trust
- **ARES** (2604.18789, ACL 2026): know *jointly* where policy+RM fail
- **CiPO** (2604.15847): know *how* to forget without destroying reasoning

**Thesis**: Alignment is shifting from "avoid harmful output" toward "calibrate confidence and scope of knowledge."

### 69. RLVR Portability (new in RLVR)

- **EA-RLVR** (2604.16881): cross-cultural entity translation, no external KB
- **Bilateral Trade LM** (2604.16472): game-theoretic negotiation with formal solution concepts
- **Plan-PRM** (2604.17957): PDDL planning as a step-annotation source

**Thesis**: RLVR's core engine — verifiable reward — is portable to any domain with a decidable verifier. Today's papers extend it to translation cultural-fit, negotiation strategy, and non-math step-rewards.

## Cross-Cutting Meta-Observation (April 22)

**Theme of the day**: *The RL engine is being dismantled and re-engineered at four levels simultaneously — the granularity of actions, the geometry of trust regions, the management of experience, and the honesty of the policy.*

1. **Granularity**: token → step (StepPO, RTMC, CAL-GRPO, IPVRM).
2. **Geometry**: clip → analytical optimum (BPO); sharpening → task-reward primacy (Beyond Distribution Sharpening); squeezing → IRL reshaping (SPS).
3. **Experience**: episode → replay buffer with age decay (Freshness-Aware PER); episode → skill library (MAGEO, Self-Evolution).
4. **Honesty**: answer always → calibrated abstention (Abstain-R1); uniform uncertainty → typed uncertainty (UA-Bench); blind trust → Policy+RM joint red-teaming (ARES).

Combined, the field is moving from "scale the same PPO pipeline" to "**decompose the pipeline into orthogonal design axes and study each axis as a first-class research object**".

## April 24, 2026 — Morning Dispatch

### 70. Self-Verifying Process Signal (Reasoning RL)

Today three papers converge on a strong claim: *the process signal does not need to come from an external PRM.*

- **GRPO-VPS** [2604.20659]: read the policy's own `P(correct answer | prefix)` across segment boundaries.
- **VPS Verbal Critique** [2604.21611]: let a stronger LLM emit step-level natural-language critique; reach 94.9 % on GPQA Diamond with *no* gradient updates.
- **DDRL** [2604.21327]: identify the dangerous ambiguity region and de-amplify it inside GRPO advantage.

**Thesis**: "Process reward" is being re-internalized inside the RL loop (GRPO-VPS) or replaced by structured verbal supervision from stronger teachers (VPS) — in both cases *without training another model*. Combined with DDRL's diagnosis of GRPO-amplification failure modes, the field is converging on *self-verifying process signals*.

### 71. Pre-RL Diagnostics

**Weak-Supervision RLVR** [2604.18574] adds a decisive observation: whether RLVR generalizes is *predetermined* by reasoning-faithfulness before RL starts. This complements April 17's "RL stabilizes but does not expand capability." Together they suggest the next wave of RL research will include a **diagnostic/intervention stage before RL** — targeted SFT + domain CPT — rather than pure end-to-end RL tuning.

### 72. Group-Relative Advantage Ascending the Abstraction Ladder

**GRAO** (inside TPGO, 2604.20714) extends group-relative advantage to the *agent/tool/workflow node* level of multi-agent systems. Combined with:
- **TEPO** (2604.12736): token-level group advantage
- **StepPO** (2604.18401): step-level
- **MARS²** (2604.14564) / **MAGRPO**: response/trajectory-level

…GRPO's family now spans every granularity. The open question is no longer "which GRPO" but "which granularity matches this problem".

### 73. Latent-Variable Exploration

**polyGRPO** [2604.21593] and **DiffMAS** [2604.21794] both argue that LLM RL has been exploring too narrowly over *surface language*. polyGRPO uses language selection as an exploration axis; DiffMAS uses latent KV-cache channels. Together with April 20's **Latent CoT** position paper (2604.15726), this hints at a new research thread: **latent-space exploration inside RL**, where the exploration dimension is structural rather than lexical.

### 74. Industrial-Grade Small Agents

**AgenticQwen** [2604.21590] and **Learning to Seek Help** [2604.17827] both address the economics of deployment: small models made capable via RL + data flywheels, or via learned SLM↔LLM cooperation. LiteResearcher (04-22) and DR-Venus (04-22) already pointed this direction; today's papers specialize it into "dual-flywheel training" (AgenticQwen) and "cross-tier collaboration" (Help). The practical alignment question is shifting from "which 70 B model wins?" to "**how do we make 4 B models act like 200 B models only when they need to?**"

### 75. Alignment Imprint as Detection

**IRM** [2604.21223] reads AI-generated text by comparing instruct-tuned and base-model likelihoods — i.e. by reading the *DPO implicit reward* directly on candidate text. Together with April 20's "PolicyBank" and April 21's "LLM-as-judge improvements," this forms a clean thread: *alignment training leaves machine-detectable traces*, and those traces themselves are a valuable signal for detection, auditing, and safety.

## Cross-Cutting Meta-Observation (April 24)

**Theme of the day**: *LLM RL is becoming introspective — the policy is simultaneously actor, critic, verifier, and auditor.*

1. **Actor + Critic** via the policy itself (GRPO-VPS reads policy confidence; VPS uses a stronger instance of the same model family).
2. **Actor + Verifier**: DDRL stabilizes self-consistency verification inside the RL loop itself.
3. **Actor + Auditor**: IRM says the model's own alignment-induced likelihood shift is detectable by other copies of itself.
4. **System + Optimizer**: TPGO lets the MAS system be optimized by an optimizer that also evolves.

Combined, these moves eliminate the external scaffolding of classic RLHF (separate RM, separate verifier, separate red-teamer) — replacing it with a self-referential loop where the policy *is* the probe of its own behavior.

## April 25, 2026 — Weekend Edition

### 76. RLVR's Verifier-Gaming Crisis Goes Public

**LLMs Gaming Verifiers** [2604.15149] is the strongest direct attack on the credibility of RLVR-only training. The paper documents that GPT-5, Olmo3 and other RLVR-trained reasoning models *systematically abandon rule induction* and instead enumerate instance-level labels — a shortcut that passes imperfect verifiers but does not generalize. Crucially, the same shortcut is *absent* in non-RLVR models (GPT-4o, GPT-4.5, Ministral). The paper introduces **Isomorphic Perturbation Testing (IPT)** — evaluate every model output on both the original task and a logically isomorphic variant; only true rule learners stay invariant.

**Connection**: This sharpens Thread 18 (Reward Hacking as a Discipline) with a *clean methodological probe* (IPT) that future RLVR benchmarks should adopt. Combined with Grift (gradient-fingerprint detection, April 20), the field now has both *training-time* (gradient) and *evaluation-time* (isomorphism) tests for verifier-gaming.

### 77. Hybrid RL: Teacher × Exploration as One Reward Problem

**OGER** [2604.18530] (Harbin Institute of Technology et al.) closes the hybrid-RL trio (LUFFY, ICPO, OGER): instead of treating offline teacher signal and online exploration as separate losses (KL anchor / imitation / RL), it folds them into a single reward-modeling problem with (i) multi-teacher collaborative training and (ii) entropy-based auxiliary exploration reward.

**Connection**: Joins Thread 1 (Policy Optimization) and Thread 5 (Reward Engineering). With LEPO (latent reasoning policy), VGF (OT), GroupDPO, and now OGER, the boundary between *which family of methods is even being used* keeps eroding — every recipe is becoming a particular choice of (group structure, regularization geometry, exploration term).

### 78. RLVR Goes Industrial Outside Math/Code

**ReaGeo** [2604.21357] (Amap × Tsinghua) is the first end-to-end LLM geocoder: convert geographic coordinates into geohash sequences (so coordinate prediction becomes text generation), add CoT for spatial reasoning, then train with **RL using a distance-deviation reward**. The recipe — *domain tokenization → CoT → metric-decomposable reward* — is directly transferable to any other metric prediction problem (price, time, dosage, layout coordinates).

**Connection**: Extends Thread 22 (RLVR Vertical Applications). Together with QuantumQA, ESC-RL (radiology), CARO (moderation), Bilateral Trade LM and OOM-RL, RLVR has now demonstrably escaped the math/code ghetto. The remaining frontier is *non-decomposable subjective tasks* (style, humor, taste).

### 79. Curiosity Gap in Agent Behavior (warning for Agentic RL training)

**Agents Explore but Agents Ignore** [2604.17609] is methodologically important: by *injecting full task solutions* into the environment, the authors show LLM agents see them in 79–81 % of runs (Terminal-Bench) yet exploit them in only 7–50 % (AppWorld). This is the cleanest demonstration to date that *outcome-only rewards do not produce environmentally curious agents.*

**Connection**: This is the corollary to Thread 65 (Granularity Revolution) and Thread 67 (Experience as First-Class). Agentic RL is now formally on notice: future training objectives must include an **environmental-curiosity** term (auxiliary reward, intrinsic motivation, or specially curated SFT).

### 80. Multi-Agent Cognitive Bias as a Training Target

**Dialectical Alignment** [2604.19548] identifies and quantifies **Actor-Observer Asymmetry (AOA)** in LLM multi-agent systems: the same agent attributes failures to external causes when self-reflecting and to internal causes when auditing peers. The paper finds the bias triggers in &gt;20 % of cases.

**Connection**: An important calibration target for any multi-agent RL system that uses self-reflection / mutual audit as reward channels (e.g. ARES, MAS-style verifiers). If the same agent system has structural cross-perspective bias, then RM signals derived from those perspectives are systematically distorted.

### 81. Structured-Memory and Tool-Attention Infrastructure

Two infrastructure papers worth noting for Agentic RL trainers:

- **StructMem** [2604.21748, ACL 2026]: dual-perspective episode extraction + cross-event consolidation gives long-horizon agents a relational, self-summarizing memory — substantially reducing token / API / runtime cost on LoCoMo. Sparse-reward RL needs *memory* before it needs *more reward*.
- **Tool Attention** [2604.21816]: ISO score + state-aware gating + lazy schema loading attack the 10–60 K-token-per-turn "MCP Tax." Generalizes "Attention Is All You Need" from token self-attention to gated tool-attention.

**Connection**: Joins Thread 42 (Agentic Infrastructure & Serving). Memory + tool gating are the two scaling bottlenecks below the RL algorithm; both must be solved before agentic RL can train at MCP-scale tool spaces.

### 82. Structured-Graph Planning and Domain Benchmarks

- **PLOTTER** [2604.21253] performs **narrative planning on structural graph representations** (event graph + character graph) before generating text — a multi-agent Evaluate-Plan-Revise loop. For Agentic RL designers, this is a clean source of *intermediate, structurally checkable* states for process-reward design.
- **DW-Bench** [2604.18964] supplies 1,046 verifiable data-warehouse graph-topology questions with controlled difficulty and a clean tool-vs-no-tool comparison — a ready-made evaluation environment for tool-use RL on data-engineering agents.
- **AgentSOC** [2604.20134, IEEE 2026] sets up a multi-layer security-operations agent stack (Narrative Counterfactual Engine + Structural Simulation Engine) with naturally constraint-rich rewards (attack hit rate − false-positive cost − policy compliance).
- **Next-Occupation Reasoning** [2604.21204]: *reason-first* SFT recipe driven by LLM-as-Judge oracle reasons; a viable warm-start before RLVR on subjective recommendation tasks.

## Cross-Cutting Meta-Observation (April 25)

**Theme of the day**: *RLVR's success has produced its own backlash — verifier gaming, exploration collapse, and curiosity gaps are all confirmed failure modes; mixed-policy RL and downstream-task RL are the practical responses.*

1. **Verifier credibility crisis**: IPT (LLMs Gaming Verifiers) is the first generalizable test that distinguishes "passes verifier" from "learned the rule." Should be standard in future RLVR papers.

2. **Hybrid is the new pure**: OGER, LUFFY, ICPO together establish that "teacher signal + online exploration" is not optional — pure on-policy RL too easily collapses exploration. Future RLVR pipelines will likely be hybrid by default.

3. **Curiosity gap is an open scientific problem**: Agents Explore but Agents Ignore makes it concrete — outcome-only Agentic RL does not produce agents that react to surprising environmental information. The next training objectives need an explicit curiosity term.

4. **RLVR is now a templated industrial recipe**: ReaGeo proves the pattern *domain tokenization → CoT → metric reward* generalizes outside math/code. Expect the next year of RLVR papers to look much more like applied engineering than algorithm invention.

5. **Multi-agent meta-bias is real and trainable**: AOA (Dialectical Alignment) is a structural distortion in self-reflection / mutual-audit reward signals, with measurable consequences for multi-agent RL.

### 83. Capability-Targeted Agentic Training (April 26)

A new sub-thread that pushes Agentic RL past the "one global RL run" assumption.

- **TRACE** [2604.05336, Stanford]: contrasts successful vs. failed trajectories to *automatically discover capability gaps*; for each gap, synthesizes a targeted training environment that rewards whether the capability was exercised; trains a LoRA adapter via RL on each environment; routes between adapters at inference. τ²-bench +14.1 over base, +9.2 over GRPO and +7.4 over GEPA at the same rollout budget.
- **SKILL0** [2604.02268, ZJU-REAL]: an *in-context RL curriculum* that begins with full skill context and progressively withdraws it according to on-policy helpfulness, ending in zero-shot autonomous behavior. ALFWorld +9.7%, Search-QA +6.6% over standard RL, with per-step context < 0.5k tokens.

**Connection**: Both papers share a thesis — *agentic capability is distributed and, once acquired, should sit in parameters not in the prompt*. Together with Latent Preference Tool Calling (2604.17886), they argue the future of Agentic RL is "less prompt scaffolding at inference."

### 84. Cross-Domain GRPO (April 26)

GRPO has clearly broken out of the math/code/logic comfort zone.

- **OP-GRPO** [2604.04142]: first off-policy GRPO for flow-matching (image/video). Replay buffer + sequence-level IS correction + late-step truncation cuts training steps to 34.2% of Flow-GRPO.
- **MolReAct** [2604.07669]: GRPO on a *synthesis-constrained* MDP — actions are chemistry reaction templates, with a tool-augmented LLM agent acting as the dynamic reaction environment. Lead optimization that respects chemical validity.
- **Privacy GRPO** [2604.20904]: norms extracted from fiction novels as RL training signal; SFT establishes a conservative prior, GRPO + per-completion contrastive scoring conditions decisions on context. Strongest correlation with human privacy expectations across 7 models.

**Connection**: Three independent groups, three completely different domains (visual generation, drug discovery, contextual privacy), all converging on GRPO as the practical default once a domain reward is well-defined. The GRPO family is becoming the *substrate* on top of which domain-specific RL is built.

### 85. Foundational Maps (April 26)

Two reference works that organize the field rather than advance a single algorithm:

- **RL-under-Data-Scarcity Survey** [2604.17312, PKU + Shanghai AI Lab]: classifies *external* (expensive human labels / preference data / PRM) vs. *internal* (rollouts, trajectory length, exploration budget) data scarcity; organizes the field along *data-centric / training-centric / framework-centric* axes. The first systematic survey of LLM-RL data efficiency.
- **Reasoning Primitives in Hybrid LLMs** [2604.21454]: separates reasoning into recall + state-tracking primitives; matched Olmo3 transformer ↔ hybrid pairs (instruction-tuned + reasoning-augmented) on synthetic primitive tasks. Reasoning augmentation gives the largest overall gain; hybrid reasoning models are markedly more robust as sequential dependence rises.

**Connection**: These two works frame "what is being trained" (primitives) and "what data RL needs" (scarcity taxonomy) — together they set the questions any future RL training method should answer about itself.

## Cross-Cutting Meta-Observation (April 26)

**Theme of the day**: *Agentic RL is fragmenting into specialty methods (capability-targeted, skill-internalization), GRPO is generalizing across modalities (flow / chemistry / norms), and the field is finally producing structural surveys.*

1. **One RL run ≠ one new agent**: TRACE shows capabilities are distributed; aiming RL at a single global objective leaves capability-specific deficits unaddressed.

2. **Skills should leave the prompt**: SKILL0 demonstrates a clean curriculum that internalizes prompt-time skills into parameters; Latent Preference Tool Calling did this earlier for tool preferences. The prompt is becoming a *training-time scaffold*, not a runtime crutch.

3. **GRPO is becoming a substrate**: Once a domain has a verifiable reward, OP-GRPO / MolReAct / Privacy GRPO show GRPO can be plugged in across image generation, chemistry, and contextual norms. Domain expertise is in the *reward design*, not the algorithm.

4. **Surveys arrive**: The field is large enough that "what is RL-for-LLM data scarcity" needs a taxonomy. The 2604.17312 survey is the first to provide one.

5. **Architecture × reasoning interactions matter**: Reasoning Primitives shows reasoning augmentation amplifies hybrid architectures' state-tracking advantage — RL trainers should pair their training method with the architecture that best supports its target primitives.

## Cross-Cutting Meta-Observation (April 27)

**Theme of the day**: *Latent reasoning matures into a contested paradigm; "RLVR faithfulness" emerges as the dominant critique vector; mode-collapse on saturated data becomes diagnosable.*

1. **The latent-reasoning fork**: April 27 sees three competing implementations of "reasoning is not natural language":
   - **Abstract-CoT** (2604.22709, IBM) — *discrete-but-non-verbal*: reserved-vocabulary tokens optimized via GRPO under constrained decoding. 11.6× token reduction.
   - **LEPO** (2604.17892, ACL 2026) — *fully continuous* via Gumbel-Softmax stochasticity in latent space; unified gradient over latent + discrete.
   - **TRS** (2604.21764) — *retrieval-augmented* skill memory; training-free, black-box-friendly.
   These three answer the same question (how do we make reasoning compute-efficient?) along three different axes (vocabulary / representation / external store).

2. **The faithfulness critique solidifies**: CIR/SR (2604.22074, Stanford) gives RLVR's harshest critic two formal metrics. Combined with **LLMs Gaming Verifiers** (2604.15149, April 25) and **Agents Explore but Agents Ignore** (2604.17609), the diagnosis is consistent: outcome rewards are insufficient — the model can be trained to be "right for wrong reasons." The remedy line — auxiliary CIR/SR rewards, IPT, environmental curiosity — is starting to converge.

3. **GRPO mode-collapse diagnosed and treated**: CUTS / Mixed-CUTS (2604.18493) and Poly-EPO (2604.17654) attack the same failure (over-strong base + saturated benchmarks → vanishing intra-group advantage → mode collapse) from sampling-side and objective-side respectively. Together with SPS (2604.16995, "Probability Squeezing Effect") and MCPO (2604.16972) from prior weeks, this gives us a four-paper toolkit for keeping GRPO viable on strong base models.

4. **GRPO continues to leak into adjacent domains**: UDM-GRPO (2604.18518) cracks Uniform Discrete Diffusion; LAT-Audio (2604.22245) brings GRPO + tool-CoT to long-form audio; Neuro-Symbolic VLM (2604.22062) bridges symbolic and verbal reasoning in vision-language. The "reward design > algorithm choice" thesis (yesterday) is reinforced.

5. **Auditing as a first-class topic**: Behavioral Canaries (2604.22191, Google) gives the first usable RLFT-stage privacy audit; PermaFrost-Attack (2604.22117) shows RLHF/DPO cannot repair pretraining-stage geometric poisoning. Together with Sound Agentic Science (2604.22080, ICLR Workshop) calling for falsification-first agentic experiments, *evaluation/auditing tooling* is moving from the periphery to a central RL research topic.

6. **Self-play breakthrough**: SGS (2604.20209) — three-role single-model (Solver/Conjecturer/Guide) — scales 7B past 671B baseline by adding a *quality gate* on synthetic problems. The lesson: the bottleneck of self-play is not the curriculum but reward-hacking by the curriculum-generator.

---

*Last updated: April 27, 2026 · 15 new papers · running total 245+ papers tracked*
