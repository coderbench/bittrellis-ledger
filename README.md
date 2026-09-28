# BitTrellis score records (hpc01-e4)

> Every evaluated pull request, the frontier it was ranked against, and the artifacts behind both.

## Progress

![Frontier gain credited to merged pull requests over time, pull requests scored per day by outcome, and the authors with the most credited gain.](progress.svg)

## Every measured result

Written by the evaluator after each pass. Re-derive any score yourself:

```bash
bittrellis frontier hpc01-e4/accepted <your artifact>
```

| | Checkpoint | RP-KL ↓ | tasks ↑ | decode tok/s ↑ | prefill 4K tok/s ↑ | peak GPU GiB ↓ | holdout | FG-2 |
|---|---|---:|---:|---:|---:|---:|---|---:|
| ★ | V3-gdn-fp8 | 0.1024 | 573/784 | 83.0 | 11,848 | 23.93 | PASS | 0.349% |
| ★ | V1-all-q4k | 0.1142 | 575/784 | 94.8 | 7,537 | 20.25 | PASS | 0.064% |
| ★ | gdn-zo-deep-mlp-skip0 | 0.1178 | 563/784 | 96.1 | 9,114 | 20.81 | PASS | 0.008% |
|   | V9-gdn-q4k-mlp-q4k | 0.1179 | 562/784 | 94.0 | 7,560 | 20.41 | — | 0.000% |
| ★ | gdn-q4k-skip-layer0 | 0.1210 | 572/784 | 95.9 | 13,592 | 21.64 | PASS | 0.077% |
|   | gdn-q4k-deep | 0.1238 | 578/784 | 94.9 | 14,302 | 21.83 | FAIL | 0.000% |
| | ↳ *not credited: private holdout FAIL* | | | | | | | |
|   | V7-mlp-q4k-early | 0.1247 | 561/784 | 94.3 | 8,199 | 21.40 | — | 0.000% |
| ★ | mlp-q4k-skip-layer0 | 0.1249 | 563/784 | 96.0 | 9,919 | 20.91 | PASS | 0.014% |
|   | V13-mlp-unsloth-bytes | 0.1258 | 566/784 | 94.4 | 14,110 | 22.02 | FAIL | 0.000% |
| | ↳ *not credited: private holdout FAIL* | | | | | | | |
| ★ | gdn-mlp-deep-q4k | 0.1258 | 567/784 | 96.1 | 11,320 | 21.26 | PASS | 0.024% |
|   | V4-gdn-q4k | 0.1265 | 566/784 | 94.9 | 12,011 | 21.58 | PASS | 0.000% |
|   | V5-attn-q4k | 0.1282 | 556/784 | 94.6 | 13,571 | 21.85 | — | 0.000% |
|   | V6-mlp-q4k | 0.1294 | 563/784 | 94.4 | 8,358 | 20.84 | PASS | 0.000% |
| ★ | V0-baseline-rebuild | 0.1357 | 564/784 | 94.9 | 14,760 | 22.02 | — | 0.678% |

Epoch `hpc01-e4` · rules: [bittrellis](https://github.com/coderbench/bittrellis) ([specification](https://github.com/coderbench/bittrellis/blob/main/docs/specification.md)).

`results/` holds one record per evaluated pull-request head -- never rewritten, with any re-measurement published beside it as `.remeasured-N` -- `observations/` the first-seen record that decides who submitted a recipe first, and `accepted/` the artifacts of merged results. The private holdout never appears here: records carry PASS or FAIL only.
