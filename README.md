# BitTrellis score records (hpc01-e3)

> Every evaluated pull request, the frontier it was ranked against, and the artifacts behind both.

Written by the evaluator after each pass. Re-derive any score yourself:

```bash
bittrellis frontier hpc01-e3/accepted <your artifact>
```

| | Checkpoint | RP-KL ↓ | tasks ↑ | decode tok/s ↑ | prefill 4K tok/s ↑ | peak GPU GiB ↓ | FG-2 |
|---|---|---:|---:|---:|---:|---:|---:|
|   | V3-gdn-fp8 | 0.1128 | 573/784 | 83.0 | 11,848 | 23.93 | 0.000% |
| ★ | V13-mlp-unsloth-bytes | 0.1201 | 566/784 | 94.4 | 14,110 | 22.02 | 0.304% |
| ★ | V1-all-q4k | 0.1242 | 575/784 | 94.8 | 7,537 | 20.25 | 0.040% |
|   | V9-gdn-q4k-mlp-q4k | 0.1277 | 562/784 | 94.0 | 7,560 | 20.41 | 0.000% |
|   | V7-mlp-q4k-early | 0.1284 | 561/784 | 94.3 | 8,199 | 21.40 | 0.000% |
| ★ | V6-mlp-q4k | 0.1346 | 563/784 | 94.4 | 8,358 | 20.84 | 0.024% |
|   | V5-attn-q4k | 0.1356 | 556/784 | 94.6 | 13,571 | 21.85 | 0.000% |
| ★ | V0-baseline-rebuild | 0.1357 | 570/784 | 94.9 | 14,760 | 22.02 | 0.193% |
| ★ | V4-gdn-q4k | 0.1424 | 566/784 | 94.9 | 12,011 | 21.58 | 0.100% |

Epoch `hpc01-e3` · rules: [bittrellis](https://github.com/coderbench/bittrellis) ([specification](https://github.com/coderbench/bittrellis/blob/main/docs/specification.md)).

`results/` holds one write-once record per evaluated pull-request head, `observations/` the first-seen record that decides who submitted a recipe first, and `accepted/` the artifacts of merged results. The private holdout never appears here: records carry PASS or FAIL only.
