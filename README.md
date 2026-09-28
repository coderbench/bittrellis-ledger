# BitTrellis score records (hpc01-e5)

> Every evaluated pull request, the frontier it was ranked against, and the artifacts behind both.

## Progress

![Frontier gain credited to merged pull requests over time, pull requests scored per day by outcome, and the authors with the most credited gain.](progress.svg)

## Every measured result

Written by the evaluator after each pass. Re-derive any score yourself:

```bash
bittrellis frontier hpc01-e5/accepted <your artifact>
```

| | Checkpoint | RP-KL ↓ | tasks ↑ | decode tok/s ↑ | prefill 4K tok/s ↑ | peak GPU GiB ↓ | holdout | FG-2 |
|---|---|---:|---:|---:|---:|---:|---|---:|
| ★ | V3-gdn-fp8 | 0.1024 | 573/784 | 84.0 | 13,764 | 23.93 | PASS | 0.102% |
| ★ | gdn-mlp-q4k-skip-layer0 | 0.1029 | 564/784 | 96.4 | 8,811 | 20.54 | PASS | 0.208% |
| ★ | gdn-state-fp8-skip0 | 0.1115 | 573/784 | 86.8 | 14,525 | 23.39 | PASS | 0.031% |
| ★ | V1-all-q4k | 0.1142 | 575/784 | 96.4 | 8,480 | 20.25 | PASS | 0.043% |
| ★ | gdn-zo-deep-mlp-skip0 | 0.1178 | 563/784 | 96.3 | 9,243 | 20.81 | PASS | 0.001% |
|   | V9-gdn-q4k-mlp-q4k | 0.1179 | 562/784 | 96.4 | 8,740 | 20.41 | — | 0.000% |
| ★ | gdn-q4k-skip-layer0 | 0.1210 | 572/784 | 96.0 | 13,885 | 21.64 | PASS | 0.000% |
|   | gdn-q4k-deep | 0.1238 | 578/784 | 95.9 | 15,158 | 21.95 | FAIL | 0.000% |
| | ↳ *not credited: private holdout FAIL* | | | | | | | |
|   | V7-mlp-q4k-early | 0.1247 | 561/784 | 96.2 | 9,753 | 21.40 | — | 0.000% |
| ★ | mlp-q4k-skip-layer0 | 0.1249 | 563/784 | 96.5 | 9,806 | 20.91 | PASS | 0.000% |
|   | V13-mlp-unsloth-bytes | 0.1258 | 566/784 | 95.7 | 16,734 | 22.02 | FAIL | 0.000% |
| | ↳ *not credited: private holdout FAIL* | | | | | | | |
| ★ | gdn-mlp-deep-q4k | 0.1258 | 567/784 | 96.2 | 11,490 | 21.26 | PASS | 0.031% |
| ★ | V4-gdn-q4k | 0.1265 | 566/784 | 96.0 | 13,865 | 21.58 | PASS | 0.000% |
| ★ | V5-attn-q4k | 0.1282 | 556/784 | 95.5 | 15,685 | 21.85 | — | 0.038% |
| ★ | V6-mlp-q4k | 0.1294 | 563/784 | 96.6 | 9,742 | 20.84 | PASS | 0.000% |
| ★ | V0-baseline-rebuild | 0.1357 | 564/784 | 95.8 | 16,932 | 22.02 | — | 0.707% |

Epoch `hpc01-e5` · rules: [bittrellis](https://github.com/coderbench/bittrellis) ([specification](https://github.com/coderbench/bittrellis/blob/main/docs/specification.md)).

`results/` holds one record per evaluated pull-request head -- never rewritten, with any re-measurement published beside it as `.remeasured-N` -- `observations/` the first-seen record that decides who submitted a recipe first, and `accepted/` the artifacts of merged results. The private holdout never appears here: records carry PASS or FAIL only.
