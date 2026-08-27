# Grok Prompt — Meridian Financial CutoverDesk Identity Migration Command Center

> **How to use:** Paste this entire document into Grok 4.6. Grok must return **one complete, self-contained HTML file** and nothing else (no markdown fences around the HTML unless required by the chat UI; if fences are required, wrap the whole file once). Open the saved `.html` file in a browser — zero build step.

---

## 0. Role & Output Contract

You are a senior front-end engineer building a **synthetic technical-program-management demonstration** for Meridian Financial (fictional). Produce a single HTML file named conceptually `iam-migration-command-center.html` that contains:

- All CSS in a `<style>` block
- All JavaScript in a `<script>` block (after Chart.js CDN)
- The canonical `DATA` object **copied verbatim** from Section 3 (do not invent alternate keys, counts, or dates)
- Chart.js loaded from: `https://cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.min.js`
- Vanilla JS only — no React, no build tools, no other libraries (no Gantt library; implement the Gantt with CSS + JS)
- No network calls except the Chart.js CDN script tag
- No authentication, no write path, no real directory / HR / identity-platform API

**Hard rules:**

1. Every number shown on any tab MUST be derived from `DATA` at runtime (`.length`, `.reduce`, `filter`, helper sums). Never hard-code tab totals that can drift.
2. Do not truncate the HTML. Emit the complete file.
3. Fixed "today" for all date logic: `2026-08-26` (from `DATA.meta.today`).
4. Show a persistent **DEMO / Synthetic data** badge in the header.
5. Before finishing, run the Acceptance Checklist in Section 11 mentally and fix any failures.

This is a Fischer Product Lab portfolio demo. It must look like a premium CISO / IAM program command center: an organizational team (executives, app owners, service desk, security) should understand migration progress in about ten seconds on Tab 1.

---

## 1. Product Brief

| Field | Value |
|---|---|
| Company | Meridian Financial (fictional) |
| Product | CutoverDesk — Identity Migration Command Center |
| Source platform | LegacyID (retiring) |
| Target platform | Nexus Identity (destination) |
| Program | Workforce identity cutover, LegacyID → Nexus Identity |
| Program window | 2026-06-01 → 2026-12-31 |
| Fixed today | 2026-08-26 |
| Audience | Organizational team needing a simple, fast read on identity-migration status |
| Persona / lens | Technical Program Manager, Enterprise Identity & Access Management |

**Five tabs (in order):**

1. **Overview** — ten-second program status: KPI cards, overall bar, per-wave RAG bars, health line
2. **Waves** — CSS/JS Gantt of the six waves plus gate / decommission milestones
3. **Identities** — migration funnel + wave × criticality matrix + cohort register
4. **Applications** — app cutover by tier, protocol, wave, SOX flag
5. **Risks** — risk register, decisions needed, readiness coverage, LegacyID decommission burndown

**How to read the program (put this as a one-line legend under the Overview KPI row):**

> On Nexus = Migrated + Verified + Legacy disabled. A wave is Complete only when exit criteria are met. `blocked` is an overlay (subset of not-yet-cut-over identities), not a seventh funnel stage.

---

## 2. Design System

### 2.1 Shell (Fischer Product Lab navy / gold)

- Page background: vertical gradient `#0C1B30` → `#1F3A5F`
- Ivory cards: `#F5F1E6`, inner muted well `#E8E2D0`
- Gold accents: `#E4C778` (highlight) and `#C29A45` (deep)
- Text on navy chrome: `#F5F1E6`; muted on navy: `#8B9BB4`
- Text on ivory cards: `#0C1B30`; muted on ivory: `#5C6B80`
- Header (navy): product title **CutoverDesk**, subtitle `Meridian Financial · LegacyID → Nexus Identity`, program window, **DEMO** pill
- DEMO pill: background `#C29A45`, text `#0C1B30`, bold 11px, letter-spacing 0.04em
- Tab bar on navy: inactive tabs ivory/60; active tab gold underline (2px `#E4C778`) + `#1F3A5F` pill background
- Content max-width ~1440px, centered, 16–24px padding
- Cards: `border-radius: 10px`, shadow `0 8px 24px rgba(0,0,0,0.35)`, 16–20px padding, 2px gold top-border on KPI cards
- Font stack: `-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif`
- Large KPI numbers: 28–32px, tabular-nums, navy on ivory
- Do **not** use a light Jira theme. This is a dark navy command center with ivory cards.

### 2.2 Wave colors (Gantt bars, chips, matrix row accents, charts — identical everywhere)

| Wave | Color |
|---|---|
| Wave 0 — Pilot | `#E4C778` |
| Wave 1 — Standard workforce | `#4C9AFF` |
| Wave 2 — Business-critical | `#36B37E` |
| Wave 3 — Privileged access | `#FF8B37` |
| Wave 4 — Executives | `#C87BFF` |
| Wave 5 — Non-human identities | `#8B9BB4` |

### 2.3 Criticality / privilege / protocol / status pills

| Kind | Values → colors |
|---|---|
| Criticality | Executive `#C87BFF`, Business-Critical `#FF8B37`, Standard `#4C9AFF`, Contingent `#36B37E`, Non-Human `#8B9BB4` |
| Privilege | Privileged `#B03A3A`, Elevated `#D4A017`, Standard `#5C6B80` |
| Protocol | SAML `#C29A45`, OIDC `#4C9AFF`, LDAP `#00A3BF`, Legacy `#6B778C` |
| Identity funnel | Not Started `#6B778C`, Ready `#4C9AFF`, Scheduled `#D4A017`, Migrated `#36B37E`, Verified `#3D9B6E`, Legacy Disabled `#1F3A5F` |
| App cutover | Verified `#3D9B6E`, Cut Over `#36B37E`, In Dual-Run `#D4A017`, Deferred `#6B778C`, Not Started `#8B9BB4` |
| Risk severity | Critical `#B03A3A`, High `#FF8B37`, Medium `#D4A017`, Low `#5C6B80` |
| Risk status | Open `#B03A3A`, Mitigating `#D4A017`, Watch `#4C9AFF`, Closed `#3D9B6E` |
| RAG | Green `#3D9B6E`, Amber `#D4A017`, Red `#B03A3A` |
| Wave / app / milestone status | Complete / Verified / Cut Over → green; In Progress / In Dual-Run / Mitigating → amber; Planned / Upcoming / Not Started → slate; Blocked / Open Critical → red |

Pills: small, rounded-full, bold 11–12px. On solid color use ivory or navy text for contrast so every pill meets ~4.5:1.

