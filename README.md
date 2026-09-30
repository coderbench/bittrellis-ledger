# BitTrellis score records (hpc01-e5)

> Every evaluated pull request, the frontier it was ranked against, and the artifacts behind both.

## Which checkpoint to use

Every merged recipe trades a little of one thing for another. Pick by what you need; each change is against today's shipped checkpoint (V0).

![The trade-off each merged recipe makes: prompt speed against closeness to the original model, with peak GPU memory](tradeoffs.svg)

| Best for | Recipe | Closeness to the original (RP-KL) | Prompt reading, 4K | Peak GPU memory |
|---|---|---|---|---|
| **Closest to the original model · Fastest prompt reading · Least GPU memory** | `gdn-fp8-mlp-q4k-skip0`<br>#33 by @cleanjunc ![eval:L](https://img.shields.io/badge/eval%3AL-2da44e?style=flat-square) | **0.0853 · 37.2% closer** | **8,704 tok/s · 48% slower** | **22.82 GiB · 0.80 GiB more** |
| *for reference* | V0, today's shipped checkpoint | 0.1357 | 16,606 tok/s | 22.02 GiB |

Build one yourself (after `scripts/setup_models.sh` in [bittrellis](https://github.com/coderbench/bittrellis)):

```bash
bittrellis build manifests/gdn-fp8-mlp-q4k-skip0.yaml --out models/gdn-fp8-mlp-q4k-skip0
```

## Progress

![Frontier gain credited to merged pull requests over time, pull requests scored per day by outcome, and the authors with the most credited gain.](progress.svg)

## Every measured result

Written by the evaluator after each pass. Re-derive any score yourself:

```bash
bittrellis frontier hpc01-e5/accepted <your artifact>
```

| | Checkpoint | RP-KL ↓ | tasks ↑ | decode tok/s ↑ | prefill 4K tok/s ↑ | peak GPU GiB ↓ | holdout | FG-2 |
|---|---|---:|---:|---:|---:|---:|---|---:|
| ★ | gdn-fp8-mlp-q4k-skip0 | 0.0853 | 566/784 | 84.2 | 8,704 | 22.82 | PASS | 0.356% |
| ★ | V3-gdn-fp8 | 0.1024 | 573/784 | 84.0 | 13,725 | 23.93 | PASS | 0.057% |
| ★ | gdn-mlp-q4k-skip-layer0 | 0.1029 | 564/784 | 96.4 | 8,798 | 20.54 | PASS | 0.154% |
| ★ | gdn-fp8-qkv-all-zo-split | 0.1083 | 568/784 | 88.5 | 14,187 | 23.02 | PASS | 0.013% |
|   | gdn-state-fp8-skip0 | 0.1115 | 573/784 | 86.8 | 14,501 | 23.39 | PASS | 0.000% |
| ★ | gdn-attn-q4k-mlp-mid | 0.1136 | 566/784 | 96.2 | 10,821 | 21.06 | PASS | 0.026% |
| ★ | V1-all-q4k | 0.1142 | 575/784 | 96.3 | 8,441 | 20.25 | PASS | 0.042% |
| ★ | gdn-zo-deep-mlp-skip0 | 0.1178 | 563/784 | 96.3 | 9,209 | 20.81 | PASS | 0.000% |
| ★ | V9-gdn-q4k-mlp-q4k | 0.1179 | 562/784 | 96.4 | 8,742 | 20.41 | — | 0.000% |
| ★ | gdn-q4k-skip-layer0 | 0.1210 | 572/784 | 96.0 | 13,846 | 21.64 | PASS | 0.000% |
|   | gdn-q4k-deep | 0.1238 | 578/784 | 95.9 | 15,127 | 21.83 | FAIL | 0.000% |
| | ↳ *not credited: private holdout FAIL* | | | | | | | |
|   | V7-mlp-q4k-early | 0.1247 | 561/784 | 96.1 | 9,697 | 21.40 | — | 0.000% |
| ★ | mlp-q4k-skip-layer0 | 0.1249 | 563/784 | 96.5 | 9,802 | 20.91 | PASS | 0.000% |
|   | V13-mlp-unsloth-bytes | 0.1258 | 566/784 | 95.7 | 16,675 | 22.02 | FAIL | 0.000% |
| | ↳ *not credited: private holdout FAIL* | | | | | | | |
| ★ | gdn-mlp-deep-q4k | 0.1258 | 567/784 | 96.2 | 11,500 | 21.26 | PASS | 0.008% |
| ★ | V4-gdn-q4k | 0.1265 | 566/784 | 96.0 | 13,843 | 21.58 | PASS | 0.000% |
| ★ | V5-attn-q4k | 0.1282 | 556/784 | 95.5 | 15,628 | 21.85 | — | 0.036% |
| ★ | V6-mlp-q4k | 0.1294 | 563/784 | 96.6 | 9,758 | 20.84 | PASS | 0.000% |
| ★ | V0-baseline-rebuild | 0.1357 | 564/784 | 95.7 | 16,606 | 22.02 | — | 0.458% |

Epoch `hpc01-e5` · rules: [bittrellis](https://github.com/coderbench/bittrellis) ([specification](https://github.com/coderbench/bittrellis/blob/main/docs/specification.md)).

`results/` holds one record per evaluated pull-request head -- never rewritten, with any re-measurement published beside it as `.remeasured-N` -- `observations/` the first-seen record that decides who submitted a recipe first, and `accepted/` the artifacts of merged results. The private holdout never appears here: records carry PASS or FAIL only.
