# Policy Optimization Methods

## Evolution
PPO (2017) → RLHF-PPO (2022) → DPO (2023) → GRPO (2024) → DAPO (2025) → Variants (2026)

## Foundational
- **PPO** — Schulman et al. (2017). Proximal Policy Optimization. Clipped surrogate objective for stable policy updates.
- **RLHF-PPO** — Ouyang et al. (2022). Adapted PPO for language model alignment with human preference reward models.
- **DPO** — Rafailov et al. (2023). Direct Preference Optimization. Reformulates RLHF as supervised learning on preference pairs. [2305.18290]
- **GRPO** — Shao et al. (2024). Group Relative Policy Optimization. Removes critic via group-relative advantages. [2402.03300]
- **DAPO** — ByteDance (2025). Scales GRPO with Clip-Higher, Dynamic Sampling, Token-Level PG Loss. [2503.14476]
- **Dr. GRPO** — (2025). Improved GRPO addressing length bias and variance issues. [2503.20783]
- **REINFORCE++** — Hu (2025). Simplified RL baseline for LLMs. [2501.03262]

## Recent (April 2026)
- **SKPO** — Skip-Connected Policy Optimization for credit assignment. [2604.08690]
- **SPPO** — Sequence-Level PPO for long-horizon reasoning. [2604.08865]
- **TEPO** — Token-Level Policy Optimization linking group rewards to tokens. [2604.12736]
- **Policy Split** — Dual-mode entropy regularization. [2604.11510]
- **TPO** — Target Policy Optimization unifying PG/PPO/GRPO/DPO. [2604.06159]
- **StaRPO** — Stability-augmented with ACF + Path Efficiency. [2604.08905]
- **DDO-RM** — Distributionally guided preference optimization. [2604.11119]
- **DRTO** — Distributionally robust token optimization. [2604.08577]
- **PIPO** — Policy improvement with retrospective verification. [2604.00860]

## April 17, 2026 additions
- **PreRL / Dual Space RL** — First RL on pre-train edge distribution `P(y)` instead of `P(y|x)`. Negative-Sample Reinforcement is 14.89× better for transition thoughts, 6.54× for reflection. [2604.14142]
- **CAPO** — Calibration-Aware Policy Optimization. Logistic AUC surrogate + uncertainty-aware advantage. Breaks accuracy-calibration trade-off in GRPO. [2604.12632]
- **SPO (MM-Doc-R1)** — Similarity-based Policy Optimization. Per-state similarity-weighted baselines replace GRPO's shared-initial-state baseline in multi-turn. [2604.13579]

## April 19, 2026 additions
- **IG-Search** — Step-level reward from Information Gain between real retrieval and counterfactual random retrieval (gold-answer log-prob). Training-free per-token advantage modulation inside GRPO for search agents. +1.6 EM over trajectory-level MR-Search. [2604.15148]
- **CW-GRPO** — Contribution-Weighted GRPO. LLM judge assigns per-round contribution scores; outcome advantages are rescaled (not replaced) by these scores. Preserves group-relative unbiasedness while amplifying informative rounds. +6.3% on Qwen3-1.7B. [2604.14267]
- **GFT** — Group Fine-Tuning. SFT reinterpreted as PG with extremely sparse implicit reward and unstable IPW. Fixed via Group Advantage Learning + Dynamic Coefficient Rectification; yields SFT policies that transition more smoothly into RL. [2604.14258]
- **VGF** — Value Gradient Flow. Recasts behavior-regularized RL as Optimal Transport from reference distribution to value-optimal distribution, solved via discrete gradient flow. Removes explicit policy parameterization and KL hyperparameter; SOTA on LLM RL and offline RL. [2604.14265]
- **TC-GRPO (RAD-2)** — Temporally Consistent GRPO. Adds temporal smoothing across adjacent rollout steps for long-horizon credit assignment. Primarily for planning but generalizable to long-horizon agentic RL. [2604.15308]
- **TCER** — Triviality-Corrected Endogenous Reward. Adapts unsupervised confidence rewards to open-ended writing using specialist–generalist relative information gain + probability-dependent correction, avoiding triviality collapse. [2604.11522]

## April 20, 2026 additions
- **GroupDPO** — Memory-efficient group-wise DPO via no-grad coefficient precomputation. First practical scaling of DPO to k ≫ 4 on a single H100. [2604.15602]
- **RCFG** — Reward-weighted classifier-free guidance is provably a policy-improvement operator. Test-time-only policy optimization and RL warm-start via distillation. [2604.15577]
- **Flexible Empowerment BoN** — Empowerment relocated from reward to Best-of-N sampler (Tsallis-based). N becomes a test-time exploration-exploitation knob. [2604.15614]

