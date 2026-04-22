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

## April 19, 2026 Additions

### Production-Scale Multi-Agent RL Pipelines
- **MindDR (Mind DeepResearch)** [2604.14518] — First fully-disclosed 30B-scale three-agent deep research system (Planning / DeepSearch / Report) with four-stage training (SFT cold-start → Search-RL via GSPO → Report-RL via RACE rubric → Preference). GSPO elevates importance ratio from token to sequence level for MoE. Matches much larger models on BrowseComp / WideSearch / xbench-DS / DeepResearch Bench.
- **MARS² (Multi-Agent Reinforced Tree-Search)** [2604.14564] — Extends group-relative advantage to multi-agent RL on a shared search tree. Thompson-sampling over (agent, node) pairs; tree-consistent reward shaping across parent/sibling nodes. First clean credit-assignment framework for structured multi-agent search.
- **TREX (Agent-Driven Fine-Tuning Automation)** [2604.14116] — Dual-agent (Researcher + Executor) system automates the entire LLM fine-tuning life cycle; models multi-round experiments as a search tree. Releases FT-Bench with 10 real-world tasks. Agent ops the RL loop itself.

### Step-Level Process Signals in GRPO
- **IG-Search (Information Gain Rewards)** [2604.15148] — Information-gain between real retrieval and random-retrieval counterfactual on gold-answer log-prob becomes per-step reward. Training-free. Plugged into GRPO per-token advantage for search queries. +1.6 EM over best trajectory-level baseline.
- **CW-GRPO (Contribution-Weighted GRPO)** [2604.14267] — LLM judge scores per-round contribution; outcome advantage is rescaled (not replaced) by contribution. Complementary to IG-Search: per-round amplitude vs. per-token distribution.

### Broadening Agentic RL Domains
- **RadAgent (3D Chest CT Tool Agent)** [2604.15231] — End-to-end RL for 3D medical image interpretation with domain toolbox. +6.0 macro-F1 over CT-Chat, +37.0% faithfulness.
- **RaTA-Tool (DPO for Multimodal Tool Retrieval)** [2604.14951] — Open-world tool selection as retrieval (not classification), aligned via DPO on task-description → tool matching. First HuggingFace-card-based open-world multimodal tool dataset.
- **APEX-MEM (Temporal Graph Memory Agent)** [2604.14362] — Property graph + append-only storage + multi-tool retrieval agent. 88.88% LOCOMO QA / 86.2% LongMemEval.

### Agentic Infrastructure
- **Scepsy (Aggregate LLM Pipeline)** [2604.15186] — Multi-LLM agentic workflow scheduling system. Profiles each LLM under different parallelism, builds Aggregate-LLM-Pipeline predictor for GPU allocation. 2.4× throughput / 27× latency improvement. Relevant to RL rollout clusters.
- **IE-as-Cache (Information Extraction as Cognitive Cache)** [2604.14930] — Repurposes IE as reusable working memory for agent reasoning, combining query-driven extraction with cache-aware reasoning.

## Updated Key Trend (April 19)

The five pillars are now augmented by a **sixth**:
6. **Full-stack industrialization**: RL pipelines (MindDR four-stage, MARS² tree-agents), the training loop itself (TREX), and rollout infrastructure (Scepsy) are all being standardized into deployable systems. At the same time, agentic RL is crossing modality/domain boundaries (RadAgent 3D medical, RaTA-Tool multimodal retrieval, APEX-MEM temporal memory) with increasing speed — the inner algorithmic core (GRPO + structured advantages + step-level process signals) now stabilizes enough for teams to focus on delivery.

## April 20, 2026 Additions

### Runtime-Alignment for Agents (new sub-thread)
- **PolicyBank** [2604.15505] — Memory mechanism that iteratively refines natural-language *policy* understanding via corrective feedback in pre-deployment testing; treats policy as an evolving object, not ground truth. Closes 82% of the human-oracle gap on policy-gap scenarios where existing agent memory achieves near-zero success. First practical recipe for runtime alignment.

### Agent Safety via Reasoning-Based Guards
- **WebAgentGuard** [2604.12284] — GRPO-trained Guard model detects prompt-injection attacks on web agents by *reasoning* about actions rather than pattern-matching. Extends the 4-17 "reasoning judge" thread into agent defense.

### Agent Industrial-Workflow Diagnostics
- **Agentic Hardware Verification** [2604.15657] — First token-budget "accounting" study of LLM-agent hardware verification. Six-category token tracking; taxonomy of coverage holes (methodology-bound ceilings vs reasoning frontiers). Enhanced domain-specialized agents reach 95-99% coverage with 4-13× fewer tokens. Mechanistic explanation for Frontier-Eng's "optimization degradation".

### Agent-as-Behavioral-Simulator (crossing into applications)
- **MUSE** [2604.13828] — Multi-domain Chinese user simulation via IPSE + Role-Reversal SFT + Rubric-Guided Multi-Turn RL. First systematic Chinese simulator for dialogue AI training.
- **PGHS** [2604.15190] — Meituan merchant diagnosis via policy-mining layer unifying LLM reasoning + ML fitting. 8.80% group error, 45.8%/40.9% over strongest single-paradigm baselines.

