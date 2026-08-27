# CutoverDesk build log

| Field | Value |
|---|---|
| Product | CutoverDesk |
| Repo | https://github.com/Fischer-Product-Lab/cutoverdesk |
| Live URL | https://cutoverdesk-fpl.vercel.app/ (alias of https://cutoverdesk.vercel.app/) |
| Branch | `main` |
| Shape | Single-file static HTML + Chart.js CDN (same family as FPL PF Roadmap) |

## Decisions

- **Not Next.js for V1.** The demo is a specified, Grok-executable command center. Shipping as `index.html` matches the PF Roadmap companion and keeps the public surface read-only with zero env vars.
- **Name.** CutoverDesk — TrustDesk sibling. Domain (cutover) + surface (desk).
- **Vendor-neutral platforms.** LegacyID → Nexus Identity, Meridian Financial (suite-coherent with the Q3 roadmap item).
- **Aggregated cohorts, not 12,400 rows.** Realistic for a TPM status tool; named examples live only in wave popovers.

## Publish order

1. Local product folder under `C:\Users\t_fis\dev\cutoverdesk`
2. `gh repo create Fischer-Product-Lab/cutoverdesk --public --push`
3. Vercel import / `npx vercel --prod`

## Hardening

- Dependabot for GitHub Actions
- Vulnerability alerts + automated security fixes via GitHub API
- Secret scanning expected from org defaults