- **Navy text** (`#0C1B30`) on gold, amber, light-blue, purple, teal, slate, **and greens** (`#E4C778`, `#C29A45`, `#4C9AFF`, `#D4A017`, `#C87BFF`, `#00A3BF`, `#8B9BB4`, `#FF8B37`, `#36B37E`, `#3D9B6E`).
- **Ivory text** (`#F5F1E6`) on navy and the darkened red (`#B03A3A` — do **not** use `#C94C4C`; it fails 4.5:1 with ivory).

### 2.4 Number formatting

```js
function formatInt(n) { return Math.round(n).toLocaleString("en-US"); }
function formatPct(ratio) {
  const p = Math.round(ratio * 1000) / 10; /* one decimal */
  return Number.isInteger(p) ? p + "%" : p.toFixed(1) + "%";
}
function formatDate(iso) { /* e.g. "Aug 26, 2026" — en-US, UTC noon to avoid TZ shift */ }
```

---

## 3. Canonical Dataset — Embed Verbatim

Copy the following object into the HTML as `const DATA = { ... };`. **Do not edit values.** All UI derives from this.

```js
const DATA = {
  meta: {
    company: "Meridian Financial",
    product: "CutoverDesk",
    program: "LegacyID → Nexus Identity Migration",
    sourcePlatform: "LegacyID",
    targetPlatform: "Nexus Identity",
    windowStart: "2026-06-01",
    windowEnd: "2026-12-31",
    today: "2026-08-26",
    owner: "Technical Program Manager, Enterprise IAM",
    disclaimer: "Synthetic demonstration data. No live directory, HR, or identity-platform integration."
  },

  waves: [
    {
      id: "w0",
      name: "Wave 0 — Pilot",
      shortName: "Wave 0",
      audience: "IT staff and IAM team (canary cohort)",
      color: "#E4C778",
      start: "2026-06-01",
      end: "2026-06-28",
      status: "Complete",
      definition: "Smallest blast-radius cohort. Proves dual-run, helpdesk playbooks, and rollback before any business population moves.",
      entryCriteria: [
        "Dual-run architecture live on Nexus Identity",
        "Break-glass accounts tested",
        "Service-desk Wave 0 runbook certified"
      ],
      exitCriteria: [
        "Pilot identities verified on Nexus for 10 business days",
        "No Sev-1 auth incidents attributable to cutover",
        "LegacyID disabled for the pilot cohort"
      ],
      examples: [
        { name: "Priya N.", role: "IAM Engineer", status: "Legacy Disabled" },
        { name: "Marcus T.", role: "IT Operations Lead", status: "Verified" }
      ]
    },
    {
      id: "w1",
      name: "Wave 1 — Standard workforce",
      shortName: "Wave 1",
      audience: "Low-privilege, low-criticality departments and contingent staff",
      color: "#4C9AFF",
      start: "2026-06-23",
      end: "2026-09-12",
      status: "In Progress",
      definition: "Largest population. Standard and contingent identities on Tier 2–3 applications. Moves only after Wave 0 exit criteria are met.",
      entryCriteria: [
        "Wave 0 gate = Go",
        "MFA enrollment ≥ 70% in scoped departments",
        "Manager attestation campaign launched"
      ],
      exitCriteria: [
        "≥ 95% of Wave 1 identities on Nexus",
        "Contingent MFA exception backlog < 50",
        "LegacyID disabled for completed departments"
      ],
      examples: [
        { name: "Elena R.", role: "Retail Banking Supervisor", status: "Verified" },
        { name: "Wei C.", role: "EMEA contingent contractor", status: "Blocked — MFA exception" }
      ]
    },
    {
      id: "w2",
      name: "Wave 2 — Business-critical users",
      shortName: "Wave 2",
      audience: "Revenue-adjacent teams and Tier 1 application users",
      color: "#36B37E",
      start: "2026-08-04",
      end: "2026-10-17",
      status: "In Progress",
      definition: "Wealth, markets, commercial banking, and client services. Dual-run required on SOX-relevant Tier 1 apps before LegacyID disable.",
      entryCriteria: [
        "Wave 1 ≥ 60% on Nexus",
        "Tier 1 SAML/OIDC mappings signed by app owners",
        "SOX evidence pack drafted"
      ],
      exitCriteria: [
        "All Tier 1 in-scope apps Verified or Cut Over",
        "SOX control evidence signed",
        "Fallout < 2% of wave population"
      ],
      examples: [
        { name: "Sofia M.", role: "Wealth Advisor", status: "In Dual-Run" },
        { name: "Jonah K.", role: "Capital Markets trader", status: "Scheduled" }
      ]
    },
    {
      id: "w3",
      name: "Wave 3 — Privileged access",
      shortName: "Wave 3",
      audience: "Admins and elevated-entitlement holders",
      color: "#FF8B37",
      start: "2026-09-21",
      end: "2026-11-07",
      status: "Planned",
      definition: "Privileged users move only after recording, approval, and break-glass controls are proven on Nexus. Highest access risk.",
      entryCriteria: [
        "Wave 2 gate = Go",
        "Privileged session recording live on Nexus",
        "Break-glass path retested",
        "SOX evidence pack signed"
      ],
      exitCriteria: [
        "100% of privileged identities on Nexus with recording",
        "Standing privileged grants recertified",
        "LegacyID admin paths disabled"
      ],
      examples: [
        { name: "Omar H.", role: "Security admin (privileged)", status: "Ready — gated" },
        { name: "Ravi S.", role: "Directory admin", status: "Not Started" }
      ]
    },
    {
      id: "w4",
      name: "Wave 4 — Executives & high-touch",
      shortName: "Wave 4",
      audience: "C-suite, board, and white-glove support cohort",
      color: "#C87BFF",
      start: "2026-10-26",
      end: "2026-11-21",
      status: "Planned",
      definition: "Smallest human wave. Dedicated concierge cutover on a published weekend, after privileged controls are live.",
      entryCriteria: [
        "Wave 3 privileged controls live",
        "White-glove runbook complete",
        "Executive device compliance 100%"
      ],
      exitCriteria: [
        "Every executive identity verified on Nexus",
        "Concierge hypercare closed with no open Sev-2+",
        "LegacyID disabled for the executive OU"
      ],
      examples: [
        { name: "A. Hale", role: "Chief Operating Officer", status: "Not Started" },
        { name: "Board Secretary", role: "Governance office", status: "Ready (attested)" }
      ]
    },
    {
      id: "w5",
      name: "Wave 5 — Non-human identities",
      shortName: "Wave 5",
      audience: "Service accounts, shared mailboxes, federated partners",
      color: "#8B9BB4",
      start: "2026-11-02",
      end: "2026-12-19",
      status: "Planned",
      definition: "Hardest wave. Non-human identities have no manager to attest them and often have hardcoded secrets. Inventory quality gates the start.",
      entryCriteria: [
        "Complete NHI inventory with owner",
        "Secret-rotation window agreed",
        "Partner federation metadata refreshed"
      ],
      exitCriteria: [
        "Every in-scope NHI has an owner and rotation date",
        "Partner metadata validated in a dry run",
        "LegacyID service-account namespace decommissioned"
      ],
      examples: [
        { name: "svc-ledger-batch", role: "General Ledger batch job", status: "Not Started" },
        { name: "fed-partner-clearing", role: "Partner federation identity", status: "Ready — metadata review" }
      ]
    }
  ],

  /* 26 cohorts. Status columns MUST sum to the cohort population.
   * blocked is an overlay (subset of notStarted + ready + scheduled), NOT a seventh stage.
   * Grand total of status columns = 12,400. */
  cohorts: [
    /* —— Wave 0 —— */
    { id: "C-W0-01", wave: "w0", criticality: "Standard", privilege: "Elevated", department: "IT Operations", region: "AMER", notStarted: 0, ready: 0, scheduled: 0, migrated: 8, verified: 12, legacyDisabled: 120, blocked: 0 },
    { id: "C-W0-02", wave: "w0", criticality: "Standard", privilege: "Privileged", department: "Identity & Access", region: "AMER", notStarted: 0, ready: 0, scheduled: 0, migrated: 4, verified: 6, legacyDisabled: 70, blocked: 0 },
    { id: "C-W0-03", wave: "w0", criticality: "Standard", privilege: "Elevated", department: "Security Operations", region: "AMER", notStarted: 0, ready: 0, scheduled: 0, migrated: 2, verified: 8, legacyDisabled: 50, blocked: 0 },

    /* —— Wave 1 —— */
    { id: "C-W1-01", wave: "w1", criticality: "Standard", privilege: "Standard", department: "Retail Banking", region: "AMER", notStarted: 40, ready: 80, scheduled: 120, migrated: 280, verified: 420, legacyDisabled: 900, blocked: 28 },
    { id: "C-W1-02", wave: "w1", criticality: "Standard", privilege: "Standard", department: "Retail Banking", region: "EMEA", notStarted: 60, ready: 90, scheduled: 110, migrated: 180, verified: 200, legacyDisabled: 280, blocked: 22 },
    { id: "C-W1-03", wave: "w1", criticality: "Standard", privilege: "Standard", department: "Human Resources", region: "AMER", notStarted: 20, ready: 40, scheduled: 60, migrated: 80, verified: 140, legacyDisabled: 300, blocked: 8 },
    { id: "C-W1-04", wave: "w1", criticality: "Contingent", privilege: "Standard", department: "Contingent Workforce", region: "AMER", notStarted: 180, ready: 220, scheduled: 160, migrated: 200, verified: 180, legacyDisabled: 160, blocked: 48 },
    { id: "C-W1-05", wave: "w1", criticality: "Standard", privilege: "Standard", department: "Operations", region: "AMER", notStarted: 50, ready: 70, scheduled: 80, migrated: 160, verified: 220, legacyDisabled: 400, blocked: 14 },
    { id: "C-W1-06", wave: "w1", criticality: "Standard", privilege: "Standard", department: "Operations", region: "APAC", notStarted: 80, ready: 90, scheduled: 70, migrated: 100, verified: 90, legacyDisabled: 110, blocked: 18 },
    { id: "C-W1-07", wave: "w1", criticality: "Standard", privilege: "Standard", department: "Finance Shared Services", region: "AMER", notStarted: 30, ready: 50, scheduled: 60, migrated: 120, verified: 180, legacyDisabled: 280, blocked: 10 },
    { id: "C-W1-08", wave: "w1", criticality: "Standard", privilege: "Standard", department: "Marketing", region: "AMER", notStarted: 20, ready: 30, scheduled: 40, migrated: 70, verified: 80, legacyDisabled: 140, blocked: 6 },
    { id: "C-W1-09", wave: "w1", criticality: "Contingent", privilege: "Standard", department: "Contingent Workforce", region: "EMEA", notStarted: 40, ready: 50, scheduled: 40, migrated: 50, verified: 60, legacyDisabled: 60, blocked: 12 },

    /* —— Wave 2 —— */
    { id: "C-W2-01", wave: "w2", criticality: "Business-Critical", privilege: "Standard", department: "Wealth Management", region: "AMER", notStarted: 180, ready: 160, scheduled: 140, migrated: 160, verified: 120, legacyDisabled: 100, blocked: 36 },
    { id: "C-W2-02", wave: "w2", criticality: "Business-Critical", privilege: "Standard", department: "Capital Markets", region: "AMER", notStarted: 160, ready: 140, scheduled: 120, migrated: 100, verified: 80, legacyDisabled: 40, blocked: 28 },
    { id: "C-W2-03", wave: "w2", criticality: "Business-Critical", privilege: "Standard", department: "Commercial Banking", region: "AMER", notStarted: 120, ready: 110, scheduled: 90, migrated: 80, verified: 70, legacyDisabled: 50, blocked: 20 },
    { id: "C-W2-04", wave: "w2", criticality: "Business-Critical", privilege: "Standard", department: "Wealth Management", region: "EMEA", notStarted: 100, ready: 80, scheduled: 70, migrated: 60, verified: 40, legacyDisabled: 30, blocked: 16 },
    { id: "C-W2-05", wave: "w2", criticality: "Business-Critical", privilege: "Standard", department: "Client Services", region: "AMER", notStarted: 40, ready: 50, scheduled: 40, migrated: 40, verified: 40, legacyDisabled: 30, blocked: 8 },

    /* —— Wave 3 —— */
    { id: "C-W3-01", wave: "w3", criticality: "Business-Critical", privilege: "Privileged", department: "Platform Engineering", region: "AMER", notStarted: 120, ready: 40, scheduled: 12, migrated: 8, verified: 0, legacyDisabled: 0, blocked: 12 },
    { id: "C-W3-02", wave: "w3", criticality: "Standard", privilege: "Privileged", department: "IT Operations", region: "AMER", notStarted: 110, ready: 30, scheduled: 16, migrated: 4, verified: 0, legacyDisabled: 0, blocked: 8 },
    { id: "C-W3-03", wave: "w3", criticality: "Standard", privilege: "Privileged", department: "Identity & Access", region: "AMER", notStarted: 70, ready: 20, scheduled: 8, migrated: 2, verified: 0, legacyDisabled: 0, blocked: 4 },
    { id: "C-W3-04", wave: "w3", criticality: "Business-Critical", privilege: "Privileged", department: "Security Operations", region: "AMER", notStarted: 56, ready: 16, scheduled: 6, migrated: 2, verified: 0, legacyDisabled: 0, blocked: 6 },

    /* —— Wave 4 —— */
    { id: "C-W4-01", wave: "w4", criticality: "Executive", privilege: "Elevated", department: "Executive Office", region: "AMER", notStarted: 58, ready: 14, scheduled: 0, migrated: 0, verified: 0, legacyDisabled: 0, blocked: 0 },
    { id: "C-W4-02", wave: "w4", criticality: "Executive", privilege: "Elevated", department: "Board & Governance", region: "AMER", notStarted: 40, ready: 8, scheduled: 0, migrated: 0, verified: 0, legacyDisabled: 0, blocked: 0 },

    /* —— Wave 5 —— */
    { id: "C-W5-01", wave: "w5", criticality: "Non-Human", privilege: "Privileged", department: "Platform Engineering", region: "AMER", notStarted: 520, ready: 80, scheduled: 20, migrated: 0, verified: 0, legacyDisabled: 0, blocked: 12 },
    { id: "C-W5-02", wave: "w5", criticality: "Non-Human", privilege: "Standard", department: "Shared Services", region: "AMER", notStarted: 400, ready: 60, scheduled: 20, migrated: 0, verified: 0, legacyDisabled: 0, blocked: 8 },
    { id: "C-W5-03", wave: "w5", criticality: "Non-Human", privilege: "Standard", department: "Partner Federation", region: "AMER", notStarted: 280, ready: 32, scheduled: 8, migrated: 0, verified: 0, legacyDisabled: 0, blocked: 4 }
  ],

  /* 20 applications. */
  applications: [
    { id: "APP-01", name: "Nexus Identity Admin Console", tier: 0, protocol: "OIDC", wave: "w0", status: "Verified", sox: false, owner: "Priya N. (IAM)" },
    { id: "APP-02", name: "Privileged Access Gateway", tier: 0, protocol: "SAML", wave: "w3", status: "Not Started", sox: true, owner: "Omar H. (Security)" },
    { id: "APP-03", name: "Directory Sync Fabric", tier: 0, protocol: "LDAP", wave: "w0", status: "Verified", sox: false, owner: "Priya N. (IAM)" },
    { id: "APP-04", name: "VPN / Zero Trust Edge", tier: 0, protocol: "SAML", wave: "w1", status: "Cut Over", sox: false, owner: "Jonah K. (Network)" },
    { id: "APP-05", name: "Core Banking Platform", tier: 1, protocol: "SAML", wave: "w2", status: "In Dual-Run", sox: true, owner: "Sofia M. (Wealth Eng)" },
    { id: "APP-06", name: "Trading Workstation", tier: 1, protocol: "SAML", wave: "w2", status: "In Dual-Run", sox: true, owner: "Wei C. (Markets Eng)" },
    { id: "APP-07", name: "Payments Hub", tier: 1, protocol: "OIDC", wave: "w2", status: "Not Started", sox: true, owner: "Ana B. (Payments)" },
    { id: "APP-08", name: "Client Portal", tier: 1, protocol: "OIDC", wave: "w2", status: "In Dual-Run", sox: false, owner: "Lisa G. (Client Platform)" },
    { id: "APP-09", name: "General Ledger", tier: 1, protocol: "SAML", wave: "w1", status: "Cut Over", sox: true, owner: "Derek L. (Finance Systems)" },
    { id: "APP-10", name: "Regulatory Reporting Suite", tier: 1, protocol: "SAML", wave: "w2", status: "Not Started", sox: true, owner: "Hannah P. (Compliance Tech)" },
    { id: "APP-11", name: "HRIS", tier: 2, protocol: "SAML", wave: "w1", status: "Cut Over", sox: false, owner: "Elena R. (HR Tech)" },
    { id: "APP-12", name: "Service Desk", tier: 2, protocol: "OIDC", wave: "w0", status: "Verified", sox: false, owner: "Ravi S. (ITSM)" },
    { id: "APP-13", name: "Expense & Travel", tier: 2, protocol: "OIDC", wave: "w1", status: "Cut Over", sox: false, owner: "Derek L. (Finance Systems)" },
    { id: "APP-14", name: "Collaboration Suite", tier: 2, protocol: "OIDC", wave: "w1", status: "Cut Over", sox: false, owner: "Marcus T. (IT Ops)" },
    { id: "APP-15", name: "Document Management", tier: 2, protocol: "SAML", wave: "w1", status: "In Dual-Run", sox: false, owner: "Nina F. (Operations)" },
    { id: "APP-16", name: "CRM / Advisor Desktop", tier: 2, protocol: "OIDC", wave: "w2", status: "Not Started", sox: false, owner: "Sofia M. (Wealth Eng)" },
    { id: "APP-17", name: "Intranet / Wiki", tier: 3, protocol: "OIDC", wave: "w1", status: "Cut Over", sox: false, owner: "Chris V. (Internal Comms)" },
    { id: "APP-18", name: "Facilities Badging", tier: 3, protocol: "LDAP", wave: "w1", status: "In Dual-Run", sox: false, owner: "Nina F. (Facilities)" },
    { id: "APP-19", name: "Learning Management", tier: 3, protocol: "SAML", wave: "w1", status: "Deferred", sox: false, owner: "Elena R. (HR Tech)" },
    { id: "APP-20", name: "Vendor Portal (legacy)", tier: 3, protocol: "Legacy", wave: "w5", status: "Not Started", sox: false, owner: "Ana B. (Procurement Systems)" }
  ],

  /* 12 risks. 5 Open, 5 Mitigating, 2 Watch. 3 have decisionNeeded: true. */
  risks: [
    { id: "RISK-01", headline: "Privileged session recording gap on Nexus", description: "Wave 3 cannot start until interactive privileged sessions are recorded end-to-end on Nexus. Vendor selection is still open.", wave: "w3", severity: "Critical", status: "Open", rag: "Red", owner: "Omar H. (Security)", due: "2026-09-18", decisionNeeded: true, decision: "Approve the privileged session-recording vendor so Wave 3 can keep its September 21 start." },
    { id: "RISK-02", headline: "Contingent workforce MFA exception backlog", description: "AMER and EMEA contractors are stacking MFA exceptions, which is the main Wave 1 fallout driver.", wave: "w1", severity: "High", status: "Mitigating", rag: "Amber", owner: "Elena R. (HR Tech)", due: "2026-09-05", decisionNeeded: false, decision: "" },
    { id: "RISK-03", headline: "Core Banking SAML assertion mapping drift", description: "Dual-run on Core Banking is showing role-claim mismatches versus LegacyID group maps.", wave: "w2", severity: "High", status: "Mitigating", rag: "Amber", owner: "Sofia M. (Wealth Eng)", due: "2026-09-12", decisionNeeded: false, decision: "" },
    { id: "RISK-04", headline: "EMEA works-council notification lag", description: "EMEA contingent cutover is paused pending works-council acknowledgement of the identity-platform change.", wave: "w1", severity: "High", status: "Open", rag: "Red", owner: "Legal / HR (Elena R.)", due: "2026-09-01", decisionNeeded: true, decision: "Proceed with EMEA contingent cutover without works-council ACK, or slip Wave 1 EMEA to September 19." },
    { id: "RISK-05", headline: "Service-account password-rotation window too short", description: "NHI owners say the proposed 14-day rotation window will break batch jobs during Wave 5.", wave: "w5", severity: "High", status: "Open", rag: "Amber", owner: "Platform Engineering (Wei C.)", due: "2026-10-31", decisionNeeded: false, decision: "" },
    { id: "RISK-06", headline: "Dual-run token lifetime mismatch", description: "Nexus access-token lifetime is shorter than LegacyID, causing mid-session drops on dual-run Tier 1 apps.", wave: "w2", severity: "Medium", status: "Mitigating", rag: "Amber", owner: "Priya N. (IAM)", due: "2026-09-08", decisionNeeded: false, decision: "" },
    { id: "RISK-07", headline: "APAC device-compliance telemetry gap", description: "APAC Operations endpoints are under-reporting MDM compliance, which blocks Ready → Scheduled.", wave: "w1", severity: "Medium", status: "Open", rag: "Amber", owner: "Endpoint (Marcus T.)", due: "2026-09-10", decisionNeeded: false, decision: "" },
    { id: "RISK-08", headline: "Executive white-glove runbook incomplete", description: "Wave 4 weekend runbook is missing concierge staffing and a named rollback commander.", wave: "w4", severity: "Medium", status: "Open", rag: "Amber", owner: "PMO (Nina F.)", due: "2026-10-10", decisionNeeded: true, decision: "Lock the executive cutover weekend of November 7–8 and name the rollback commander." },
    { id: "RISK-09", headline: "Partner federation metadata stale", description: "Three federated partners have not rotated signing certificates since 2025.", wave: "w5", severity: "Medium", status: "Watch", rag: "Amber", owner: "Priya N. (IAM)", due: "2026-11-02", decisionNeeded: false, decision: "" },
    { id: "RISK-10", headline: "SOX control evidence pack not signed", description: "Wave 2 exit requires a signed SOX pack covering assertion mapping, joiner/mover/leaver, and access recert.", wave: "w2", severity: "Medium", status: "Mitigating", rag: "Amber", owner: "GRC (Hannah P.)", due: "2026-10-03", decisionNeeded: false, decision: "" },
    { id: "RISK-11", headline: "Helpdesk surge staffing for Wave 2", description: "Service desk model assumes +18% ticket volume during Wave 2 dual-run; overtime roster is only 70% filled.", wave: "w2", severity: "Low", status: "Mitigating", rag: "Green", owner: "Ravi S. (ITSM)", due: "2026-09-04", decisionNeeded: false, decision: "" },
    { id: "RISK-12", headline: "LegacyID license true-down schedule", description: "Procurement needs a December true-down quantity once Wave 5 inventory is final.", wave: "w5", severity: "Low", status: "Watch", rag: "Green", owner: "Procurement (Ana B.)", due: "2026-12-04", decisionNeeded: false, decision: "" }
  ],

  readiness: [
    { id: "RDY-01", name: "MFA enrollment", percent: 78, target: 95, owner: "IAM" },
    { id: "RDY-02", name: "Device compliance", percent: 71, target: 90, owner: "Endpoint" },
    { id: "RDY-03", name: "Manager attestation of access", percent: 64, target: 100, owner: "App owners" },
    { id: "RDY-04", name: "Application dependency mapping", percent: 82, target: 100, owner: "Architecture" },
    { id: "RDY-05", name: "Fallback / break-glass tested", percent: 45, target: 100, owner: "Security" },
    { id: "RDY-06", name: "Communications acknowledged", percent: 69, target: 95, owner: "Change management" },
    { id: "RDY-07", name: "Helpdesk playbook certified", percent: 88, target: 100, owner: "Service desk" },
    { id: "RDY-08", name: "Legacy password-hash export freeze", percent: 100, target: 100, owner: "IAM" }
  ],

  milestones: [
    { id: "M1", name: "Dual-run architecture live", date: "2026-06-15", status: "Complete" },
    { id: "M2", name: "Wave 0 gate review (Go)", date: "2026-06-26", status: "Complete" },
    { id: "M3", name: "Wave 1 gate review (Go with conditions)", date: "2026-07-24", status: "Complete" },
    { id: "M4", name: "Wave 2 gate review", date: "2026-09-04", status: "Upcoming" },
    { id: "M5", name: "Privileged control attestation", date: "2026-09-18", status: "Upcoming" },
    { id: "M6", name: "Wave 3 gate review", date: "2026-10-16", status: "Upcoming" },
    { id: "M7", name: "Executive white-glove weekend", date: "2026-11-07", status: "Upcoming" },
    { id: "M8", name: "LegacyID decommission decision", date: "2026-12-04", status: "Upcoming" },
    { id: "M9", name: "LegacyID contract end / true-down", date: "2026-12-31", status: "Upcoming" }
  ],

  /*
   * LegacyID accounts still active (not yet legacyDisabled).
   * August actualRemaining MUST equal totalIdentities - sum(legacyDisabled) = 9,280.
   * June / July are historical snapshots. Sep–Dec are forecast only (actualRemaining: null).
   */
  decommissionBurndown: [
    { month: "2026-06", label: "Jun", actualRemaining: 12160, forecastRemaining: 12100 },
    { month: "2026-07", label: "Jul", actualRemaining: 10840, forecastRemaining: 10600 },
    { month: "2026-08", label: "Aug", actualRemaining: 9280, forecastRemaining: 8800 },
    { month: "2026-09", label: "Sep", actualRemaining: null, forecastRemaining: 6200 },
    { month: "2026-10", label: "Oct", actualRemaining: null, forecastRemaining: 4100 },
    { month: "2026-11", label: "Nov", actualRemaining: null, forecastRemaining: 1800 },
    { month: "2026-12", label: "Dec", actualRemaining: null, forecastRemaining: 0 }
  ]
};
```

