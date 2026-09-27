# BitTrellis score records (hpc01-e3)

> Every evaluated pull request, the frontier it was ranked against, and the artifacts behind both.

## Which checkpoint to use

Every merged recipe trades a little of one thing for another. Pick by what you need; each change is against today's shipped checkpoint (V0).

![The trade-off each merged recipe makes: prompt speed against closeness to the original model, with peak GPU memory](tradeoffs.svg)

| Best for | Recipe | Closeness to the original (RP-KL) | Prompt reading, 4K | Peak GPU memory |
|---|---|---|---|---|
| **Closest to the original model · Least GPU memory** | `gdn-zo-deep-mlp-skip0`<br>#8 by @dato-bitar ![eval:XS](https://img.shields.io/badge/eval%3AXS-c6efce?style=flat-square) | **0.1242 · 8.5% closer** | 9,114 tok/s · 38% slower | **20.81 GiB · 1.20 GiB less** |
| **Fastest prompt reading** | `gdn-q4k-deep`<br>#5 by @coderbench ![eval:M](https://img.shields.io/badge/eval%3AM-4ac26b?style=flat-square) | 0.1291 · 4.9% closer | **14,302 tok/s · 3% slower** | 21.83 GiB · 0.19 GiB less |
| *for reference* | V0, today's shipped checkpoint | 0.1357 | 14,760 tok/s | 22.02 GiB |

Build one yourself (after `scripts/setup_models.sh` in [bittrellis](https://github.com/coderbench/bittrellis)):

```bash
bittrellis build manifests/gdn-zo-deep-mlp-skip0.yaml --out models/gdn-zo-deep-mlp-skip0
bittrellis build manifests/gdn-q4k-deep.yaml --out models/gdn-q4k-deep
```

## Progress

![Frontier gain credited to merged pull requests over time, pull requests scored per day by outcome, and the authors with the most credited gain.](progress.svg)

## Every measured result

Written by the evaluator after each pass. Re-derive any score yourself:

```bash
bittrellis frontier hpc01-e3/accepted <your artifact>
```

| | Checkpoint | RP-KL ↓ | tasks ↑ | decode tok/s ↑ | prefill 4K tok/s ↑ | peak GPU GiB ↓ | holdout | FG-2 |
|---|---|---:|---:|---:|---:|---:|---|---:|
|   | V3-gdn-fp8 | 0.1128 | 573/784 | 83.0 | 11,848 | 23.93 | FAIL | 0.000% |
| | ↳ *not credited: private holdout FAIL* | | | | | | | |
|   | V3-gdn-fp8 | 0.1128 | 573/784 | 83.0 | 11,848 | 23.93 | FAIL | 0.000% |
| | ↳ *not credited: private holdout FAIL* | | | | | | | |
|   | V13-mlp-unsloth-bytes | 0.1201 | 566/784 | 94.4 | 14,110 | 22.02 | FAIL | 0.000% |
| | ↳ *not credited: private holdout FAIL* | | | | | | | |
|   | V13-mlp-unsloth-bytes | 0.1201 | 566/784 | 94.4 | 14,110 | 22.02 | FAIL | 0.000% |
| | ↳ *not credited: private holdout FAIL* | | | | | | | |
| ★ | V1-all-q4k | 0.1242 | 575/784 | 94.8 | 7,537 | 20.25 | PASS | 0.000% |
| ★ | V1-all-q4k | 0.1242 | 575/784 | 94.8 | 7,537 | 20.25 | PASS | 0.000% |
| ★ | gdn-zo-deep-mlp-skip0 | 0.1242 | 563/784 | 96.1 | 9,114 | 20.81 | PASS | 0.025% |
|   | V9-gdn-q4k-mlp-q4k | 0.1277 | 562/784 | 94.0 | 7,560 | 20.41 | — | 0.000% |
|   | V9-gdn-q4k-mlp-q4k | 0.1277 | 562/784 | 94.0 | 7,560 | 20.41 | — | 0.000% |
|   | V7-mlp-q4k-early | 0.1284 | 561/784 | 94.3 | 8,199 | 21.40 | — | 0.000% |
|   | V7-mlp-q4k-early | 0.1284 | 561/784 | 94.3 | 8,199 | 21.40 | — | 0.000% |
| ★ | gdn-q4k-deep | 0.1291 | 578/784 | 94.9 | 14,302 | 21.83 | PASS | 0.072% |
| ★ | gdn-mlp-deep-q4k | 0.1300 | 567/784 | 96.1 | 11,320 | 21.26 | PASS | 0.024% |
| ★ | mlp-q4k-skip-layer0 | 0.1318 | 563/784 | 96.0 | 9,919 | 20.91 | PASS | 0.013% |
|   | V6-mlp-q4k | 0.1346 | 563/784 | 94.4 | 8,358 | 20.84 | PASS | 0.000% |
|   | V6-mlp-q4k | 0.1346 | 563/784 | 94.4 | 8,358 | 20.84 | PASS | 0.000% |
|   | V5-attn-q4k | 0.1356 | 556/784 | 94.6 | 13,571 | 21.85 | — | 0.000% |
| | ↳ *not credited: task guard overall: lost 33, gained 19 vs incumbent (p=0.0352 < 0.05)* | | | | | | | |
|   | V5-attn-q4k | 0.1356 | 556/784 | 94.6 | 13,571 | 21.85 | — | 0.000% |
| | ↳ *not credited: task guard overall: lost 33, gained 19 vs incumbent (p=0.0352 < 0.05)* | | | | | | | |
| ★ | V0-baseline-rebuild | 0.1357 | 570/784 | 94.9 | 14,760 | 22.02 | — | 0.000% |
| ★ | V0-baseline-rebuild | 0.1357 | 570/784 | 94.9 | 14,760 | 22.02 | — | 0.000% |
| ★ | gdn-q4k-skip-layer0 | 0.1367 | 572/784 | 95.9 | 13,592 | 21.64 | PASS | 0.009% |
|   | V4-gdn-q4k | 0.1424 | 566/784 | 94.9 | 12,011 | 21.58 | PASS | 0.000% |
|   | V4-gdn-q4k | 0.1424 | 566/784 | 94.9 | 12,011 | 21.58 | PASS | 0.000% |

Epoch `hpc01-e3` · rules: [bittrellis](https://github.com/coderbench/bittrellis) ([specification](https://github.com/coderbench/bittrellis/blob/main/docs/specification.md)).

`results/` holds one record per evaluated pull-request head -- never rewritten, with any re-measurement published beside it as `.remeasured-N` -- `observations/` the first-seen record that decides who submitted a recipe first, and `accepted/` the artifacts of merged results. The private holdout never appears here: records carry PASS or FAIL only.
