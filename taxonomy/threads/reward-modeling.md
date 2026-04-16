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

## Key Trend
Two simultaneous movements: (1) making reward models much more efficient (multi-response, CPMI, E-GRM), and (2) making them more robust to hacking (SignCert-PO, robust optimization). These are complementary — efficiency without robustness leads to faster exploitation.
