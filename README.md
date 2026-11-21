# neatsprint-contracts

Versioned API and event contracts for NeatSprint. **This repository is the source of truth**
for interfaces; services generate their OpenAPI from code and CI fails on drift.

| Path | Contents |
| :--- | :--- |
| `openapi/common.yaml` | Shared schemas (problem details, pagination, security), parameters, responses |
| `openapi/iam.yaml` | Identity, session, users, roles, invitations |
| `openapi/core.yaml` | Tenants, plans, applications, settings |
| `asyncapi/events.yaml` | Domain events published through the outbox |
| `.spectral.yaml` | Lint rules |

Service contracts (`task`, `team`, `worklog`, `monitoring`, `reports`, `chat`, `ai`) are added in
their milestone and follow `common.yaml` conventions.

## Commands

```bash
npm install
npm run lint          # OpenAPI lint (fails on warnings)
```

Or without installing: `npx --yes @stoplight/spectral-cli lint "openapi/*.yaml"`.

## Rules

1. Additive changes only within `/api/v1`; breaking changes require a major version and an ADR.
2. Every operation has an `operationId`, a tag and a non-empty description.
3. Every error response uses `common.yaml#/components/schemas/ProblemDetail`.
4. Every tenant-scoped resource documents that foreign ids return `404`.
5. Update `docs/API_SPEC.md` in the platform repo in the same change.

## Versioning

SemVer. Consumers pin a tag (`v0.1.0`). The platform's `docs/DECISIONS.md` records interface
decisions.
