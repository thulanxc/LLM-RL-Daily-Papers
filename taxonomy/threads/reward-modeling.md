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