### 3.1 Pre-reconciled reference totals (for your self-check — compute, do not hard-code in UI)

**Funnel (all 26 cohorts):**

| Stage | Count |
|---|---:|
| Not Started | **2,774** |
| Ready | **1,560** |
| Scheduled | **1,290** |
| Migrated | **1,710** |
| Verified | **1,946** |
| Legacy Disabled | **3,120** |
| **Total identities** | **12,400** |
| On Nexus (Migrated + Verified + Legacy Disabled) | **6,776** (54.6%) |
| Blocked overlay | **328** |

**Per wave (population / on Nexus / %):**

| Wave | Identities | On Nexus | % | Blocked |
|---|---:|---:|---:|---:|
| Wave 0 | 280 | 280 | 100% | 0 |
| Wave 1 | 7,420 | 5,440 | 73.3% | 166 |
| Wave 2 | 2,640 | 1,040 | 39.4% | 108 |
| Wave 3 | 520 | 16 | 3.1% | 30 |
| Wave 4 | 120 | 0 | 0% | 0 |
| Wave 5 | 1,420 | 0 | 0% | 24 |

**Criticality / privilege / region:**

| Slice | Identities |
|---|---:|
| Standard | 6,560 |
| Business-Critical | 2,900 |
| Contingent | 1,400 |
| Non-Human | 1,420 |
| Executive | 120 |
| Privilege: Standard | 10,860 |
| Privilege: Elevated | 320 |
| Privilege: Privileged | 1,220 |
| AMER | 10,260 |
| EMEA | 1,600 |
| APAC | 540 |