## Key Trend (updated April 20)
The credit-assignment thread has fragmented into four orthogonal design axes: (1) **probability space** (PreRL `P(y)` vs. standard `P(y|x)`); (2) **advantage structure** (CAPO calibration-aware, SPO per-state similarity, TC-GRPO temporal-consistent, MARS² tree-structured group, GroupDPO k≫4 DPO); (3) **process signal injection** (IG-Search per-token log-prob IG inside GRPO vs. CW-GRPO per-round contribution rescaling — training-free signal vs. judge-based signal); (4) **regularization geometry** (VGF Optimal-Transport replacing KL). Meanwhile **GFT** demonstrates the SFT↔RL boundary is fully soluble: SFT is a degenerate PG special case. **April 20's GroupDPO + RCFG + Flexible Empowerment BoN add a fifth axis — *when* policy improvement happens (train-time gradient vs. test-time sampling vs. test-time guidance)**. Combined, SFT / DPO / GRPO / OT / RCFG now appear as instances of a single group-advantage + budget-regularized optimization framework indexed by (group size, regularization geometry, advantage rescaling, probability space, update locus).

## Morning Edition (April 21) — 策略优化新增

- **MT-GRPO** [2604.02869] — First multi-turn GRPO with *iterative reward calibration* applied to real customer-service tool-calling agents, addressing long-horizon credit assignment in sparse-reward settings.
- **AtManRL** [2604.16158] — GRPO extension augmenting the outcome advantage with an attention-saliency reward component, enabling joint optimization of accuracy and CoT faithfulness.
- **Selective Parameter Optimization** [2604.17051] — Gradient-sensitivity-guided selective RLHF post-training: updates only task-relevant parameters, matching full-parameter tuning at fraction of compute.

### Connections
- MT-GRPO ↔ CW-GRPO (2604.14267): parallel ways to extend GRPO to multi-turn — temporal calibration vs per-round contribution rescaling.
- Selective Parameter Optimization ↔ LongAct (2604.14922): the "RL on a restricted sub-parameter set" motif — LongAct constrains via self-emergent QK activations; this paper constrains via gradient sensitivity.

## April 22, 2026 additions — 粒度革命 · Granularity Revolution

- **StepPO** [2604.18401] — Position paper: token-level MDP is inadequate for LLM agents; proposes step-level MDP where a "step" (think+tool-call+observe round) is the proper action. Step-level credit assignment aligns reward propagation with decision granularity.
- **CAL-GRPO (Learning to Correct)** [2604.17912] — Calibrated Attempt-Level GRPO for multi-attempt CoT (Verification@K). Proves naive pass/fail weighting is biased; derives unbiased low-variance weights. Outperforms trajectory-level and naive attempt-level on MATH, Maze, structured Markov Chains.
- **Bounded Ratio RL (BRRL/BPO)** [2604.18578] — Closed-form analytical optimal for PPO's clipped objective. BPO minimizes advantage-weighted divergence to the analytical optimum, giving provable monotonic policy improvement — a third path between KL-penalty and heuristic clipping.
- **MCPO** [2604.16972] — Mastery-Consolidated Policy Optimization. Fixes GRPO's two failure modes: (1) vanishing advantage on fully-mastered prompts leads to unbounded policy drift, (2) majority-correct prompts get under-weighted. Adds hinge-KL (only on mastered prompts) + majority-correct weighting. Counter-intuitively improves both pass@1 AND pass@k.
- **SPS** [2604.16995] — Steering Probability Squeezing. First to name and quantify the "squeezing effect" (probability mass concentrating on few high-reward trajectories). Interleaves IRL on on-policy rollouts to reshape trajectory distribution; improves Pass@k without external supervision.
- **RTMC** [2604.11037] — Rollout-Tree Monte Carlo critic-free step-level credit assignment. State-action signatures compress trajectories for cross-rollout state matching; aggregates MC returns on shared prefixes. +3.2pp on SWE-bench Verified over GRPO.

### Key Trend (April 22): The Granularity Revolution
Four papers this week explicitly target the **action/decision unit** in LLM RL:
1. **Token-level → step-level** (StepPO, RTMC, ProCeedRL)
2. **Attempt-level calibration** (CAL-GRPO)
3. **Trajectory distribution-level** (SPS, Beyond Distribution Sharpening)
4. **Analytical PPO structure** (Bounded Ratio RL)
5. **Prompt-level adaptive regularization** (MCPO)

