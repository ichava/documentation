# Security Policy

Canonical disclosure policy for the Ichava ecosystem. Linked by every package's `SECURITY.md`.

## Reporting a vulnerability

**Do not** open a public GitHub issue for a security report.

Two channels, in order of preference:

1. **GitHub private vulnerability reporting**, from the Security tab of the affected repository.
   The report arrives attached to the repo with a draft advisory and a CVE request path already in
   place, so nothing has to be transcribed and the fix, the advisory and the disclosure stay
   together.
2. **Email `security@simtabi.com`**, if you would rather not use GitHub or do not have an account.

Either way, include:

- Affected repo and version (commit SHA or tagged release)
- Issue type (XSS, XXE, path traversal, injection, supply-chain, etc.)
- Step-by-step reproduction
- Proof of concept or working exploit, if available
- Realistic blast radius and prerequisite conditions

## Response SLA

| Step | Window |
|---|---|
| Acknowledgement | 48 hours |
| Triage and severity | 5 business days |
| Patch released for current `main` and most recent tagged minor | 14 days for severity ≤ 3, 30 days for severity 4 |
| Public advisory and CVE filing (when assigned) | coordinated with reporter, default 90-day embargo |

## Supported versions

Until `1.0.0` is tagged, security fixes land on `main` only. From `1.0.0` onward, the latest minor of the current major receives fixes; older minors receive fixes only for severity ≤ 3.

| Channel | Status |
|---|---|
| `main` (pre-1.0) | actively supported |
| Latest tagged `1.x` | supported |
| Older `1.x` tags | severity ≤ 3 only |
| `< 1.0` (none yet) | not applicable |

## Scope

In scope:

- `ichava/core` runtime code
- `ichava/browser` HTTP layer (middleware, routes, controllers)
- `ichava/tabler-icons`, `ichava/bundled-icons`, `ichava/metronic-icons`
- The `ichava::ichava-core.make:icon-package` scaffolder output template
- Configuration defaults shipped in `config/ichava/core.php` and `config/ichava/browser.php`

Out of scope:

- Vulnerabilities in upstream icon source repositories (Tabler, Heroicons, etc.)
- Host application misconfiguration (forgetting to set `APP_KEY`, etc.)
- Issues that require an attacker to already have privileged code execution

## Threat model

Full STRIDE walkthrough, configurable hardening modes, and the audit-pipeline contract: [`security-threat-model.md`](security-threat-model.md).

## Hall of fame

Security researchers credited as reports land. Add yourself via PR after public disclosure.

## Languages

English only.