**Applications (20):** Verified 3 · Cut Over 6 · In Dual-Run 5 · Deferred 1 · Not Started 5. **On Nexus apps (Cut Over + Verified) = 9.** SOX-relevant = 6.

**Risks (12):** Open 5 · Mitigating 5 · Watch 2 · Critical 1 · High 4 · `decisionNeeded` 3.

**Waves complete:** 1 of 6 (Wave 0 only).

**August LegacyID remaining:** 12,400 − 3,120 = **9,280** (must match `decommissionBurndown` August `actualRemaining`).

---

## 4. App Shell & Shared Helpers

### 4.1 HTML structure

```
header
  title row (CutoverDesk, DEMO badge, LegacyID → Nexus Identity, window, today)
  tablist (5 buttons)
main
  #panel-overview
  #panel-waves
  #panel-identities
  #panel-applications
  #panel-risks
popover / modal root (for wave + milestone + cohort detail)
footer line with DATA.meta.disclaimer
```

Only one panel visible at a time. Tabs use `role="tab"` / `aria-selected`. **Default tab: Overview.**

### 4.2 Required helpers

```js
function parseDate(iso) { /* Date at UTC noon to avoid TZ shift */ }
function formatDate(iso) { /* "Aug 26, 2026" */ }
function formatInt(n) { /* 12400 → "12,400" */ }
function formatPct(ratio) { /* 0.54645 → "54.6%"; 1 → "100%" */ }
function daysBetween(a, b) { /* inclusive calendar math for Gantt */ }
function waveMeta(id) { /* lookup DATA.waves */ }
function waveColor(id) { /* lookup color */ }
function pill(label, bg, fg) { /* HTML string or element */ }

function cohortTotal(c) {
  return c.notStarted + c.ready + c.scheduled + c.migrated + c.verified + c.legacyDisabled;
}
function cohortOnNexus(c) {
  return c.migrated + c.verified + c.legacyDisabled;
}
function sumBy(arr, fn) { return arr.reduce((n, x) => n + fn(x), 0); }

function waveCohorts(waveId) {
  return DATA.cohorts.filter(c => c.wave === waveId);
}
function wavePopulation(waveId) {
  return sumBy(waveCohorts(waveId), cohortTotal);
}
function waveOnNexus(waveId) {
  return sumBy(waveCohorts(waveId), cohortOnNexus);
}
function waveBlocked(waveId) {
  return sumBy(waveCohorts(waveId), c => c.blocked);
}

function waveRag(wave) {
  const pct = waveOnNexus(wave.id) / wavePopulation(wave.id);
  if (wave.status === "Complete") return "green";
  if (wave.status === "In Progress") {
    if (pct >= 0.60) return "green";
    if (pct >= 0.25) return "amber";
    return "red";
  }
  /* Planned */
  return wave.start > DATA.meta.today ? "green" : "amber";
}

function appOnNexus(a) {
  return a.status === "Cut Over" || a.status === "Verified";
}

function readinessRag(item) {
  if (item.percent >= item.target) return "green";
  if (item.percent >= item.target - 15) return "amber";
  return "red";
}
```

