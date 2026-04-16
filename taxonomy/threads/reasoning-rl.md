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
