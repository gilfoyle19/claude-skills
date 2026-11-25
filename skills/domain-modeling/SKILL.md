---
name: domain-modeling
description: Shape and tighten a project's shared domain language. Use when codebase vocabulary is being discussed, when a GLOSSARY.md is written or edited, or when an architecture decision record (ADR) is created or revised.
---

# Domain Modeling

Shape the project's domain language while the design is still taking form. This is the *hands-on* practice: questioning words, making up boundary-case situations, and recording terms and decisions as soon as they settle. (Simply *looking up* words in `GLOSSARY.md` is not this skill: any skill can do that in a line. Use this skill when the model itself is changing, not when you are only reading it.)

## Where things live

A typical repo has one context:

```
/
├── GLOSSARY.md
├── docs/
│   └── adr/
│       ├── 0001-event-sourced-orders.md
│       └── 0002-postgres-for-write-model.md
└── src/
```

A `GLOSSARY-MAP.md` at the root means the repo has several contexts, and the map tells you where each one is:

```
/
├── GLOSSARY-MAP.md
├── docs/
│   └── adr/                          ← decisions that span the system
├── src/
│   ├── ordering/
│   │   ├── GLOSSARY.md
│   │   └── docs/adr/                 ← decisions for this context only
│   └── billing/
│       ├── GLOSSARY.md
│       └── docs/adr/
```

Only create a file once there is something to put in it. With no `GLOSSARY.md`, make one when the first term is settled. With no `docs/adr/`, make it when the first ADR is called for.

## While the conversation runs

### Test words against the glossary

If the user says something that clashes with the vocabulary already in `GLOSSARY.md`, raise it straight away. "The glossary says 'cancellation' means X, but you appear to mean Y. Which one?"

### Pin down loose wording

If the user reaches for a vague or overloaded word, offer a precise standard term. "When you say 'account', is that the Customer or the User? They aren't the same thing."

### Work through specific situations

While relationships in the domain are under discussion, test them with concrete situations. Make up situations that push on the edges and make the user say exactly where one concept ends and another begins.

### Check the code

If the user describes how something behaves, see whether the code matches. When it doesn't, point it out: "The code cancels whole Orders, yet you've just said an Order can be partly cancelled. Which is correct?"

### Write to GLOSSARY.md as you go

As soon as a term is settled, update `GLOSSARY.md` on the spot. Don't save them up for later: record each one when it happens. Follow the layout in [glossary-template.md](./glossary-template.md).

Keep `GLOSSARY.md` completely free of implementation detail. It is not a spec, not a notepad, and not a place to park implementation choices. It is a glossary and only a glossary.

### Suggest ADRs rarely

Suggest writing an ADR only when all three of these hold:

1. **Costly to undo**: changing course later would carry real cost
2. **Puzzling without background**: someone reading it later will ask "why was it done like this?"
3. **A genuine trade-off**: real alternatives existed and one was chosen for specific reasons

If even one is missing, don't write the ADR. Follow the layout in [decision-record-template.md](./decision-record-template.md).