Add a defensive `console.warn` (do not surface in UI) if any cohort's six status columns do not match a recomputed total, if grand total ≠ 12,400, or if August `actualRemaining` ≠ `12400 - sum(legacyDisabled)`. These should never fire if DATA is copied verbatim.

---

## 5. Tab 1 — Overview (default)

This is the “understand in ten seconds” tab. Lead with numbers, not tables.

### 5.1 Five KPI cards (single row, wrap on small screens)

Compute from DATA:

| Card | Value |
|---|---|
| Identities on Nexus | `sum(cohortOnNexus)` / `sum(cohortTotal)` plus `formatPct` — **6,776 / 12,400 (54.6%)** |
| Apps cut over | `applications.filter(appOnNexus).length` / `applications.length` — **9 / 20 (45%)** |
| Waves complete | `waves.filter(w => w.status === "Complete").length` / `waves.length` — **1 / 6** |
| Blocked / fallout | `sum(c.blocked)` — **328** (danger tint) |
| LegacyID decommissioned | `sum(c.legacyDisabled)` — **3,120** |

Card anatomy: gold top edge, large number, small muted label, optional sub-line (e.g. “Migrated + Verified + Legacy disabled”).

### 5.2 Legend + health line

Under the KPI row:

1. The one-line “How to read” legend from Section 1.
2. A **program health** sentence built from live figures — do not hard-code the percents:

