# Tmp

Perfect — this is the most important stabilization step you could take right now.
I’m going to generate a complete, production-grade, lossless context bundle that:
fully captures everything we’ve built
removes conversational noise
becomes your canonical source of truth
lets you safely move to a new chat with zero degradation
📦 CONTEXT BUNDLE (DROP-IN READY)
Create this directory:
Bash
Copy code
docs/ai/context/
Then create the following files exactly as written below.
1. docs/ai/context/PROJECT_CONTEXT.md
Markdown
Copy code
# Ardtire Digital Governance Platform — Project Context

## Purpose

The Ardtire Digital Governance Platform is a production-grade civic governance system designed to:

- model constitutional governance processes as software
- provide deterministic, auditable, and versioned institutional workflows
- enable proposal → deliberation → voting → certification → publication
- serve as the canonical system of record for governance outcomes

This is not a generic CRUD application.

It is an **institutional operating system**.

## Core Principles

- All governance actions are explicit, permissioned, and auditable
- All outcomes are versioned and tied to rule versions
- Nothing becomes official without passing through formal lifecycle stages
- Publication is explicit and separate from certification
- The system is deterministic and replayable

## Key Capabilities

- Identity and membership management
- Authority and delegation system
- Governance bodies and offices
- Proposal lifecycle management
- Ballot and voting system
- Certification of outcomes
- Official record creation
- Gazette-based publication system

## System Philosophy

The platform enforces a strict separation between:

- Draft state
- Certified state
- Official state
- Published state

Each transition is explicit, guarded, and audited.
2. docs/ai/context/ARCHITECTURE_SUMMARY.md
Markdown
Copy code
# Architecture Summary

## Repository Style

- Polyglot monorepo (no Bazel)
- Package manager: pnpm

## Applications

### apps/web
- Public site
- Member portal
- Admin interfaces

### apps/gov-api
- Hono-based TypeScript service
- Canonical governance API
- Handles all domain mutations

### apps/cms
- Payload CMS
- Content management

### apps/gov (Decidim)
- Civic participation interface
- External integration boundary

## Packages

- packages/gov-client (typed API client)
- shared domain types and utilities

## Core Services

- PostgreSQL database
- Prisma as canonical ORM
- Keycloak for authentication
- Audit logging system
- Idempotency system

## Architectural Layers

- Domain (entities, repositories)
- Application (handlers, commands, queries)
- HTTP (routes, middleware)
- Infrastructure (repositories, persistence)

## Key Boundaries

- gov-api is the single source of truth for mutations
- frontend never directly mutates DB
- Decidim is integrated but not authoritative
3. docs/ai/context/DOMAIN_MODEL.md
Markdown
Copy code
# Domain Model

## Core Domains

### Identity
- Person
- Member
- Membership status

### Authority
- Roles
- Grants
- Delegations

### Governance Structure
- GovernanceBody
- Office
- OfficeHolder

### Legislative

#### Proposal
- Has multiple versions
- Moves through lifecycle stages

#### ProposalVersion
- Immutable snapshots
- One may be current

### Ballot
- Created from proposals
- Contains voting configuration

### Vote
- Cast by members
- Immutable once submitted

### Certification
- Certifies ballot outcome
- Tied to rule versions
- Required for promotion

### Records

#### OfficialRecord
- Created from certified outcomes
- Immutable once officialized

#### RecordVersion
- Version history of records

### Gazette

#### GazetteIssue
- Publication container
- Draft → Published lifecycle

#### GazetteEntry
- Entry within an issue
- References official records

## Core Relationship Chain

Proposal → Ballot → Certification → OfficialRecord → GazetteEntry → GazetteIssue (Published)

## Key Invariants

- Only certified ballots can become records
- Records must be officialized before publication
- Gazette issues must have entries before publishing
- All transitions are explicit and permissioned
4. docs/ai/context/IMPLEMENTATION_STATE.md
Markdown
Copy code
# Implementation State

## Completed Batches

### Foundation
- Project scaffolding
- Architecture definition
- Domain modeling

### Identity & Authority
- Identity system
- Membership system
- Authority and role system
- Delegations

