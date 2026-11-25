# Decision Record (ADR) Layout

ADRs go in `docs/adr/`, numbered in sequence: `0001-slug.md`, `0002-slug.md`, and so on.

Don't create `docs/adr/` until the first ADR is actually needed.

## Template

```md
# {Brief title of the decision}

{1-3 sentences: the background, what was decided, and the reason.}
```

Nothing more is required. A single paragraph is a complete ADR. What matters is capturing *that* the decision happened and *why*, not completing a form.

## Extra sections

Add these only when they genuinely help. Most ADRs can leave them out.

- **Status** frontmatter (`proposed | accepted | deprecated | superseded by ADR-NNNN`): handy when a decision gets revisited
- **Considered Options**: only when the alternatives that lost are worth remembering
- **Consequences**: only when knock-on effects aren't obvious and need stating

## Numbering

Find the highest number already in `docs/adr/` and add one.

## When to suggest an ADR

All three must hold:

1. **Costly to undo**: changing course later would carry real cost
2. **Puzzling without background**: someone reading the code later will ask "why on earth was it done like this?"
3. **A genuine trade-off**: real alternatives existed and one was chosen for specific reasons

If a decision is cheap to undo, skip it: you can simply undo it. If nothing about it is puzzling, nobody will ask why. If there was no real alternative, there's nothing to record beyond "we took the obvious route."

### Good candidates

- **Overall architecture.** "We're using a monorepo." "The write model is event-sourced, the read model is projected into Postgres."
- **How contexts talk to each other.** "Ordering and Billing communicate via domain events, not synchronous HTTP."
- **Technology choices that lock you in.** Database, message bus, auth provider, deployment target. Not every library, only the ones that would take a quarter to replace.
- **Ownership and scope lines.** "Customer data is owned by the Customer context; other contexts reference it by ID only." The deliberate no's matter as much as the yes's.
- **Intentional departures from the expected approach.** "We're using manual SQL instead of an ORM because X." Anything where a sensible reader would assume the reverse. These keep the next engineer from "fixing" something done on purpose.
- **Constraints the code doesn't show.** "We can't use AWS because of compliance requirements." "Response times must be under 200ms because of the partner API contract."
- **Alternatives turned down for non-obvious reasons.** If GraphQL was considered and REST chosen for subtle reasons, write it down; otherwise someone will propose GraphQL again in six months.
