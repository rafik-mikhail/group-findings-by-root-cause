# Notes: Group findings by root cause

## Gotchas

- **Causal group or cohort.** GitHub security campaigns group alerts by rule, CWE, or severity; that is a cohort, useful for focused work. DefectDojo Root Causes groups findings that one fix would clear; that is a causal group. Keep the two apart, because only a causal group can share one fix key.
- **A group is not a verdict.** Validating the representative does not validate the members. Each member keeps its own disposition.
- **Fixed versions conflict.** Advisories for one package can need different minimum versions, or one may need a major upgrade. Choose the version that satisfies all, or split.
- **Transitive dependencies.** The change usually belongs to the direct parent, not the vulnerable package.
- **Monorepos.** One shared lockfile or version catalog can make findings across many packages a single change; separate lockfiles cannot.
- **Big groups hide small risks.** Ordering by size helps throughput, not risk. Step 4 sets priority.

## Areas for improvement

- Add a dependency-graph helper that computes the minimal fixing version and the direct parent automatically.
- Add a shared-location detector over SARIF code flows.
- Link groups across repositories when an organization-wide base image or shared library is the cause.

## Sources

- [DefectDojo RBVM buyer's guide](https://defectdojo.com/hubfs/Whitepapers/RBVM_Buyers_Guide_DefectDojo_Pro.pdf): Root Causes groups findings one fix would clear, ranked by findings and assets.
- [DefectDojo: Triage findings](https://docs.defectdojo.com/triage_findings/): group findings that share a vulnerable component, CVE, infrastructure resource, or weakness at a URL.
- [GitHub: About security campaigns](https://docs.github.com/en/code-security/concepts/security-at-scale/about-security-campaigns): grouping closely related alerts by rule, CWE, or severity.
- [GitHub: Dependabot security updates](https://docs.github.com/en/code-security/concepts/supply-chain-security/dependabot-security-updates): grouped security updates per ecosystem.
