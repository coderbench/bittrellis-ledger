# BitTrellis score records (hpc02-e1)

> Every evaluated pull request, the frontier it was ranked against, and the artifacts behind both.

## Progress

![Frontier gain credited to merged pull requests over time, pull requests scored per day by outcome, and the authors with the most credited gain.](progress.svg)

## Every measured result

Written by the evaluator after each pass. Re-derive any score yourself:

```bash
bittrellis --track HPC-02 frontier hpc02-e1/accepted <your artifact>
```

| | Checkpoint | RP-KL ↓ | tasks ↑ | decode tok/s ↑ | prefill 4K tok/s ↑ | peak GPU GiB ↓ | holdout | FG-2 |
|---|---|---:|---:|---:|---:|---:|---|---:|
| ★ | V3-exps-q5k-down-q6k | 0.0340 | 564/784 | 382.3 | 36,996 | 29.24 | PASS | 0.364% |
| ★ | V0-unsloth-ud | 0.0450 | 570/784 | 397.4 | 39,225 | 25.51 | — | 0.000% |
| ★ | V1-kq-rtn-udmap | 0.0460 | 563/784 | 397.4 | 39,333 | 25.51 | PASS | 0.000% |
| ★ | V2-all-q4k | 0.1207 | 573/784 | 466.3 | 40,265 | 23.25 | PASS | 9.513% |

Epoch `hpc02-e1` · rules: [bittrellis](https://github.com/coderbench/bittrellis) ([specification](https://github.com/coderbench/bittrellis/blob/main/docs/specification.md)).

`results/` holds one record per evaluated pull-request head -- never rewritten, with any re-measurement published beside it as `.remeasured-N` -- `observations/` the first-seen record that decides who submitted a recipe first, and `accepted/` the artifacts of merged results. The private holdout never appears here: records carry PASS or FAIL only.
