---
sidebar_position: 2
tags:
  - Reference
  - Day-2
---

# Static Site : Deployments

---

## Workflow: Pull Request Ready for Review

```mermaid
sequenceDiagram
  autonumber
  participant DEV
  participant IDP
  participant PIPELINE
  participant INFRA
  DEV ->> IDP: Dispatch (Pull Request)
  IDP ->> IDP: Orchestrator logic
  Note right of IDP: Env: SBX
  Note right of IDP: Lifespan: Ephemeral
  Note right of IDP: Pattern: New
  Note right of IDP: Target: Surge.sh
  IDP ->> INFRA: Continous deployment for context
  create participant TARGET
  INFRA ->> TARGET: Create
  INFRA ->> TARGET: Deploy
  INFRA ->> IDP: URL for Site
  IDP ->> PIPELINE: Common PDT (SBX)
  IDP ->> DEV: Specific PDT (SBX)
  IDP ->> DEV: Add comments to PR
  DEV ->> DEV: Pull Request Review
  DEV ->> IDP: <br/><br/>Dispatch (PR Merged)
  IDP ->> INFRA: Request delete
  destroy TARGET
  INFRA ->> TARGET: Delete
  Note right of IDP: End
```

---

## Workflow: Clean up ephemeral environments

```mermaid
sequenceDiagram
  autonumber
  participant DEV
  participant IDP
  participant PIPELINE
  participant INFRA
  participant TARGET
  IDP ->> IDP: Schedule: <br/>Check for old ephemeral environments
  IDP ->> INFRA: Delete any old envionrments
  INFRA ->> TARGET: Delete
  Note right of IDP: End
```

---

## Workflow: Commit/merge to trunk

```mermaid
sequenceDiagram
  autonumber
  participant DEV
  participant IDP
  participant PIPELINE
  participant INFRA
  participant TARGET
  DEV ->> IDP: Dispatch (Push to Trunk)
  IDP ->> IDP: Orchestrator logic
  Note right of IDP: Env: CI
  Note right of IDP: Lifespan: Isolated
  Note right of IDP: Pattern: Overwrite
  Note right of IDP: Target: GHP on Repo
  IDP ->> INFRA: Continous deployment for context
  INFRA ->> TARGET: Dispatch (Deploy)
  TARGET ->> TARGET: Deploy
  Note over IDP,TARGET: ISSUE - Can't do PDT until deployed
  IDP ->> PIPELINE: Common PDT (CI)
  IDP ->> DEV: Specific PDT (CI)
  IDP ->> IDP: Dispatch (STG Deploy)
  Note right of IDP: End
```

---

## Workflow: Dispatch for STG deployment

```mermaid
sequenceDiagram
  autonumber
  participant DEV
  participant IDP
  participant PIPELINE
  participant INFRA
  participant TARGET
  IDP ->> IDP: Dispatch (STG Deploy)
  IDP ->> IDP: Orchestrator logic
  Note right of IDP: Env: STG
  Note right of IDP: Lifespan: Integrated
  Note right of IDP: Pattern: Overwrite
  Note right of IDP: Target: Vercel
  IDP ->> INFRA: Continous deployment for context
  INFRA ->> TARGET: Deploy
  IDP ->> PIPELINE: Common PDT (CI)
  IDP ->> DEV: Specific PDT (CI)
  IDP ->> IDP: Dispatch (PRD Deploy)
  Note right of IDP: End
```

---

## Workflow: Blue/green deployments for PRD

```mermaid
sequenceDiagram
  autonumber
  participant DEV
  participant IDP
  participant PIPELINE
  participant INFRA
  participant TARGET
  IDP ->> IDP: Schedule: <br/>Check for old ephemeral environments
  IDP ->> INFRA: Delete any old envionrments
  INFRA ->> TARGET: Delete
  Note right of IDP: End
```
