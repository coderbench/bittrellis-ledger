# BitTrellis score records (hpc01-e6)

> Every evaluated pull request, the frontier it was ranked against, and the artifacts behind both.

## Which checkpoint to use

Every merged recipe trades a little of one thing for another. Pick by what you need; each change is against today's shipped checkpoint (V0).

![The trade-off each merged recipe makes: prompt speed against closeness to the original model, with peak GPU memory](tradeoffs.svg)

| Best for | Recipe | Closeness to the original (RP-KL) | Prompt reading, 4K | Peak GPU memory |
|---|---|---|---|---|
| **Closest to the original model** | `nvfp4-gptq-mlp-gdn-fp8-state-lmhead-q4k`<br>#107 by @kaivexa ![eval:XS](https://img.shields.io/badge/eval%3AXS-c6efce?style=flat-square) | **0.0663 · 51.1% closer** | 14,509 tok/s · 14% slower | 23.39 GiB · 1.38 GiB more |
| **Fastest prompt reading** | `nvfp4-gptq-mlp-attn-q4k-lmhead-q4k`<br>#106 by @kaivexa ![eval:XS](https://img.shields.io/badge/eval%3AXS-c6efce?style=flat-square) | 0.0807 · 40.5% closer | **15,707 tok/s · 7% slower** | 21.85 GiB · 0.16 GiB less |
| **Least GPU memory** | `nvfp4-gptq-mlp-0-24-47-q4k-mlp-1-23-48-63-gdn-qkv-attn-q4k-lmhead-q4k`<br>#112 by @cleanjunc ![eval:XS](https://img.shields.io/badge/eval%3AXS-c6efce?style=flat-square) | 0.0818 · 39.7% closer | 10,251 tok/s · 39% slower | **20.98 GiB · 1.03 GiB less** |
| *for reference* | V0, today's shipped checkpoint | 0.1357 | 16,895 tok/s | 22.02 GiB |