Combined with the emerging consensus from Beyond Distribution Sharpening (2604.16259) that RL must inject task rewards, the field is converging on: **the right RL unit is the reasoning step, and the right regularization is adaptive to mastery state**.

## April 23, 2026 additions
- **EVPO** [2604.19485] — Explained Variance Policy Optimization. Casts the PPO-vs-GRPO choice as a **Kalman filtering** problem, proves Explained Variance (computable from a single batch) is the exact decision boundary between critic and batch-mean baselines, and adaptively switches each step. Beats both PPO and GRPO across classical control, agentic tasks, and math reasoning.
- **CalibAdv (Negative Advantage Is a Double-Edged Sword)** [2604.18235] — First quantitative analysis of GRPO's *negative-advantage* pathology in deep-search: correct intermediate steps get uniformly penalized when the final answer is wrong. Fixes it with **prefix-shared weighting** + natural-language guardrail. +4.7pp F1 on multi-hop QA.
- **LVLM RL Theory (TA-MDP)** [2604.19857] — Rethinks Visual-ARFT convergence. Introduces Tool-Augmented MDP formalism, proves the three-component verifiable reward (format/accuracy/executability) is potential-decomposable and that GRPO convergence is bottlenecked by the slowest component; OOD generalization bounded by tool-call distribution coverage entropy.
- **OLLM** [2604.19087] — Options-based LLM inserts a 2-layer latent "plug-in" before the output head, modeling variation via discrete options. RL no longer needs a KL penalty because exploration is structurally constrained by the latent space.

### Post-GRPO Differentiation (April 23)
The "critic vs. critic-free" debate is collapsing into a unified lens: EVPO treats the two as a continuum with a data-driven switching rule; CalibAdv focuses on the *direction* of the gradient rather than its magnitude; TA-MDP gives the theoretical ceiling for multi-component verifiable rewards. OLLM meanwhile argues the entire RL objective should re-architect the underlying sampling space rather than patch the policy gradient.

## April 24, 2026 additions

- **GRPO-VPS** [2604.20659] — Step-level advantage shaping from the policy's own confidence in the verifiable answer. Refines GRPO credit assignment without breaking its critic-free simplicity.
- **polyGRPO** [2604.21593] — Adds *language* as a discrete exploration axis inside GRPO groups. Most other GRPO variants explore over decoding noise; polyGRPO exploits the latent-variable view of language to widen exploration cheaply.
- **GRAO (inside TPGO)** [2604.20714] — First extension of group-relative advantage to the *agent / tool / workflow node* level of multi-agent systems. Makes the optimizer itself a learnable function of historical edit-evaluation trajectories.
- **Reward-Balancing RL** [2604.20433] — Recasts iterative reward normalization as an optimal-control problem; offers tools for stability/convergence analysis that can inform KL-regularized PG and shaping-based LLM RL methods.

### Cross-links
- GRPO-VPS and polyGRPO represent the two dominant vectors of GRPO evolution this week: *depth of credit assignment* (step-level supervision) and *breadth of exploration* (cross-language probing).
- GRAO extends the GRPO family vertically (token → response → agent-module); combined with TEPO (token-level) and StepPO (step-level), the field now has group-relative advantage at nearly every granularity.

## April 26, 2026 additions

- **OP-GRPO** [2604.04142] — *First off-policy GRPO for flow-matching models.* Three pieces: (i) actively select high-quality trajectories into a replay buffer; (ii) sequence-level importance-sampling correction to mitigate distribution shift; (iii) *truncate trajectories at late denoising steps* because their off-policy ratios are theoretically and empirically ill-conditioned. Achieves Flow-GRPO performance with only 34.2% of training steps on image and video generation benchmarks. Most direct port of "LLM RL acceleration tricks" (off-policy + replay + IS) into the diffusion / flow-matching family.

### Cross-links
- **OP-GRPO ↔ Freshness-Aware PER (2604.16918)** — both replay-based accelerations for online policy gradient, but on different model classes (flow vs. autoregressive LM). Replay design (priority, freshness, IS correction) is converging across modalities.
- **OP-GRPO ↔ MAR-GRPO (2604.06966)** — within image generation, the GRPO family is now also forking into hybrid AR-diffusion specialists; off-policy and architecture-aware variants will likely combine.
