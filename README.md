# Group Findings by Root Cause

> **Retired.** This step is no longer part of the workflow and the repository is archived. Grouping before validation guessed at shared causes from unvalidated findings. Its parts moved:
>
> - Mechanical fix targets (dependency and lockfile, base image, IaC module, secret) are tagged as labels in [Deduplicate Scan Findings](https://github.com/rafik-mikhail/deduplicate-scan-findings).
> - Shared code causes and missing central controls are grouped after validation through the fix key in [Decide Finding Action](https://github.com/rafik-mikhail/decide-finding-action).
> - Batching by fix key and pattern cohorts stays in [Batch Finding Fixes](https://github.com/rafik-mikhail/batch-finding-fixes).
>
> The current workflow is Normalize → Deduplicate → Prioritize → Validate → Decide → Batch.

An agent skill that groups distinct findings that one change would plausibly resolve, such as one dependency upgrade, shared helper, IaC module, or secret rotation. It also lists pattern cohorts of similar findings that need the same kind of fix in separate places. Groups are planning hypotheses, not verdicts.

## Use the skill

Use [`SKILL.md`](SKILL.md) in your agent’s skill directory under `group-findings-by-root-cause/`. Provide the clusters from [Deduplicate Scan Findings](https://github.com/rafik-mikhail/deduplicate-scan-findings), with read access to source, manifests, and IaC modules where available. The skill writes `groups/groups.jsonl` and `groups/groups.md`.

## Use as agent instructions

Copy the [Group Findings by Root Cause instruction gist](https://gist.github.com/rafik-mikhail/e59011040922d1b137dd7bcba6da371e) into your agent’s instruction file. The gist contains the same guidance with `applyTo: "**"` front matter for tools that support it. If your agent accepts plain Markdown instructions, copy the body without the front matter.

## Where it fits

This skill is step 3 of a seven-step workflow that takes a received scan report to fix pull requests. Steps 1–4 work on the whole report, steps 5–6 work on one finding at a time, and step 7 works on one batch at a time.

| Step | Skill | Works on |
|---|---|---|
| 1 | [Normalize Scan Report](https://github.com/rafik-mikhail/normalize-scan-report) | whole report |
| 2 | [Deduplicate Scan Findings](https://github.com/rafik-mikhail/deduplicate-scan-findings) | whole report |
| 3 | **Group Findings by Root Cause** | whole report |
| 4 | [Prioritize Scan Findings](https://github.com/rafik-mikhail/prioritize-scan-findings) | whole report, then again for confirmed findings |
| 5 | [Validate Scan Finding](https://github.com/rafik-mikhail/validate-scan-finding) | one finding at a time |
| 6 | [Decide Finding Action](https://github.com/rafik-mikhail/decide-finding-action) | one finding at a time |
| 7 | [Batch Finding Fixes](https://github.com/rafik-mikhail/batch-finding-fixes) | one batch at a time |

Verification by rescan and closing with regression monitoring are not covered yet.

## How to test

Follow the [evaluation guide](TESTING.md).

## Notes

[NOTES.md](NOTES.md) covers gotchas, areas for improvement, and the sources behind the guidance.
