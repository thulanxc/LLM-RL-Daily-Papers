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

## Key Trend
Multimodal RL is maturing from "apply text RL to vision-language models" to addressing modality-specific challenges (visual forgetting, grounding faithfulness). Relax's omni-modal support suggests the infrastructure is catching up with the algorithms.
