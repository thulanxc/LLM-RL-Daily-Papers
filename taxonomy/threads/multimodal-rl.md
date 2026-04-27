# Multimodal RL

## Evolution
Text RLHF (2022) → Vision-Language RL (2025) → Omni-Modal RL (2026)

## Core Challenge
Extending RL training from text-only to multimodal inputs (image, video, audio). Key issues: visual forgetting during long reasoning, faithfulness of visual grounding, and infrastructure for heterogeneous data.

## Recent (April 2026)
- **OpenVLThinkerV2 / G2RPO** — Gaussian GRPO for multimodal reasoning. Non-linear distributional matching. [2604.08539]
- **VGPO** — Visual Attention Compensation for visual forgetting in VLMs. [2604.09349]
- **Faithful GRPO** — Constrained optimization for faithful visual reasoning. [2604.08476]
- **Relax** — Omni-modal RL engine supporting text + image + audio + video. [2604.11554]
- **MedVR** — Annotation-free medical visual reasoning via RL. [2604.08203]

## Night Edition (April 16, late-night) Additions
- **MedVR (deep-dive)** [2604.08203] — EVR (entropy-guided visual regrounding) + CCA (consensus-based credit assignment) enable *annotation-free* medical visual reasoning via agentic RL. Model-internal uncertainty triggers visual re-examination actions; rollout consensus substitutes for human step-level labels.
- **Saliency-R1** [2604.04500] — Zero-overhead saliency map (decomposing token logits into visual-token first-order contributions). Alignment with bbox annotations as GRPO reward. CVPR 2026.

## Key Trend
Multimodal RL is maturing along two complementary axes:
1. **Infrastructure (Relax)** catching up with algorithms.
2. **Internal-signal supervision** emerging — both MedVR (entropy + consensus) and Saliency-R1 (logit-decomposition saliency) derive training signal from *model-internal quantities*, not external human annotation. This is the multimodal analogue to Thread 8's "Agentic Self-Supervision".

## April 27, 2026 additions

- **Neuro-Symbolic VLM RL** [2604.22062, Georgia Tech] — Trains Qwen3-VL-2B-Instruct via GRPO to use a constrained **neuro-symbolic language (NSL)** instead of natural language or raw Python for math/science VLM reasoning. Token efficiency: **75% fewer tokens than SymPy**; +3.33% on a vision-language math/science/general benchmark. Stakes out a useful middle ground between verbal CoT (over-long) and pure symbolic execution (over-rigid).
- **LAT-Audio (Listening with Time)** [2604.22245] — RL meets long-form audio: dataset (LAT-Chronicle, 1.2k hours), benchmark (LAT-Bench, audio up to 30 min), model with a **Think-With-Audio CoT** that progressively zooms global→local via tool calls; final stage uses **GRPO** to refine reasoning quality. Surpasses prior LALMs on temporal awareness.
- **UDM-GRPO** [2604.18518] — Cross-listed from Policy Optimization: stabilizes GRPO on Uniform Discrete Diffusion. Brings GRPO to text-to-image generation with major SOTA jumps.

### Connection
The April 27 multimodal additions reinforce a broader observation: **GRPO is becoming a substrate that ports to any modality with a verifiable reward**. Image (UDM-GRPO), audio (LAT-Audio), VLM with symbolic reasoning (Neuro-Symbolic VLM) — the algorithm is the same; the reward design and action-space framing are where domain expertise lives.
