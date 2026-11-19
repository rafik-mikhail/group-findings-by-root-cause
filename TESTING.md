# Group findings by root cause — evaluation guide

Version under test: `1.0.0`. Use deduplicated fixture clusters with source and manifests available read-only. Pre-register expected causal groups, cohorts, and singletons.

| Fixture | Expected behavior |
|---|---|
| Five CVEs in one package, all fixed by one version | One `dependency-upgrade` group with that version. |
| Two CVEs in one package, no single version fixes both | Split, with the reason. |
| Transitive vulnerable package under one direct dependency | Group records the direct dependency to change. |
| Eight SQL-injection alerts whose flows pass through one query builder | One `shared-code` group citing the shared location in each flow. |
| Eight SQL-injection alerts in unrelated functions | One pattern cohort, no causal group. |
| One Terraform module instantiated in six places, same check | One `iac-module` group. |
| Same leaked secret in three files | One `secret-rotation` group. |
| Same package in two repositories with separate lockfiles | Two groups (or linked siblings), not one. |
| Critical singleton beside a large medium-severity group | Singleton kept and visible with its own severity. |
| Membership based only on similar file names | Not placed in a causal group. |

## Scoring and release checks

Score causal-group precision strictly: a member that one change would not fix is an error. Report cohort quality separately. Fail the release on any causal membership without cited shared evidence, any cross-repository causal group without a shared change, or any severity lost by grouping.
