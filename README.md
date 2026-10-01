# BitTrellis score records (hpc01-e5)

> Every evaluated pull request, the frontier it was ranked against, and the artifacts behind both.

## Which checkpoint to use

Every merged recipe trades a little of one thing for another. Pick by what you need; each change is against today's shipped checkpoint (V0).

![The trade-off each merged recipe makes: prompt speed against closeness to the original model, with peak GPU memory](tradeoffs.svg)

| Best for | Recipe | Closeness to the original (RP-KL) | Prompt reading, 4K | Peak GPU memory |
|---|---|---|---|---|
| **Closest to the original model** | `gdn-fp8-mlp-q4k-zo-deep-q4k`<br>#40 by @milosde111 ![eval:S](https://img.shields.io/badge/eval%3AS-8ddb8c?style=flat-square) | **0.0850 · 37.4% closer** | 8,736 tok/s · 47% slower | 22.16 GiB · 0.15 GiB more |
| **Fastest prompt reading** | `gdn-fp8-lmhead-q4k`<br>#38 by @carlo171112 ![eval:S](https://img.shields.io/badge/eval%3AS-8ddb8c?style=flat-square) | 0.0967 · 28.7% closer | **13,307 tok/s · 20% slower** | 23.93 GiB · 1.91 GiB more |
| **Least GPU memory** | `gdn-attn-q4k-mlp-early8-mid24-skip0`<br>#37 by @dato-bitar ![eval:XS](https://img.shields.io/badge/eval%3AXS-c6efce?style=flat-square) | 0.1091 · 19.6% closer | 10,272 tok/s · 38% slower | **20.92 GiB · 1.09 GiB less** |
| *for reference* | V0, today's shipped checkpoint | 0.1357 | 16,561 tok/s | 22.02 GiB |

Build one yourself (after `scripts/setup_models.sh` in [bittrellis](https://github.com/coderbench/bittrellis)):

```bash
bittrellis build manifests/gdn-fp8-mlp-q4k-zo-deep-q4k.yaml --out models/gdn-fp8-mlp-q4k-zo-deep-q4k
bittrellis build manifests/gdn-fp8-lmhead-q4k.yaml --out models/gdn-fp8-lmhead-q4k
bittrellis build manifests/gdn-attn-q4k-mlp-early8-mid24-skip0.yaml --out models/gdn-attn-q4k-mlp-early8-mid24-skip0
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
| ★ | gdn-fp8-mlp-q4k-zo-deep-q4k | 0.0850 | 568/784 | 87.1 | 8,736 | 22.16 | PASS | 0.059% |
|   | gdn-fp8-mlp-q4k-skip0 | 0.0853 | 566/784 | 84.2 | 8,711 | 22.82 | PASS | 0.000% |
| ★ | gdn-fp8-lmhead-q4k | 0.0967 | 576/784 | 83.9 | 13,307 | 23.93 | PASS | 0.047% |
|   | V3-gdn-fp8 | 0.1024 | 573/784 | 84.0 | 13,726 | 24.05 | PASS | 0.000% |
| ★ | gdn-mlp-q4k-skip-layer0 | 0.1029 | 564/784 | 96.4 | 8,832 | 20.54 | PASS | 0.069% |
| ★ | gdn-fp8-qkv-all-zo-split | 0.1083 | 568/784 | 88.5 | 14,191 | 23.02 | PASS | 0.011% |
| ★ | gdn-attn-q4k-mlp-early8-mid24-skip0 | 0.1091 | 572/784 | 96.2 | 10,272 | 20.92 | PASS | 0.010% |
|   | gdn-state-fp8-skip0 | 0.1115 | 573/784 | 86.8 | 14,531 | 23.39 | PASS | 0.000% |
|   | gdn-attn-q4k-mlp-mid | 0.1136 | 566/784 | 96.2 | 10,835 | 21.18 | PASS | 0.000% |
| ★ | V1-all-q4k | 0.1142 | 575/784 | 96.3 | 8,433 | 20.25 | PASS | 0.042% |
| ★ | gdn-zo-deep-mlp-skip0 | 0.1178 | 563/784 | 96.3 | 9,229 | 20.81 | PASS | 0.000% |
| ★ | V9-gdn-q4k-mlp-q4k | 0.1179 | 562/784 | 96.5 | 8,728 | 20.41 | — | 0.000% |
| ★ | gdn-q4k-skip-layer0 | 0.1210 | 572/784 | 96.0 | 13,893 | 21.64 | PASS | 0.000% |
|   | gdn-q4k-deep | 0.1238 | 578/784 | 95.9 | 15,161 | 21.83 | FAIL | 0.000% |
| | ↳ *not credited: private holdout FAIL* | | | | | | | |
|   | V7-mlp-q4k-early | 0.1247 | 561/784 | 96.2 | 9,758 | 21.40 | — | 0.000% |
|   | mlp-q4k-skip-layer0 | 0.1249 | 563/784 | 96.6 | 9,833 | 20.91 | PASS | 0.000% |
|   | V13-mlp-unsloth-bytes | 0.1258 | 566/784 | 95.7 | 16,537 | 22.02 | FAIL | 0.000% |
| | ↳ *not credited: private holdout FAIL* | | | | | | | |
| ★ | gdn-mlp-deep-q4k | 0.1258 | 567/784 | 96.2 | 11,495 | 21.26 | PASS | 0.007% |
| ★ | V4-gdn-q4k | 0.1265 | 566/784 | 96.0 | 13,843 | 21.58 | PASS | 0.000% |
| ★ | V5-attn-q4k | 0.1282 | 556/784 | 95.5 | 15,649 | 21.85 | — | 0.036% |
|   | V6-mlp-q4k | 0.1294 | 563/784 | 96.6 | 9,786 | 20.84 | PASS | 0.000% |
| ★ | V0-baseline-rebuild | 0.1357 | 564/784 | 95.7 | 16,561 | 22.02 | — | 0.396% |

Epoch `hpc01-e5` · rules: [bittrellis](https://github.com/coderbench/bittrellis) ([specification](https://github.com/coderbench/bittrellis/blob/main/docs/specification.md)).

`results/` holds one record per evaluated pull-request head -- never rewritten, with any re-measurement published beside it as `.remeasured-N` -- `observations/` the first-seen record that decides who submitted a recipe first, and `accepted/` the artifacts of merged results. The private holdout never appears here: records carry PASS or FAIL only.
