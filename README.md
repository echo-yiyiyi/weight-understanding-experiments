# Weight Understanding Experiments

Results snapshot collected on 2026-11-05 from four experiment-1 policy networks.

| Directory | Contents |
| --- | --- |
| [jev](jev/) | Original text runs plus coordinate-annotated and statistical-summary runs; with and without `other` |
| [gpt-6.1-sol](gpt-6.1-sol/report.md) | Full original prompts, public OpenAI API |
| [ablation-no-observation](ablation-no-observation/report.md) | Remove THE OBSERVATION; retain THE ACTIONS |
| [ablation-no-actions](ablation-no-actions/report.md) | Retain THE OBSERVATION; remove THE ACTIONS |
| [ablation-no-input-output](ablation-no-input-output/report.md) | Remove both descriptions; retain network, weights and answer instructions |

## Snapshot status

- GPT-6.1 Sol baseline: 4/4 completed, all four game identifications correct.
- No observation: 4/4 completed, all four game identifications correct.
- No actions: 3/4 completed at snapshot time; these three game identifications are correct. Freeway is unfinished, not a wrong answer.
- No input/output descriptions: 4/4 completed, all four game identifications correct.
- Jev: original, coordinate and statistics representations each scored 0/4 with `other` and 1/4 without `other`. These are separate experimental conditions, not repeated estimates of one condition.

Frogger-like road-crossing answers count as Freeway under the upstream experiment's scoring convention. Confidence in GPT answers is self-reported, unlike Jev's distribution-concentration confidence. Correct game names do not establish that every weight interpretation is correct. These are small, single-run comparisons; the baseline and ablations also differ in API provider.

## Artifacts

Markdown reports contain readable results. Per-example folders retain answers, actual requests, responses and available progress/stream logs. `answer.partial.md` is incomplete output and must not be scored as a final answer. `previous-*` and `report-before-resume-*` files retain earlier attempts; authoritative final outputs are the unprefixed response/answer files. Earlier failed public-OpenAI ablation attempts are retained separately.

`status.json` records final-response availability at snapshot time. `manifest.json` lists every artifact's SHA-256 and size. Local workspace prefixes were removed from artifact paths for portability. No API keys or virtual environments are included. Azure connection metadata contains the resource endpoint and deployment, not credentials. Original working directories remain untouched.

## Source and attribution

Prompts and network weights originate from [RikiyaT/lm_understand-logs](https://github.com/RikiyaT/lm_understand-logs), experiment 1 of *Sparks of Weight Space Programming: LLMs can understand and write neural network weights*. Their logs, data and networks are licensed CC BY 4.0; see [UPSTREAM-LICENSE.txt](UPSTREAM-LICENSE.txt). Original prompts were adapted into typed questions for Jev, or had specified sections removed for the ablation conditions. This repository contains our additional model runs, not the entire upstream dataset.
