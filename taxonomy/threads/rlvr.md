# RL with Verifiable Rewards (RLVR)

## Evolution
RLHF (2022) → Outcome-Based RL (2024) → DeepSeek-R1 (2025) → RLVR Expansion (2026)

## Core Idea
Instead of learning a reward model from human preferences, use verifiable signals (correct/incorrect answers, passing/failing tests) as reward. Simpler, more scalable, and avoids reward hacking.

## Foundational
- **DeepSeek-R1** (2025). Demonstrated that RLVR with GRPO can produce emergent chain-of-thought reasoning. [2501.12948]
- **DeepSeekMath** — Shao et al. (2024). GRPO with math verification rewards. [2402.03300]

## Recent (April 2026)
- **SUPERNOVA** — Extends RLVR to general reasoning via data curation framework. 52.8% improvement on BBEH. [2604.08477]
- **SD-Zero** — Self-revision converts binary rewards to dense supervision. Sample-efficient, no external teacher. [2604.12002]
- **Imperfect Verifiers** — RLVR robust to 15% verifier noise across 3 model families. [2604.07666]
- **Bidirectional Entropy** — Informative vs. spurious entropy decomposition in RLVR. [2604.04894]
- **Cog-DRIFT** — Cognitive reformulation turns hard problems into solvable variants. [2604.04767]
- **Self-Distilled RLVR** — Token-level self-distillation for update magnitude + RLVR for direction. [2604.03128]
- **PubSwap** — Federated RLVR with public-data off-policy coordination. [2604.12160]
- **NExt** — Low-rank trajectory extrapolation for RLVR acceleration (37.5% savings). [2604.11446]
- **Negotiation RLVR** — Verifiable rewards for strategic negotiation. [2604.09855]
- **PerMix-RLVR** — Preserving persona expressivity under RLVR training. [2604.08986]

## Night Edition (April 16, late-night) Additions — Vertical Expansion
- **QuarkMedSearch** [2604.12867] — SFT (short→long) + RLVR for Chinese medical long-horizon deep search; explicit anti-hacking reward design.
- **ReasonXL** [2604.12378] — SFT + **Dr. GRPO** recipe for multilingual reasoning (EN/DE/FR/IT/ES, 2M aligned samples per language). Representational analysis reveals language-identity "activation bottleneck" in early layers.
- **HintMR** [2604.12229] — Distillation of the *meta-skill* of generating & consuming step-level hints into small LMs.
- **MathAgent** [2604.11188] — Legislator-Executor adversarial constraint-graph evolution produces 1K synthesized samples outperforming LIMO / s1K.

## Key Trend
RLVR is expanding beyond math/code to general reasoning (SUPERNOVA), negotiation, multimodal tasks, medical deep search (QuarkMedSearch), multilingual reasoning (ReasonXL), content moderation (CARO via DPO), knowledge editing, and argumentation. The "imperfect verifier" result lowers the barrier for new domains. 

**Night-edition pattern**: Every new RLVR domain is adopting the same recipe template — *SFT (short-to-long or style-shift) → RLVR with domain-specific anti-hacking reward*. This is becoming the de facto playbook for vertical-domain RL.

## Morning Edition (April 21) — RLVR 新增

- **QuantumQA / VRM** [2604.18176] — Extends RLVR to scientific reasoning via *Verification-aware Reward Model* that adaptively fuses deterministic solver signals with multidimensional semantic evaluation. 8B model competitive with proprietary-scale systems.
- **KnowRL** [2604.12627] — Tackles RLVR zero-gradient collapse on hard problems via Constrained Subset Search over atomic knowledge points — provides just-enough guidance while preserving exploration.
- **Semantic Equivalence Self-Play** [2604.17010] — RLVR with *formal proof* as verifier: Liquid Haskell for equivalence, execution counterexamples for inequivalence. +13.3pp on EquiBench.
- **AtManRL** [2604.16158] — Adds a *faithfulness-based* verifiable signal (attention saliency) alongside outcome correctness to push CoT toward genuine causal use.

### Connections
- QuantumQA ↔ OOM-RL (market signal) ↔ MedVR (medical rubric): domain-specific executable verifiers continue to expand the RLVR applicability frontier.
- AtManRL introduces a new axis: verifiability-of-reasoning-*process*, not just answer.

## April 22, 2026 additions

- **MCPO** [2604.16972] — Fixes GRPO's mastered-prompt gradient collapse (see policy-optimization thread).
- **EA-RLVR** [2604.16881] — Entity-Anchored RLVR for cross-cultural entity translation. Anchors supervision on entity-level verifiable reward (not sequence similarity) + lightweight structural gates. Explicitly avoids external knowledge base dependency — relies on parametric knowledge already in pretraining.
- **Bilateral Trade LM** [2604.16472] — Training LMs for bilateral bargaining with private information. Event-driven simulator separates binding offers (tool calls) from natural-language messages for automated evaluation. Round-robin tournament (5 frontier models, 15,000 negotiations) reveals "price discrimination via sequential offers" as optimal strategy.
- **Abstain-R1** [2604.17073] — Clarification-aware RLVR (see alignment thread).
- **Plan-PRM** [2604.17957] — PDDL-verifiable step rewards for PRM training (see reward-modeling thread).

### Key Trend (April 22): RLVR Expands Beyond Math

Today's RLVR work covers:
- Cross-cultural translation (EA-RLVR)
- Game-theoretic negotiation (Bilateral Trade LM)
- Unanswerable-query detection (Abstain-R1)
- Non-math reasoning via PDDL planning (Plan-PRM)
- Calibrated abstention (Abstain-R1)

The verifiable-reward paradigm is proving portable — provided one can design a domain-appropriate verifier.

## April 24, 2026 additions

- **DDRL (Debiased-Denoised TTRL)** [2604.21327] — First clear failure-mode decomposition of *Test-Time RLVR*: ambiguity-region pseudo-labels × GRPO's group-relative advantage amplification produce "spurious signal amplification." Fix: frequency-based sampling + fixed (debiased) advantage. Robust across multiple math benchmarks.
- **GRPO-VPS** [2604.20659] — No-external-PRM process supervision for RLVR. Verifiable in the sense that the process signal is the *policy's own* conditional probability of the (verifiable) correct answer across segment boundaries. Extends the RLVR contract from outcome-only to step-wise while remaining fully outcome-verifiable at training time.
- **Weak-Supervision RLVR** [2604.18574] — When does RLVR still work if the reward is not perfectly verifiable? Three settings (scarce / noisy / self-supervised proxy). Key predictor: reasoning faithfulness pre-RL. Intervention: reasoning-trace SFT + domain CPT before RL.
- **Parallel-SFT** [2604.20835] — RLVR transfer across programming languages. Source-PL RL *hurts* target-PL performance unless SFT initialization contains parallel programs (same function in multiple PLs). Establishes the first cross-PL transferability result for code RLVR.

### Connections
- GRPO-VPS ↔ Plan-PRM (2604.17957) & IPVRM (2604.13197): three different stances on "where process signal comes from" — synthesized from planners, learned as prefix value, or read off the policy itself.
- DDRL ↔ TTRL (2504.16084): formally identifies the failure mode TTRL was silent about, and delivers a direct replacement for its advantage estimator.
- Weak-Supervision RLVR ↔ Imperfect Verifiers (2604.07666): complementary — Imperfect Verifiers tolerates 15% label noise, Weak-Supervision RLVR asks what pre-conditions let a model tolerate it.
- Parallel-SFT ↔ SUPERNOVA (2604.08477): both identify that *SFT shape* (instruction diversity / parallel programs) is decisive for RLVR transfer.
