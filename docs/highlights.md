# CutoverDesk highlights

**Live:** [cutoverdesk-fpl.vercel.app](https://cutoverdesk-fpl.vercel.app/)

## Overview

CutoverDesk is a TPM-lens command center for an enterprise identity-platform migration. It answers: how is the cutover actually going, by wave, criticality, privilege, and application?

## Problem

Identity migrations stall because leadership sees either a spreadsheet of 12,000 rows or a slide that says “on track.” App owners, service desk, and security need the same simple status: who has moved, who is blocked, and which gates are still open.

## What it does

- Derives every KPI from a single synthetic `DATA` object (12,400 identities, 20 apps, 12 risks).
- Sequences six waves from lowest blast-radius (pilot) to hardest (non-human identities).
- Surfaces blocked/fallout as an overlay, not a fake seventh funnel stage.
- Makes wave-gate decisions and SOX-relevant apps visible without a live directory.

## Engine thesis

Deterministic first. Status is math over cohort counts (`On Nexus = Migrated + Verified + Legacy disabled`). RAG colors are rules, not a model.

## Security highlights

Read-only, synthetic-only, no secrets, no write endpoints. See [SECURITY.md](../SECURITY.md).