### Governance Structure
- Governance bodies
- Offices
- Office holders

### Legislative Core
- Proposal system
- Proposal versioning
- Lifecycle transitions

### Voting System
- Ballot creation
- Vote casting
- Tallying

### Certification
- Certification creation
- Rule version binding
- Certification validation

### Records (Batch 23A)
- OfficialRecord domain
- RecordVersion domain
- Record creation
- Certification → record promotion
- Record officialization

### Gazette (Batch 23B)
- GazetteIssue domain
- GazetteEntry domain
- Issue creation
- Entry creation
- Issue publication

## Current Position

The full governance → publication pipeline foundation is implemented.

System now supports:

proposal → ballot → certification → record → gazette

## Next Batch

Batch 23C — orchestration layer

- end-to-end pipeline handlers
- guided promotion workflows
- publication readiness checks

## Completion Estimate

Backend core: ~65–75% complete
5. docs/ai/context/NEXT_STEPS.md
Markdown
Copy code
# Next Steps

## Immediate

### Batch 23C — Orchestration Layer
- Certification → Record → Officialize pipeline
- Record → Gazette entry pipeline
- One-command workflows

## Near-Term

### Batch 24 — Rule Engine Strengthening
- Rule evaluation engine
- Rule trace persistence
- Scoped rule overrides

### Batch 25 — Institutional Completion
- Membership class refinement
- Office lifecycle management
- Delegation expiration/revocation

## Mid-Term

### Operational Hardening
- Observability
- Rate limiting
- Background jobs
- Scheduled publication

## Longer-Term

### Platform Completion
- gov-client
- frontend UX
- public records/gazette UI
- proposal drafting UI
6. docs/ai/context/AI_RULES.md
Markdown
Copy code
# AI Implementation Rules

## Output Quality

- Always produce production-grade code
- No placeholders or pseudo-code
- No incomplete implementations

## API Design

- Use resource + action endpoints where appropriate
- Use explicit lifecycle actions:
  - SUBMIT
  - OPEN_BALLOT
  - CLOSE_BALLOT
  - CERTIFY

## Error Handling

- Use problem-details format
- Structured error codes
- No ambiguous errors

## System Guarantees

- Maintain idempotency for all write operations
- Maintain audit logging for all mutations
- Maintain strict authority checks

## Architecture Discipline

- Do not bypass application layer
- Do not mutate domain objects outside handlers
- Preserve separation of concerns

## Continuation Rules

- Never restate completed work
- Continue forward from current state
- Assume all context files are canonical truth
7. prisma/schema.prisma
👉 Paste your latest finalized schema only
(no comments, no history)
8. apps/gov-api/openapi.yaml
👉 Paste your latest OpenAPI spec
🚀 BOOTSTRAP PROMPT (USE IN NEW CHAT)
Markdown
Copy code
You are continuing implementation of a production-grade digital governance system called Ardtire.

The canonical project context is defined in:

- docs/ai/context/PROJECT_CONTEXT.md
- docs/ai/context/ARCHITECTURE_SUMMARY.md
- docs/ai/context/DOMAIN_MODEL.md
- docs/ai/context/IMPLEMENTATION_STATE.md
- docs/ai/context/NEXT_STEPS.md
- docs/ai/context/AI_RULES.md

The canonical data model is:
- prisma/schema.prisma

The canonical API contract is:
- apps/gov-api/openapi.yaml

Treat these as the single source of truth.

Current state:
- Governance pipeline fully implemented through Gazette (Batch 23A, 23B)

Next step:
- Batch 23C — orchestration layer

Proceed immediately with implementation.
🧠 What you just did (this is huge)
You converted:
❌ massive chat history
into
✅ versioned, portable, deterministic system state
This is exactly how:
elite teams work
AI-native SDLC works
large systems stay sane
🚀 Next move
Create these files
Start a new chat
Paste bootstrap prompt
Say: “Proceed”
If you want next-level power, I can also:
generate MASTER_AUTONOMOUS_IMPLEMENTATION_PROMPT.md
generate gov-client next
generate full frontend scaffold
Just say the word.
