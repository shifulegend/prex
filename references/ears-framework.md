# EARS Framework Reference (Easy Approach to Requirements Syntax)

Use EARS to eliminate natural-language ambiguity in `requirements.md`. Every requirement must follow one of the five patterns below (or a valid combination) so requirements map directly to automated unit, integration, and state-machine tests.

## Core Patterns

| Pattern | Keyword Syntax | Architectural Purpose | Example |
| :--- | :--- | :--- | :--- |
| **Ubiquitous** | `The [system] shall [action]` | Always-active properties and core capabilities | `The system shall encrypt all PII at rest using AES-256.` |
| **Event-Driven** | `When [trigger], the [system] shall [action]` | Responses to discrete triggers or user inputs | `When the user submits valid credentials, the system shall issue a signed JWT.` |
| **State-Driven** | `While [state], the [system] shall [action]` | Behavior active only while a condition persists | `While offline, the system shall queue pending mutations locally.` |
| **Unwanted Behavior** | `If [condition], then the [system] shall [action]` | Error handling, fault tolerance, edge cases | `If the upstream API times out, then the system shall retry up to 3 times with exponential backoff.` |
| **Optional Feature** | `Where [feature], the [system] shall [action]` | Behavior conditional on feature flags or hardware | `Where SSO is enabled, the system shall redirect login requests to the configured IdP.` |

## Complex / Combined Requirements

Combine keywords when behavior depends on both a persistent state and a discrete trigger:
- `While [state], when [trigger], the [system] shall [action]`
- Example: `While the application is offline, when the user clicks Sync, the system shall display a queued-for-sync status banner.`

## Test Mapping Rules

- **Event-Driven** → Integration tests with explicit trigger inputs.
- **State-Driven** → State-machine / lifecycle tests.
- **Unwanted Behavior** → Boundary-condition and failure-injection unit tests.
