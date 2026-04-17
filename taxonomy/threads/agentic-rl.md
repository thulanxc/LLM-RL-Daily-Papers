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

## Night Edition (April 16, late-night) Additions

### TIR Trust, Efficiency & Experience (new sub-thread)
- **E³-TIR** [2604.09455] — Warm-up paradigm fusing three experience types (Expert Prefix / Expert Guided / Self-Exploration); +6% across 3B–8B. Middle path between Zero-RL and SFT-then-RL.
- **ATTC (When to Trust Tools)** [2604.08281] — First framework to train *tool trust calibration*: model explicitly decides accept / reject / recompute when reasoning and tool conflict. Trust-consistent reward in GRPO.
- **PTE — Beyond Accuracy** [2604.05404] — Hardware-aware TIR efficiency metric. Reveals KV-Cache eviction and long-tool-response as major costs. Higher PTE ↔ lower correctness — more tool calls ≠ better answers.

### Self-Supervision & Memory Agents
- **Self-Guide** [2604.03098] — Co-evolution of policy and internal reward; interleaved self-guidance and action steps serve both inference-time guidance and training-time dense supervision.
- **MIA (Memory Intelligence Agent)** [2604.04503] — Manager-Planner-Executor architecture + alternating RL. Parametric ↔ non-parametric memory cycle enables test-time learning.

### Multi-Agent Language RL
- **LangMARL** [2604.00722] — First to implement MARL entirely in natural language: language critic, language gradient estimator, language optimizer. CTDE paradigm for LLM agents.

### Engineering Agent Benchmarks
- **Frontier-Eng** [2604.12290] — 47 real engineering tasks with continuous rewards + hard constraints. Reveals "optimization degradation" in frontier models (Claude 4.6 Opus best).
- **SandMLE** [2604.04872] — Synthetic micro-MLE sandboxes (50–200 samples, ≤15s execution); 13× speedup enables trajectory-level on-policy RL for MLE agents for the first time.

### Medical / Domain Deep Search
- **QuarkMedSearch** [2604.12867] — SFT short→long + RLVR with strict anti-hacking reward for Chinese medical deep search.

## Updated Key Trend (post-Night Edition)

Agentic RL has now split into four parallel research programs:
1. **Capability amplification** (RefineRL, GrandCode — pre-April-16)
2. **Diagnostic observability** (RAGEN-2, Skill-SD — late edition)
3. **Trust & efficiency** (E³-TIR, ATTC, PTE — night edition)
4. **Environment & benchmark** (Frontier-Eng, SandMLE — night edition)

The field is maturing along the exact axes that distributed systems did: build → observe → optimize → benchmark.

## April 17, 2026 Additions

### Decoupled Multi-Objective Policy Optimization
- **ToolOmni / DMO-GRPO** [2604.13787] — First to decouple retrieval vs execution advantages within a single GRPO pipeline. Prevents sub-task gradient interference. NDCG@5 +4.5%, SoPR 52.5%.

### Action-Trajectory Diagnostics
- **Exploration-Exploitation Errors Are Measurable** [2604.13151] — Policy-agnostic quantification of "didn't try" vs "blindly tried" using action sequences alone. Reveals distinct failure modes per frontier model; reasoning models improve both axes.

### Multi-Turn Baseline Repair
- **SPO (MM-Doc-R1)** [2604.13579] — Similarity-weighted per-state baselines replace GRPO's shared-initial-state baseline in multi-turn. Drop-in fix for the most widely deployed multi-turn GRPO setting.

## Updated Key Trend (April 17)

Four pillars are now joined by a **fifth**:
5. **Objective decomposition**: Single-scalar rewards are the Agentic RL bottleneck. ToolOmni (retrieval ⊥ execution) + the Exploration-Exploitation-Errors framework suggest the next generation of agentic RL algorithms will treat credit assignment as multi-dimensional by default.
