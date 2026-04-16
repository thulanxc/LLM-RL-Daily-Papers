# Agentic RL

## Evolution
Single-Turn RLHF (2022) → Tool Use RL (2024) → Multi-Turn Agent RL (2025) → Superhuman Agents (2026)

## Core Idea
Train LLM agents for multi-step, tool-using, environment-interacting tasks using RL. Key challenges: credit assignment over long horizons, sparse/delayed rewards, partial observability.

## Recent (April 2026)
- **GrandCode** — First AI to beat all humans in live Codeforces. Agentic GRPO for multi-stage rollouts. [2604.02721]
- **RefineRL** — Skeptical-Agent for competitive programming. 4B models outperform 32B. [2604.00790]
- **HiExp** — Hierarchical experience for strategic exploration in search agents. [2604.08124]
- **SEARL** — Joint policy + Tool Graph Memory optimization. ACL 2026. [2604.07791]
- **Negotiation RLVR** — Four-phase strategic evolution in LLM negotiation. [2604.09855]
- **LangMARL** — Natural language multi-agent RL. [2604.00722]
- **Agent Q-Mix** — MARL for LLM multi-agent topology selection. [2604.00344]
- **AgentGL** — Agentic graph learning with RL. [2604.05846]

## Late Edition (April 16 PM) Additions

### Diagnosis
- **RAGEN-2** [2604.06268] — First to name "Template Collapse" (entropy-invisible failure). Mutual Information > entropy as reasoning quality proxy. SNR-Aware Filtering uses reward variance.

### Self-Supervision
- **Skill-SD** [2604.10674] — Trajectories → natural-language skills → teacher-only privileged info. Resolves OPSD+RL collapse.

### Tool-Use Environments
- **ToolCAD** [2604.07960] — LLM tool agent for text-to-CAD; interactive CAD gym + online curriculum RL.
- **AnomalyAgent** [2604.07900] — 5-tool closed-loop industrial anomaly synthesis; task + reflection + behavior rewards.
- **COVERT** [2604.09813] — Oracle-preserving augmentation for RL-ready tool-use data synthesis.

### Multi-Hop KG / Graph Agents
- **AgentGL** [2604.05846] — Graph-conditioned curriculum RL for Agentic Graph Learning.
- **KG-Reasoner** [2604.12487] — Integrates multi-hop KG traversal into unified "thinking" phase via RL.
- **TRACE** [2604.11193] — Narrative + experience-prior driven multi-hop KGQA.

### Multi-Agent Boundary Testing
- **OOM-RL** [2604.11477] — Capital loss as un-hackable gradient; STDAW workflow; Sharpe 2.06 over 20 months.
- **Trust Boundary MARL** [2604.05483] — Bias-Diffusion + MARL to detect black-box LLM untrustworthy regions.

## Key Trend
Agentic RL is producing the most dramatic capability amplifications. RefineRL shows 4B→32B-equivalent performance, and GrandCode beats legendary grandmasters. The key enabler: treating complex tasks as multi-turn agent problems rather than single-shot generation.

The **April 16 PM** update adds a new research dimension: **diagnostic observability**. RAGEN-2's Template Collapse framework, and Skill-SD's self-generated skills, together signal that the field is moving from "make it work" to "know why it works" — a maturity shift comparable to observability's role in distributed systems.
