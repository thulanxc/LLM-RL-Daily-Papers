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

## Key Trend
The field is converging on the credit assignment problem — how to distribute sequence-level reward signal to individual tokens/steps. SKPO, TEPO, SPPO, and GenAC each address this differently.