Build one yourself (after `scripts/setup_models.sh` in [bittrellis](https://github.com/coderbench/bittrellis)):

```bash
bittrellis build manifests/nvfp4-gptq-mlp-gdn-fp8-state-lmhead-q4k.yaml --out models/nvfp4-gptq-mlp-gdn-fp8-state-lmhead-q4k
bittrellis build manifests/nvfp4-gptq-mlp-attn-q4k-lmhead-q4k.yaml --out models/nvfp4-gptq-mlp-attn-q4k-lmhead-q4k
bittrellis build manifests/nvfp4-gptq-mlp-0-24-47-q4k-mlp-1-23-48-63-gdn-qkv-attn-q4k-lmhead-q4k.yaml --out models/nvfp4-gptq-mlp-0-24-47-q4k-mlp-1-23-48-63-gdn-qkv-attn-q4k-lmhead-q4k
```

## Progress

![Frontier gain credited to merged pull requests over time, pull requests scored per day by outcome, and the authors with the most credited gain.](progress.svg)

## Every measured result

Written by the evaluator after each pass. Re-derive any score yourself:

```bash
bittrellis frontier hpc01-e6/accepted <your artifact>
```

| | Checkpoint | RP-KL ↓ | tasks ↑ | decode tok/s ↑ | prefill 4K tok/s ↑ | peak GPU GiB ↓ | holdout | FG-2 |
|---|---|---:|---:|---:|---:|---:|---|---:|
|   | nvfp4-gptq-mlp-gdn-fp8-all-attn-q4k-lmhead-q4k | 0.0628 | 567/784 | 83.4 | 13,022 | 23.78 | PASS | 0.000% |
| ★ | nvfp4-gptq-mlp-gdn-fp8-state-lmhead-q4k | 0.0663 | 561/784 | 86.1 | 14,509 | 23.39 | PASS | 0.016% |
| ★ | nvfp4-gptq-mlp-gdn-fp8-qkv-attn-q4k-lmhead-q4k | 0.0688 | 561/784 | 88.7 | 13,599 | 22.68 | PASS | 0.021% |
|   | nvfp4-blockfit-gdn-fp8-qkv-attn-q4k-lmhead-q4k | 0.0743 | 570/784 | 88.7 | 13,731 | 22.68 | PASS | 0.000% |
| ★ | nvfp4-gptq-mlp-gdn-qkv-attn-q4k-lmhead-q4k | 0.0754 | 574/784 | 94.4 | 13,725 | 21.67 | PASS | 0.030% |
|   | gdn-fp8-state-blockfit | 0.0760 | 572/784 | 86.2 | 14,666 | 23.39 | PASS | 0.000% |
|   | nvfp4-blockfit-gdn-fp8-qkv-attn-q4k-mlp-q4k-1-23-48-63-lmhead-q4k | 0.0763 | 577/784 | 89.4 | 10,261 | 21.99 | PASS | 0.000% |
|   | nvfp4-blockfit-gdn-fp8-qkv-lmhead-q4k | 0.0782 | 575/784 | 88.9 | 14,534 | 22.84 | PASS | 0.000% |
|   | nvfp4-blockfit-gdn-fp8-qkv12-51-attn-q4k-lmhead-q4k | 0.0796 | 563/784 | 90.8 | 14,433 | 22.38 | PASS | 0.000% |
|   | nvfp4-gptq-mlp-gdn-fp8-mid24-35-lmhead-q4k | 0.0798 | 568/784 | 92.5 | 16,059 | 22.39 | PASS | 0.000% |
| ★ | nvfp4-gptq-mlp-attn-q4k-lmhead-q4k | 0.0807 | 573/784 | 94.9 | 15,707 | 21.85 | PASS | 0.006% |
| ★ | nvfp4-gptq-mlp-0-24-47-q4k-mlp-1-23-48-63-gdn-qkv-attn-q4k-lmhead-q4k | 0.0818 | 567/784 | 94.7 | 10,251 | 20.98 | PASS | 0.015% |
|   | nvfp4-blockfit-gdn-fp8-qkv16-47-zo24-35-lmhead-q4k | 0.0849 | 573/784 | 90.6 | 15,407 | 22.65 | PASS | 0.000% |
|   | gdn-fp8-mlp-q4k-zo-deep-q4k | 0.0850 | 568/784 | 86.9 | 8,897 | 22.16 | PASS | 0.000% |
|   | gdn-fp8-mlp-q4k-skip0 | 0.0853 | 566/784 | 84.0 | 8,816 | 22.82 | PASS | 0.000% |
|   | nvfp4-blockfit-gdn-qkv-attn-q4k-lmhead-q4k | 0.0858 | 569/784 | 94.3 | 13,813 | 21.67 | PASS | 0.000% |
|   | gdn-fp8-qkv-z-out-q4k-mlp-q4k | 0.0872 | 573/784 | 88.4 | 8,927 | 21.85 | PASS | 0.000% |
|   | gdn-q4k-fp8-mid24-35-mlp-q4k | 0.0889 | 568/784 | 93.7 | 8,941 | 20.98 | PASS | 0.000% |
|   | gdn-fp8-unsloth-mlp0-27-q4k-mlp46-63-lmhead | 0.0892 | 572/784 | 83.5 | 11,881 | 23.61 | PASS | 0.000% |
|   | nvfp4-blockfit-gdn-fp8-mid24-35-lmhead-q4k | 0.0896 | 575/784 | 92.6 | 16,198 | 22.39 | PASS | 0.000% |
| ★ | q4k-qkv-attn-mlp-nvfp4-blockfit-zo-lmhead | 0.0899 | 565/784 | 95.1 | 8,849 | 20.56 | PASS | 0.013% |
|   | nvfp4-blockfit-attn-q4k-lmhead-q4k | 0.0909 | 563/784 | 94.9 | 15,813 | 21.85 | PASS | 0.000% |
| ★ | gdn-attn-q4k-early3-mid28-blockfit-rest-lmhead | 0.0921 | 572/784 | 95.3 | 12,506 | 21.36 | PASS | 0.003% |
|   | gdn-fp8-qkv-out-q4k-mlp-early8-mid55 | 0.0938 | 570/784 | 88.1 | 10,255 | 22.25 | PASS | 0.000% |
| ★ | gdn-q4k-mlp-early8-mid24-skip0-attn-blockfit-rest-lmhead | 0.0946 | 566/784 | 95.7 | 10,890 | 21.08 | PASS | 0.000% |
|   | gdn-fp8-lmhead-q4k | 0.0967 | 576/784 | 83.4 | 13,842 | 23.93 | PASS | 0.000% |
| ★ | nvfp4-blockfit-all-lmhead-q4k | 0.0992 | 567/784 | 95.0 | 16,893 | 22.02 | PASS | 0.039% |
|   | gdn-q4k-skip0-nvfp4-blockfit-rest-lmhead-q4k | 0.1015 | 578/784 | 95.2 | 13,954 | 21.64 | PASS | 0.000% |
|   | V3-gdn-fp8 | 0.1024 | 573/784 | 83.3 | 13,761 | 23.93 | PASS | 0.000% |
| ★ | gdn-mlp-q4k-skip-layer0 | 0.1029 | 564/784 | 96.2 | 8,993 | 20.54 | PASS | 0.000% |
|   | gdn-q4k-fp8-mid24-35-unsloth-mlp0-27-lmhead | 0.1031 | 574/784 | 92.8 | 13,984 | 22.08 | PASS | 0.000% |
|   | gdn-fp8-mid24-35-unsloth-mlp0-27-lmhead | 0.1078 | 575/784 | 92.6 | 16,217 | 22.39 | PASS | 0.000% |
|   | gdn-fp8-qkv-all-zo-split | 0.1083 | 568/784 | 87.8 | 14,229 | 23.02 | PASS | 0.000% |
| ★ | gdn-attn-q4k-mlp-early8-mid24-skip0 | 0.1091 | 572/784 | 95.7 | 10,417 | 20.92 | PASS | 0.000% |
|   | gdn-state-fp8-skip0 | 0.1115 | 573/784 | 86.1 | 14,568 | 23.51 | PASS | 0.000% |
|   | gdn-attn-q4k-mlp-early3-mid28-skip0 | 0.1134 | 560/784 | 95.4 | 12,472 | 21.36 | PASS | 0.000% |
|   | gdn-attn-q4k-mlp-mid | 0.1136 | 566/784 | 95.5 | 10,997 | 21.06 | PASS | 0.000% |
| ★ | V1-all-q4k | 0.1142 | 575/784 | 96.1 | 8,619 | 20.25 | PASS | 0.043% |
|   | gdn-fp8-mid24-35-lmhead-q4k | 0.1167 | 567/784 | 92.6 | 16,223 | 22.39 | PASS | 0.000% |
| ★ | gdn-zo-deep-mlp-skip0 | 0.1178 | 563/784 | 96.0 | 9,449 | 20.81 | PASS | 0.000% |
| ★ | V9-gdn-q4k-mlp-q4k | 0.1179 | 562/784 | 96.2 | 8,903 | 20.41 | — | 0.000% |
|   | gdn-q4k-skip-layer0 | 0.1210 | 572/784 | 95.2 | 13,931 | 21.64 | PASS | 0.000% |
|   | gdn-q4k-deep | 0.1238 | 578/784 | 95.1 | 15,246 | 21.83 | FAIL | 0.000% |
| | ↳ *not credited: private holdout FAIL* | | | | | | | |
|   | V7-mlp-q4k-early | 0.1247 | 561/784 | 95.6 | 9,794 | 21.40 | — | 0.000% |
|   | mlp-q4k-skip-layer0 | 0.1249 | 563/784 | 96.3 | 10,019 | 20.91 | PASS | 0.000% |
|   | V13-mlp-unsloth-bytes | 0.1258 | 566/784 | 95.0 | 16,851 | 22.02 | FAIL | 0.000% |
| | ↳ *not credited: private holdout FAIL* | | | | | | | |
|   | gdn-mlp-deep-q4k | 0.1258 | 567/784 | 95.6 | 11,653 | 21.26 | PASS | 0.000% |
|   | V4-gdn-q4k | 0.1265 | 566/784 | 95.2 | 13,904 | 21.58 | PASS | 0.000% |
|   | V5-attn-q4k | 0.1282 | 556/784 | 94.8 | 15,760 | 21.85 | — | 0.000% |
|   | V6-mlp-q4k | 0.1294 | 563/784 | 96.3 | 9,978 | 20.84 | PASS | 0.000% |
|   | V0-baseline-rebuild | 0.1357 | 564/784 | 95.0 | 16,895 | 22.02 | — | 0.000% |

Epoch `hpc01-e6` · rules: [bittrellis](https://github.com/coderbench/bittrellis) ([specification](https://github.com/coderbench/bittrellis/blob/main/docs/specification.md)).

`results/` holds one record per evaluated pull-request head -- never rewritten, with any re-measurement published beside it as `.remeasured-N` -- `observations/` the first-seen record that decides who submitted a recipe first, and `accepted/` the artifacts of merged results. The private holdout never appears here: records carry PASS or FAIL only.
