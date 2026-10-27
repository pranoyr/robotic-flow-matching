# robotic-flow-matching

An implementation of **∆-flow** from *∆ Flow Matching for Robot Foundation Models*
(Zuo, An, et al., MARS Lab, Nanyang Technological University).

## Idea

Robot foundation models use flow matching to generate the future. Vision-language-action models
(VLAs) generate action chunks, and world-action models (WAMs) also generate future visual states.
Standard flow matching starts every sample from a fixed Gaussian prior, even though future actions
and states are usually close to recent ones.

∆-flow builds the **source distribution from recent history plus mild noise** instead of from
`N(0, I)`. Because the source starts close to the target, the model only has to learn a small
residual ∆. As a result:

- training converges faster (e.g. ImageWAM reaches 90% on LIBERO in 1 epoch instead of 6)
- **single-step inference** works (1.54× / 2.49× / 4.45× speedups on π0.5 / ImageWAM / Fast-WAM)
- actions stay smooth (4.5× lower jerk than one-step Gaussian sampling)
- action-history sources can replace the Gaussian source in pretrained WAMs at inference, without retraining

## Status

Work in progress.

## Setup

```bash
uv sync
uv run main.py
```