```text
Wave 0 is complete. Wave 1 is {w1pct} on Nexus with contingent MFA fallout.
Wave 2 is in dual-run at {w2pct}. {blocked} identities are blocked.
Wave 3 (privileged) is gated on session recording.
```

### 5.3 Overall progress

Full-width ivory card:

- Label: “Program progress · identities on Nexus”
- Bar: gold fill, width = onNexus / total
- Caption: `{formatInt(onNexus)} of {formatInt(total)} identities`

### 5.4 Per-wave progress (six rows)

For each wave in `DATA.waves` order:

- Color dot + wave name + audience (muted, one line)
- Status pill + RAG pip from `waveRag`
- Bar using the wave color, width = waveOnNexus / wavePopulation
- Right-side figures: `{onNexus}/{pop} · {pct}` and, if blocked > 0, a small red “{n} blocked”

Wave 0 must read 100% green Complete. Wave 1 green (~73.3%). Wave 2 amber (~39.4%). Waves 3–5 Planned with near-zero / zero fill.

---

## 6. Tab 2 — Waves (Gantt)

### 6.1 Layout

- Horizontal scroll if needed; left sticky column ~300px
- Time axis: `windowStart` → `windowEnd` (Jun–Dec 2026)
  - Top: month headers **Jun · Jul · Aug · Sep · Oct · Nov · Dec**
  - Faint week or month gridlines
  - Vertical **today** line at `DATA.meta.today` (Aug 26), labeled “Today”
