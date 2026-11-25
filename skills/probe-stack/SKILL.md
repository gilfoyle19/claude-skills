---
name: probe-stack
description: A persistent questioning session for a software feature, system, or architecture that covers every layer of the stack (product, data, logic, API/integration, UI, security, compliance, performance, reliability, observability, infrastructure, testing) before anything is built.
disable-model-invocation: true
---

Call the Skill tool with "interrogate", and run that session with the layer coverage below on top of it. Everything in `interrogate` still applies: waves of questions drawn from the ready set, a suggested answer on every question, facts looked up rather than asked, and no action until the user confirms common ground.

## Why layers

A plain interrogation only explores the parts of the decision map that come up in conversation. In software, the parts nobody mentions (who can access this, what happens when it fails, how anyone will know it failed) are where designs break. The layers make sure every part of the system gets visited, so nothing reaches implementation as an unspoken assumption.

## Core layers

Every session must cover these. See [layers.md](./layers.md) for what each layer asks about.

1. **Product**: users, problem, scope, success measure
2. **Data**: entities, storage, schema, ownership, lifecycle
3. **Logic**: business rules, workflows, edge cases, invariants
4. **API / Integration**: contracts, external systems, versioning, error handling
5. **UI**: screens, flows, states, feedback
6. **Security**: authentication, authorization, secrets, attack surface
7. **Compliance / Privacy**: personal data, regulation, retention, audit
8. **Performance**: load, latency targets, caching, limits
9. **Reliability**: failure modes, retries, backups, recovery
10. **Observability**: logs, metrics, alerts, debugging in production
11. **Infrastructure / Deployment**: hosting, environments, CI/CD, rollback
12. **Testing**: strategy, test data, release gates

## Situational layers

Add one only when the product calls for it, and say why you added it: accessibility and internationalization, state and concurrency, configuration and feature flags, cost, data migration. layers.md lists the signs that each one is needed.

## How layers fit the waves

- **Product comes first.** Answers in every other layer depend on who the users are and what success looks like, so Product questions are the first ready set. Only include questions from other layers in wave 1 if they don't depend on Product answers.
- **Layers are a coverage check, not a script.** Build the ready set from dependencies exactly as `interrogate` describes; a wave can mix layers. Don't march through the layers one at a time.
- **Tag each question with its layer**, so the user can see coverage:

  ```
  🔍 **P1** - [Security] **<short label>**: <the question in full>

  💡 <your suggested answer>
  ```

- **Size the questions to the project.** A weekend script and a multi-tenant SaaS need very different depth. For a layer that barely applies, ask one question that proposes a light answer ("No auth: it runs locally for one user. Yes?") instead of a full set.
- **Look up the existing stack first.** In a codebase, send a sub-agent to find the language, framework, database, hosting, auth, test setup and CI before asking about them. Ask only about choices still open, and about places where the user's plan disagrees with the code.

## Coverage line

After each wave, end with one line showing where every core layer stands:

```
Coverage: Product ✅ · Data ✅ · Logic ⏳ · API ⏳ · UI ⬜ · Security ⏳ · Compliance ⬜ · Performance ⬜ · Reliability ⬜ · Observability ⬜ · Infra ⬜ · Testing ⬜
```

✅ settled · ⏳ in progress · ⬜ not started · ➖ not applicable (user agreed)

## When the session is done

The session ends when the ready set is empty **and** every core layer is ✅ or ➖. A layer can only be ➖ if the user agreed it doesn't apply; never mark one ➖ silently. Then give a short summary of decisions grouped by layer, and wait for the user to confirm common ground before acting on any of it.
