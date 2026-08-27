# CutoverDesk

**Identity cutover, by wave.**

A Fischer Product Lab command center for a Technical Program Manager running an enterprise identity-platform migration. It shows Meridian Financial’s synthetic cutover from **LegacyID** to **Nexus Identity** so an org team can read progress in about ten seconds.

> **Synthetic demonstration.** Every identity count, application, and risk is fictional. There is no live directory, HR, or identity-platform integration, no authentication, and no write path. The UI shows a persistent DEMO badge.

**Live:** [cutoverdesk-fpl.vercel.app](https://cutoverdesk-fpl.vercel.app/) · **Repo:** [Fischer-Product-Lab/cutoverdesk](https://github.com/Fischer-Product-Lab/cutoverdesk)

## Screens

| Tab | What it answers |
|---|---|
| **Overview** | Identities on Nexus, apps cut over, waves complete, blocked/fallout, LegacyID decommissioned |
| **Waves** | Six-wave Gantt plus gate and decommission milestones |
| **Identities** | Funnel, wave × criticality matrix, 26-cohort register |
| **Applications** | 20 apps by tier, protocol, wave, and SOX flag |
| **Risks** | Register, decisions needed, readiness coverage, LegacyID burndown |

## Local

Open `index.html` in a browser (Chart.js loads from CDN — network required once).

Or:

```bash
npx serve .
```

## Deploy

Static site. Root file is `index.html`. Re-deploy with `npx vercel --prod`, or connect the GitHub repo in the Vercel project settings for push-to-deploy.

## Fischer Product Lab suite

| Product | Question |
|---|---|
| [AgentOps](https://agentops-fpl.vercel.app/) | Is this AI initiative safe to launch? |
| [TrustDesk](https://trustdesk-fpl.vercel.app/) | Can we answer the customer questionnaire with evidence? |
| [VulnBoard](https://vuln-board.vercel.app/) | What is the executive vuln posture? |
| [ProductPulse](https://productpulse-fpl.vercel.app/) | Did the launched thing actually work? |
| [Portfolio Health](https://portfolio-health-fpl.vercel.app/) | How is the whole operating portfolio doing? |
| [PF Roadmap](https://fpl-pf-roadmap.vercel.app/) | Are we planned and loaded for the quarter? |
| **CutoverDesk** | How is the identity migration actually going? |

## Security

Read-only synthetic demo: no real data, no secrets, no live integrations. See [SECURITY.md](./SECURITY.md) and [docs/threat-model.md](./docs/threat-model.md).