- Top track: nine milestone diamonds from `DATA.milestones`, positioned by `date`. Complete = gold filled; Upcoming = ivory outline. Click → popover (name, formatted date, status).
- Six wave rows in `DATA.waves` order:
  - Left: **name**, muted audience, `{n} identities` (from cohorts)
  - Bar: start/end as % of program window, fill = wave color, height 26–32px, rounded. Implement as a `<button>` (not a div) with an `aria-label` such as “Wave 2 — Business-critical users, Aug 4 to Oct 17, In Progress”. Milestone diamonds are also buttons with `aria-label` (name, formatted date, status).
  - Completed portion (optional inner shade): width = onNexus% of the bar, darker/navy overlay at ~35% opacity — only if easy; otherwise the Overview bars already show %

### 6.2 Click wave → detail popover

| Field | Source |
|---|---|
| Name + color pip | wave |
| Audience | wave.audience |
| Window | formatDate(start) – formatDate(end) |
| Status | pill |
| RAG | waveRag |
| Definition | wave.definition |
| Entry criteria | ul of entryCriteria |
| Exit criteria | ul of exitCriteria |
| Identities | population, on Nexus, %, blocked — all from cohorts |
| Example identities | wave.examples (name, role, status) |

Close via ✕, Escape, or click-outside. On open, save `document.activeElement` and move focus to the close button. On close, restore focus. Trap Tab / Shift+Tab inside the dialog.

### 6.3 Implementation note

Use CSS grid or absolute positioning inside a relatively positioned track. **Do not** pull in a third-party Gantt library.

---

## 7. Tab 3 — Identities

### 7.1 Funnel strip (six stage cards)

Stages in this exact order, summing `DATA.cohorts` fields:

`notStarted` · `ready` · `scheduled` · `migrated` · `verified` · `legacyDisabled`

Each card: stage label, `formatInt(count)`, `formatPct(count / total)`. The six counts **must sum to 12,400**.

### 7.2 Chart.js bar

Ivory card with a Chart.js **bar** chart of the same six stages, colors from Section 2.3 (Identity funnel). Y-axis starts at 0. No animation required. Title: “Migration funnel”. Set `maintainAspectRatio: false` so the chart fills a fixed-height container (~260px). If `Chart` is undefined (CDN failed / offline), replace the canvas with the muted message “Chart unavailable offline — data in cards above” — do **not** throw.

### 7.3 Wave × criticality matrix

Rows = `DATA.waves` (preserve order).  
Columns = `["Executive", "Business-Critical", "Standard", "Contingent", "Non-Human"]`.

Each cell:

```js
const cellCohorts = DATA.cohorts.filter(c => c.wave === waveId && c.criticality === tier);
const pop = sumBy(cellCohorts, cohortTotal);
const on = sumBy(cellCohorts, cohortOnNexus);
```

Show `formatInt(pop)` (or `0` if empty). Tint background by `on/pop` (0% = ivory, 100% = wave color at ~40% opacity). Show `{formatPct}` as a **visible** subtitle inside cells that have population (not `title`-only).

Row header includes wave color pip. Column headers are criticality names. Append a derived **totals column** (per wave) and **totals row** (per criticality plus grand total).

### 7.4 Cohort register

Full-width table of all 26 cohorts, grouped by wave (wave header row with color + population). Columns:

| Column | Source |
|---|---|
| ID | `id` (mono) |
| Department | `department` |
| Region | `region` |
| Criticality | pill |
| Privilege | pill |
| Population | `cohortTotal` |
| On Nexus | `cohortOnNexus` + % |
| Blocked | `blocked` (red if > 0) |
| Funnel | compact `NS/R/S/M/V/LD` counts |

Clicking a cohort row may open a small popover repeating those fields. Optional; table alone is acceptable.

Every cohort appears exactly once. 26 rows plus 6 wave headers.

---

## 8. Tab 4 — Applications

### 8.1 Four stat cards

| Card | Filter |
|---|---|
| Cut over (on Nexus) | `appOnNexus` → **9** |
| In dual-run | `status === "In Dual-Run"` → **5** |
| Not started | `status === "Not Started"` → **5** |
| Deferred | `status === "Deferred"` → **1** |

Also show a muted “{n} SOX-relevant” from `applications.filter(a => a.sox).length` (**6**) near the cards.

### 8.2 Chart.js doughnut

Small ivory card: doughnut of the five app statuses (Verified, Cut Over, In Dual-Run, Deferred, Not Started) with Section 2.3 colors. Center text = `applications.length` (**20**). Implement center text with a Chart.js `beforeDraw` / `afterDraw` plugin. Set `maintainAspectRatio: false`. If `Chart` is undefined, show “Chart unavailable offline — data in cards above” instead of throwing.

### 8.3 Grouped register

Group by `tier` 0 → 3. Section header: **Tier {n}** + count + short hint:

| Tier | Hint |
|---|---|
| 0 | Identity and edge infrastructure |
| 1 | Business-critical / SOX-adjacent |
| 2 | Enterprise productivity |
| 3 | Long-tail and legacy |

Each app row:

