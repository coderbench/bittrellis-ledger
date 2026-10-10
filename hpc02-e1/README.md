# BitTrellis score records (hpc02-e1)

> Every evaluated pull request, the frontier it was ranked against, and the artifacts behind both.

## Which checkpoint to use

Every merged recipe trades a little of one thing for another. Pick by what you need; each change is against today's shipped checkpoint (V0).

![The trade-off each merged recipe makes: prompt speed against closeness to the original model, with peak GPU memory](tradeoffs.svg)

| Best for | Recipe | Closeness to the original (RP-KL) | Prompt reading, 4K | Peak GPU memory |
|---|---|---|---|---|
| **Closest to the original model** | `ud-exps-q5k-downs-q6k-kq-imat-lmhead-q8`<br>#152 by @e11734937-beep ![eval:S](https://img.shields.io/badge/eval%3AS-8ddb8c?style=flat-square) | **0.0304 · 32.6% closer** | 36,808 tok/s · 6% slower | 29.47 GiB · 3.96 GiB more |
| **Fastest prompt reading** | `ud-downs-q4k-lmhead-embed-q4k`<br>#126 by @cleanjunc ![eval:XL](https://img.shields.io/badge/eval%3AXL-0e8a16?style=flat-square) | 0.0493 · 9.4% further | **40,165 tok/s · 3% faster** | 23.96 GiB · 1.54 GiB less |
| **Least GPU memory** | `pr142-attention-qo-11-39-kq-imat`<br>#153 by @cleanjunc ![eval:S](https://img.shields.io/badge/eval%3AS-8ddb8c?style=flat-square) | 0.0634 · 40.8% further | 40,141 tok/s · 3% faster | **23.32 GiB · 2.18 GiB less** |
| *for reference* | V0, today's shipped checkpoint | 0.0450 | 39,151 tok/s | 25.51 GiB |

Build one yourself (after `scripts/setup_models.sh` in [bittrellis](https://github.com/coderbench/bittrellis)):

```bash
bittrellis build manifests/ud-exps-q5k-downs-q6k-kq-imat-lmhead-q8.yaml --out models/ud-exps-q5k-downs-q6k-kq-imat-lmhead-q8
bittrellis build manifests/ud-downs-q4k-lmhead-embed-q4k.yaml --out models/ud-downs-q4k-lmhead-embed-q4k
bittrellis build manifests/pr142-attention-qo-11-39-kq-imat.yaml --out models/pr142-attention-qo-11-39-kq-imat
```

## Progress

![Frontier gain credited to merged pull requests over time, pull requests scored per day by outcome, and the authors with the most credited gain.](progress.svg)

## Every measured result

Written by the evaluator after each pass. Re-derive any score yourself:

```bash
bittrellis --track HPC-02 frontier hpc02-e1/accepted <your artifact>
```

| | Checkpoint | RP-KL ↓ | tasks ↑ | decode tok/s ↑ | prefill 4K tok/s ↑ | peak GPU GiB ↓ | holdout | FG-2 |
|---|---|---:|---:|---:|---:|---:|---|---:|
| ★ | ud-exps-q5k-downs-q6k-kq-imat-lmhead-q8 | 0.0304 | 565/784 | 383.6 | 36,808 | 29.47 | PASS | 0.062% |
| ★ | V3-exps-q5k-down-q6k | 0.0340 | 564/784 | 383.6 | 37,001 | 29.24 | PASS | 0.000% |
|   | ud-exps-gate-up-q5k | 0.0366 | 562/784 | 387.0 | 37,387 | 28.01 | PASS | 0.000% |
| ★ | ud-downs-q6k-imat-lmhead-q8 | 0.0384 | 566/784 | 393.8 | 38,181 | 26.97 | PASS | 0.030% |
|   | V0-unsloth-ud | 0.0450 | 570/784 | 398.5 | 39,151 | 25.51 | — | 0.000% |
| ★ | ud-lmhead-q4k-embed-q4k | 0.0459 | 566/784 | 398.9 | 39,071 | 25.12 | PASS | 0.002% |
|   | V1-kq-rtn-udmap | 0.0460 | 563/784 | 398.9 | 39,216 | 25.51 | PASS | 0.000% |
| ★ | ud-downs-q4k-lmhead-embed-q4k | 0.0493 | 570/784 | 404.4 | 40,165 | 23.96 | PASS | 0.025% |
|   | ud-exps-gate-up-q5k-downs-gdn-qkv-q4k-kq-imat-lmhead-q8 | 0.0512 | 564/784 | 420.1 | 38,416 | 26.65 | PASS | 0.000% |
| ★ | pr129-kq-imatrix-downs-gdn-qkv | 0.0547 | 561/784 | 431.8 | 39,947 | 23.73 | PASS | 0.033% |
|   | ud-downs-q4k-gdn-qkv-q4k-lmhead-embed-q4k | 0.0612 | 565/784 | 432.1 | 40,151 | 23.73 | PASS | 0.000% |
| ★ | pr142-attention-qo-11-39-kq-imat | 0.0634 | 563/784 | 460.3 | 40,141 | 23.32 | PASS | 0.174% |
|   | pr129-recurrent-zo-deep-downs-q4k | 0.0713 | 565/784 | 447.0 | 39,424 | 23.42 | PASS | 0.000% |
| ★ | pr145-kq-imat | 0.0855 | 567/784 | 474.6 | 39,963 | 23.40 | PASS | 0.082% |
|   | pr129-recurrent-zo-q4k | 0.0965 | 570/784 | 458.7 | 39,890 | 23.50 | PASS | 0.000% |
|   | pr130-attention-qo-11-39-q4k | 0.1016 | 566/784 | 474.3 | 39,885 | 23.40 | PASS | 0.000% |
|   | V2-all-q4k | 0.1207 | 573/784 | 457.9 | 39,346 | 23.25 | PASS | 0.000% |

Epoch `hpc02-e1` · rules: [bittrellis](https://github.com/coderbench/bittrellis) ([specification](https://github.com/coderbench/bittrellis/blob/main/docs/specification.md)).

`results/` holds one record per evaluated pull-request head -- never rewritten, with any re-measurement published beside it as `.remeasured-N` -- `observations/` the first-seen record that decides who submitted a recipe first, and `accepted/` the artifacts of merged results. The private holdout never appears here: records carry PASS or FAIL only.
