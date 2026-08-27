# CutoverDesk threat model

Read-only static HTML demo. STRIDE against the public Vercel surface, not a live IAM platform.

| Threat | Example | Mitigation |
|---|---|---|
| Spoofing | Someone claims the page is a live Meridian console | Persistent DEMO / Synthetic badge; disclaimer footer; no login |
| Tampering | A visitor changes wave status | No write path; all numbers derived from an in-page `DATA` object |
| Repudiation | A click is treated as a program decision | Popovers are read-only; no approvals or persistence |
| Information disclosure | Real identity or HR data leaks | Synthetic data only; no directory, HR, or identity-platform APIs |
| Denial of service | Chart.js CDN is unreachable | Fallback message in chart boxes; KPI cards still render from `DATA` |
| Elevation of privilege | Visitor reaches an admin surface | No admin routes, no auth, no environment variables |

## Residual risk

The Chart.js script is loaded from a public CDN. That is an accepted V1 tradeoff for a zero-build demo. Offline or CDN failure does not expose data; charts degrade to a muted message.
