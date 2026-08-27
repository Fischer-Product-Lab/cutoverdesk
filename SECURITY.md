# Security Policy

CutoverDesk is a **public, read-only portfolio demonstration**. The security posture below is intentional: mature, secure-by-design judgment rather than a feature-complete production system.

## Data handling

This project uses **synthetic data only**. No production, customer, employer, directory, or personal data is stored in this repository or the demo environment. Every identity count, application, risk, and named example is invented for demonstration.

## Security controls

- **Read-only public demo** — no forms that mutate data, no public write endpoints, no admin surface.
- **Synthetic data only** — no real identities, no PII, no employer systems.
- **No client-side secrets** — no API keys or sensitive values in browser-delivered code.
- **No AI calls in V1** — all status, percentages, and RAG colors are derived at runtime from the embedded `DATA` object.
- **No file uploads** and **no uncontrolled public AI prompt box.**
- **V1 requires no environment variables.**
- **Documented threat model** — see [`docs/threat-model.md`](./docs/threat-model.md).

## Reporting a vulnerability

Because this is a synthetic, read-only demo, the security risk surface is minimal. If you notice a concern (for example, accidentally committed secrets), please open a private security advisory via the repository's **Security** tab, or open an issue without including sensitive details. There is no SLA; this is a personal portfolio project.
