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
