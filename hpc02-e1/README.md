# BitTrellis score records (hpc02-e1)

> Every evaluated pull request, the frontier it was ranked against, and the artifacts behind both.

## Which checkpoint to use

Every merged recipe trades a little of one thing for another. Pick by what you need; each change is against today's shipped checkpoint (V0).

![The trade-off each merged recipe makes: prompt speed against closeness to the original model, with peak GPU memory](tradeoffs.svg)

| Best for | Recipe | Closeness to the original (RP-KL) | Prompt reading, 4K | Peak GPU memory |
|---|---|---|---|---|
| **Closest to the original model** | `ud-lmhead-q4k-embed-q4k`<br>#124 by @cleanjunc ![eval:M](https://img.shields.io/badge/eval%3AM-4ac26b?style=flat-square) | **0.0459 · 1.9% further** | 39,265 tok/s · 0% faster | 25.12 GiB · 0.39 GiB less |
| **Fastest prompt reading · Least GPU memory** | `ud-downs-q4k-lmhead-embed-q4k`<br>#126 by @cleanjunc ![eval:XL](https://img.shields.io/badge/eval%3AXL-0e8a16?style=flat-square) | 0.0493 · 9.4% further | **40,279 tok/s · 3% faster** | **23.96 GiB · 1.54 GiB less** |
| *for reference* | V0, today's shipped checkpoint | 0.0450 | 39,225 tok/s | 25.51 GiB |

Build one yourself (after `scripts/setup_models.sh` in [bittrellis](https://github.com/coderbench/bittrellis)):

```bash
bittrellis build manifests/ud-lmhead-q4k-embed-q4k.yaml --out models/ud-lmhead-q4k-embed-q4k
bittrellis build manifests/ud-downs-q4k-lmhead-embed-q4k.yaml --out models/ud-downs-q4k-lmhead-embed-q4k
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
| ★ | V3-exps-q5k-down-q6k | 0.0340 | 564/784 | 382.3 | 36,996 | 29.24 | PASS | 0.364% |
|   | V0-unsloth-ud | 0.0450 | 570/784 | 397.4 | 39,225 | 25.51 | — | 0.000% |
| ★ | ud-lmhead-q4k-embed-q4k | 0.0459 | 566/784 | 397.7 | 39,265 | 25.12 | PASS | 0.002% |
|   | V1-kq-rtn-udmap | 0.0460 | 563/784 | 397.4 | 39,333 | 25.51 | PASS | 0.000% |
| ★ | ud-downs-q4k-lmhead-embed-q4k | 0.0493 | 570/784 | 403.1 | 40,279 | 23.96 | PASS | 0.536% |
| ★ | V2-all-q4k | 0.1207 | 573/784 | 466.3 | 40,265 | 23.25 | PASS | 7.128% |

Epoch `hpc02-e1` · rules: [bittrellis](https://github.com/coderbench/bittrellis) ([specification](https://github.com/coderbench/bittrellis/blob/main/docs/specification.md)).

`results/` holds one record per evaluated pull-request head -- never rewritten, with any re-measurement published beside it as `.remeasured-N` -- `observations/` the first-seen record that decides who submitted a recipe first, and `accepted/` the artifacts of merged results. The private holdout never appears here: records carry PASS or FAIL only.
