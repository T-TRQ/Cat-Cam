# ADR-0001: Record architecture decisions

**Status:** Accepted
**Date:** 2026-05-13

## Context

This project will accumulate many design decisions over its life, what database to use, how to handle authentication, what protocol the Pi speaks to the server, what library does Argon2id, whether to use cookies or bearer tokens, how to ship updates to the Pi, and so on.

Decisions made early but undocumented become invisible: future me (or anyone reading this on GitHub) sees only the *result*, not the *reasoning*, and is more likely to "fix" a deliberate choice without understanding the constraint it solved.

Threat-model-driven decisions are especially prone to this. A choice that looks weird in isolation often makes sense once you know what it was defending against.

## Decision

Significant architecture decisions will be recorded as Architecture Decision Records (ADRs) in `docs/adr/`. I use the [Michael Nygard format](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions): one short markdown file per decision, with sections for Context, Decision, Consequences, and Alternatives Considered.

A decision is "significant" if at least one of these is true:
- it would be expensive to reverse later,
- it has security implications,
- it is non-obvious to a reader of the code.

Files are numbered sequentially (`0001-`, `0002-`, ...). Numbers are never reused, even if an ADR is later superseded.

Possible Status values:
- **Proposed** - under discussion, not yet committed to.
- **Accepted** - current.
- **Deprecated** - no longer the way we do it, but no replacement.
- **Superseded by ADR-NNNN** - replaced by a newer decision.

A superseded ADR is not deleted. It stays as a record.

## Consequences

- Future-me has a written record of why things are the way they are.
- Decisions can be marked Superseded later without losing the history.
- Adds a small overhead per significant decision, the overhead is the point: it forces the decision to be considered before it's made, not after.
- Reviewers (including the GitHub audience) can see the design thinking, not just the code.

## Alternatives Considered

- **No ADRs (rely on commit messages):** loses context once commits scroll off. Hard to search. Doesn't support evolving status.
- **A single `DECISIONS.md` file:** doesn't support per-decision status cleanly. Diffs get noisy as the file grows. Hard to link to a specific decision.
- **External wiki:** drifts from the repo. ADRs in-repo stay versioned alongside the code they describe.
