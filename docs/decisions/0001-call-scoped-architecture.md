# ADR 0001: Call-scoped state and backend boundaries

Status: Accepted (2026-09-05)

## Context

Michaela previously combined prompt logic, mutable call data, webhook requests,
event persistence, appointment validation, and final export in one module. Model
arguments could select customer identifiers and persist results, while global event
state could leak information between concurrent calls.

## Decision

- `CallState` owns every call-local invariant and is attached to
  `AgentSession.userdata`.
- `EventJournal` is created per call, redacts PII, and persists only after explicit
  opt-in through `MICHAELA_EVENT_LOG_PATH`.
- `EnergyBackend` is the only boundary for customer, calendar, booking, and result
  webhooks. Production uses `N8nEnergyBackend`; tests use `FakeEnergyBackend`.
- Customer and room identifiers always come from job metadata.
- A booking requires a server-returned slot and an explicit user confirmation.
- Final results are written once from `on_session_end` with an idempotency key.
- Simple field ordering and tool exposure live in a declarative `CollectionPlan`;
  specialized conversational tasks keep their own behavior.

## Consequences

The core invariants can be tested without network or audio. External simulations,
telephony behavior, provider latency, and production webhook compatibility remain
deployment gates and are not proven by the local suite.