### Updated Pillar
7. **Runtime alignment**: Alignment becomes a continuous in-deployment process. PolicyBank + WebAgentGuard + Grift (reward-hacking detector) together make the "trained and shipped" model no longer the end state — safety must be refreshed via ongoing feedback, reasoning judges, and model-internal probes.

## Morning Edition (April 21) — Agentic RL 新增

- **CoEvolve** [2604.15840] — Closes the agent-data loop: rollout failure patterns (forgetting + uncertainty signals) drive LLM-based task synthesis; synthesized tasks are validated via environment interaction and added to the training distribution. **+19.43%** / **+15.58%** / **+18.14%** gains on Qwen2.5-7B / Qwen3-4B / Qwen3-30B-A3B (AppWorld & BFCL).
- **AutoSearch** [2604.17337] — Defines "minimal-sufficient search depth" (jointly determined by question complexity and agent capability) and uses it as the RL reward signal for agentic RAG: rewards reaching this depth, penalizes over-searching. Reduces search-step count while maintaining accuracy on multi-hop QA.
- **ClawEnvKit** [2604.18543] — End-to-end automatic environment generator (parser / generator / validator) for claw-like agents. Auto-ClawEval delivers 1,040 environments across 24 categories at **1/13,800** the cost of human construction. Harness engineering yields up to +15.7pp over bare ReAct.
- **π-Play** [2604.14054] — Data-free multi-agent self-play via privileged self-distillation: a teacher observing both agents' internal states distills dense supervision to a student that sees only the visible interaction. Works on both cooperative and competitive tasks.
- **LAnR** [2604.17866] — Latent Abstraction for Retrieval: replaces text-based search queries with dense vectors generated from `[PRED]` hidden states; encode / retrieve / generate are all performed within the LLM's own latent space. Removes an entire external component from the agent loop.
- **MT-GRPO** [2604.02869] — First multi-turn GRPO (combined with GTPO) on real customer-service tool-calling tasks, with *Iterative Reward Calibration* progressively refining intermediate rewards across training rounds.

### Connections
- CoEvolve ↔ RAGEN-2 (2604.06268): RAGEN-2 diagnosed "Template Collapse" via mutual information; CoEvolve operationalizes the fix via failure-pattern-driven data synthesis.
- ClawEnvKit ↔ CoEvolve: orthogonal automation — one generates tasks, the other generates environments. Combined → end-to-end automated agentic-RL training factory.
- AutoSearch ↔ GUARD (2604.14528): GUARD controls branching at failure points; AutoSearch controls *depth*. Both are instances of "RL-trained resource allocation."
- LAnR ↔ Latent CoT (2604.15726): both push the "surface text → latent state" migration — LAnR extends it to retrieval.
- MT-GRPO ↔ CW-GRPO (2604.14267): two ways to make GRPO multi-turn — MT-GRPO iteratively calibrates reward; CW-GRPO rescales advantages with per-round LLM-judge contributions.
- π-Play ↔ MARS² (2604.14564): two multi-agent RL paradigms — MARS² shares search tree; π-Play shares privileged knowledge via distillation.

## April 22, 2026 additions

- **StepPO** [2604.18401] — Step-level MDP for agentic RL (see policy-optimization thread for detail).
- **Self-Evolution via World Knowledge** [2604.18131] — Trains agents with outcome-based reward on "how much self-distilled world knowledge improves downstream task success". Reward only in training phase; deployment is spontaneous and reward-free. A path to "meta-evolution" agents.
- **Freshness-Aware PER** [2604.16918] — First successful Prioritized Experience Replay for LLM/VLM RL. Adds multiplicative exponential age decay to any PER priority (grounded in effective sample size). Dramatic gains: +46% NQ Search, +367% Sokoban, +133% VLM FrozenLake. Standard PER without decay consistently degrades performance.
- **RTMC** [2604.11037] — Rollout-Tree Monte Carlo step-level credit assignment (see policy-optimization thread).
- **ProCeedRL** [2604.02006] — Process Critic + Exploratory Demonstration RL. Addresses the "error accumulation in misleading contexts" failure mode in multi-turn agents. Shifts exploration from passive selection to active intervention.
- **Latent Preference Tool Calling** [2604.17886] — Cross-session personalized tool calling. PRefine uses generate-verify-refine loop; achieves tool-call accuracy with only 1.24% of full-history prompting tokens. Introduces MPT benchmark (265 multi-session dialogues).
- **MAGEO** [2604.19516] — Multi-agent framework for Generative Engine Optimization with reusable strategy library. Planner/editor/fidelity evaluator collaborate; validated edits are progressively distilled into engine-specific skills. ACL 2026 Findings.

### Key Trend (April 22): Experience Becomes a First-Class Citizen

Three papers this week treat "experience" or "knowledge" as the central training asset:
- **Freshness-Aware PER**: manages replay-buffer priorities with age decay
- **Self-Evolution Agents**: distills self-generated world knowledge
- **MAGEO**: accumulates reusable editing strategies as a "skill library"

This marks a shift from per-episode optimization to **cross-episode experience management** — closer to how humans learn.
