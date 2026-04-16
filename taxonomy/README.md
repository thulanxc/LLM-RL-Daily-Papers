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

---

*Last updated: April 16, 2026 (Night Edition, 23:00 UTC)*
