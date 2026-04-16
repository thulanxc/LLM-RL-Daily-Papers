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

## Cross-Cutting Themes (April 2026)

1. **Credit Assignment is the central challenge**: SKPO, TEPO, SPPO, GenAC, and the survey (2604.09459) all focus on better credit assignment — at token, step, sequence, and trajectory levels.

2. **RLVR is expanding**: From math/code to general reasoning (SUPERNOVA), negotiation, and multimodal tasks. The "imperfect verifier" result lowers barriers further.

3. **Efficiency is non-negotiable**: Every major contribution now includes efficiency considerations — replay buffers (40% savings), trajectory extrapolation (37.5%), multi-response scoring (4x), and async training (2x).

4. **Agentic RL is producing superhuman results**: GrandCode and RefineRL show that RL-trained agents can dramatically exceed their base model capabilities.

5. **Self-improvement loops are maturing**: SD-Zero, Self-Distilled RLVR, MISE, and GenAC all involve the model providing its own training signal in some form.

---

*Last updated: April 16, 2026*