- **Name** (bold) + `APP-XX` (muted mono)
- Protocol chip
- Wave chip (wave color + shortName)
- Status pill
- SOX chip if `sox` — gold **outline** chip (transparent fill, gold border, navy text, label “SOX”). Do **not** render SOX as a solid gold pill.
- Owner

All 20 applications appear exactly once.

---

## 9. Tab 5 — Risks & Readiness

### 9.1 Four stat cards

| Card | Value |
|---|---|
| Total risks | `risks.length` → **12** |
| Open | `status === "Open"` → **5** (danger tint) |
| Mitigating | `status === "Mitigating"` → **5** |
| Critical + High | severity in `["Critical","High"]` → **5** |

### 9.2 Decisions needed

Filter `risks.filter(r => r.decisionNeeded)`. Three ivory callout cards (gold left border):

- RISK id + headline
- Decision text (`r.decision`)
- Owner · due `formatDate(due)` · severity pill

### 9.3 Readiness coverage

For each `DATA.readiness` item: name, owner, bar (gold if `percent >= target`, else wave-blue/amber/red via `readinessRag`), caption `{percent}% of {target}%`. Eight rows. RDY-08 is the only green-at-target row (100/100).

### 9.4 LegacyID decommission burndown

Chart.js **line** chart from `DATA.decommissionBurndown`:

- X = `label` (Jun–Dec)
- Dataset A: `actualRemaining` (gold, skip nulls — Jun/Jul/Aug only)
- Dataset B: `forecastRemaining` (ivory/navy dashed, all seven points)
- Y starts at 0; title: “LegacyID accounts still active”
- Caption under chart, computed: “August actual {formatInt(aug.actualRemaining)} must equal identities not yet legacy-disabled ({formatInt(total - sum(legacyDisabled))}).”
- Set `maintainAspectRatio: false` so the line chart fills a fixed-height container (~300px). If `Chart` is undefined, show “Chart unavailable offline — data in cards above” instead of throwing.

### 9.5 Risk register

Table or stacked cards, grouped by severity (Critical → Low). Each row:

- `RISK-XX` mono chip
- Headline + description
- Wave chip
- Severity pill + status pill + RAG pip
- Owner
- Due `formatDate` — if `due < today` and status is Open, emphasize in red (with this DATA, no due date is before Aug 26; still implement the rule)

All 12 risks appear exactly once. No lorem. Use the headlines/descriptions from DATA.

---

## 10. Consistency Rules (non-negotiable)

1. Embed `DATA` from Section 3 **verbatim**.
2. Funnel six stages sum to `sum(cohortTotal)` = 12,400 on every tab that shows a total.
3. Overview “on Nexus” = Migrated + Verified + Legacy Disabled = 6,776. Never treat `blocked` as part of that sum.
4. `blocked` is overlay only; for every cohort, `blocked <= notStarted + ready + scheduled`.
5. Per-wave population on Overview, Gantt, and matrix row totals all equal `wavePopulation(id)`.
6. Apps on Nexus (Overview + Applications cards) = Cut Over + Verified = 9.
7. Waves complete = count of `status === "Complete"` = 1.
8. August burndown `actualRemaining` equals `totalIdentities - sum(legacyDisabled)`.
9. Wave colors identical across Overview bars, Gantt, chips, matrix tints, and any charts.
10. All user-visible dates use `formatDate` (`Aug 26, 2026`), not raw ISO.
11. DEMO / Synthetic badge always visible.
12. No placeholder “lorem” text — use DATA copy (definitions, criteria, risk prose, example identities).
13. Default tab is Overview.

---

## 11. Acceptance Checklist (run before you finish)

- [ ] Single HTML file opens locally with Chart.js from CDN
- [ ] Five tabs switch panels without page reload; default is Overview
- [ ] Overview KPIs read **6,776 / 12,400 (54.6%)**, **9 / 20**, **1 / 6**, **328**, **3,120**
- [ ] Overall bar and six wave bars match those derived percents; Wave 0 green 100%, Wave 1 green ~73.3%, Wave 2 amber ~39.4%
- [ ] Health line uses live Wave 1 / Wave 2 percents and the live blocked count
- [ ] Gantt shows 6 wave bars, 9 milestones, month headers Jun–Dec, today line on Aug 26, 2026
- [ ] Wave bars and milestone diamonds are keyboard-focusable buttons with aria-labels; Enter/Space opens the popover
- [ ] Popover moves focus to Close on open, restores prior focus on close, and traps Tab inside the dialog
- [ ] Clicking a wave opens a popover with criteria, derived counts, and example identities
- [ ] Identity funnel cards sum to 12,400 (2,774 / 1,560 / 1,290 / 1,710 / 1,946 / 3,120)
- [ ] Matrix has 6 rows × 5 criticality columns plus totals row/column; Executive total 120, Non-Human total 1,420, Wave 0 only under Standard (280); cell % is visible
- [ ] Charts use `maintainAspectRatio: false`; if Chart.js is missing, a muted fallback message appears and the console stays clean
- [ ] Cohort table lists all 26 cohorts exactly once
- [ ] Applications: 20 rows, grouped by tier; doughnut center 20; cards 9 / 5 / 5 / 1
- [ ] Risks: cards 12 / 5 / 5 / 5; three decision callouts (RISK-01, RISK-04, RISK-08); eight readiness bars; burndown has gold actual through Aug and dashed forecast through Dec
- [ ] DEMO badge and disclaimer visible; no console errors in a clean browser session

---

## 12. Suggested File Skeleton (follow closely)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>CutoverDesk — Meridian Financial Identity Migration</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.min.js"></script>
  <style>/* navy/gold shell + tabs + ivory cards + gantt + pills + matrix */</style>
</head>
<body>
  <!-- header + tabs + 5 panels + popover + footer disclaimer -->
  <script>
    const DATA = { /* verbatim from Section 3 */ };

    /* helpers */
    /* tab wiring */
    /* renderOverview() */
    /* renderWaves() + Gantt + popover */
    /* renderIdentities() + Chart.js bar + matrix */
    /* renderApplications() + Chart.js doughnut */
    /* renderRisks() + Chart.js burndown */
    /* boot: render all, show overview */
  </script>
</body>
</html>
```

---

## 13. Final Instruction to Grok

Generate the **complete** HTML now. Prefer a polished, executive-ready visual density — compact but readable, suitable for a standing IAM program review. An exec should grasp overall status from Tab 1 without scrolling past the wave bars.

Do not ask clarifying questions; the dataset and behavior are fully specified. If anything is ambiguous, choose the simplest interpretation that preserves numeric reconciliation with `DATA`.
