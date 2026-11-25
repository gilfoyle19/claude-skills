# GLOSSARY.md Layout

## Shape

```md
# {Context Name}

{A sentence or two on what this context is and why it exists.}

## Language

**Order**:
{A sentence or two describing the term}
_Avoid_: Purchase, transaction

**Invoice**:
A request for payment sent to a customer after delivery.
_Avoid_: Bill, payment request

**Customer**:
A person or organization that places orders.
_Avoid_: Client, buyer, account
```

## Guidelines

- **Take a position.** If several words name the same idea, choose the strongest one and put the rest under `_Avoid_`.
- **Keep each definition short.** No more than one or two sentences. Say what the thing IS, not what it does.
- **List only terms that belong to this project's context.** Generic programming ideas (timeouts, error types, helper patterns) stay out, however heavily the project uses them. Before adding a term, ask whether the idea is particular to this context or just general programming. Only the first kind goes in.
- **Use subheadings for groups** once natural clusters appear. If every term sits in one tight area, a single flat list is fine.

## One context or many

**One context (most repos):** a single `GLOSSARY.md` at the repo root.

**Several contexts:** a `GLOSSARY-MAP.md` at the repo root names the contexts, where each lives, and how they connect:

```md
# Glossary Map

## Contexts

- [Ordering](./src/ordering/GLOSSARY.md): receives and tracks customer orders
- [Billing](./src/billing/GLOSSARY.md): generates invoices and processes payments
- [Fulfillment](./src/fulfillment/GLOSSARY.md): manages warehouse picking and shipping

## Relationships

- **Ordering → Fulfillment**: Ordering emits `OrderPlaced` events; Fulfillment consumes them to start picking
- **Fulfillment → Billing**: Fulfillment emits `ShipmentDispatched` events; Billing consumes them to generate invoices
- **Ordering ↔ Billing**: Shared types for `CustomerId` and `Money`
```

Work out which shape applies:

- If `GLOSSARY-MAP.md` exists, read it to find the contexts
- If there is only a root `GLOSSARY.md`, there is one context
- If neither exists, create a root `GLOSSARY.md` once the first term is settled

With several contexts, work out which one the current topic belongs to. If you can't tell, ask.
