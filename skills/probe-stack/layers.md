# Layers

What each layer covers. These are prompts for spotting open decisions, not questions to read out. Only ask what is still undecided and matters for this project.

## Core layers

### Product
- Who are the users, and roughly how many?
- What problem does this solve, and what do users do today without it?
- What is in scope for the first version, and what is explicitly out?
- How will we know it worked: what's the success measure?
- Deadlines, budget, team size, or other hard constraints?

### Data
- What are the main entities and how do they relate?
- Where is data stored (relational, document, file, cache, third party), and why?
- Who owns each piece of data: this system, or another one it copies from?
- What has to stay consistent, and what can be eventually consistent?
- How does data grow, and what gets archived or deleted?

### Logic
- What are the business rules and the states each entity moves through?
- What must always be true (invariants)?
- Which edge cases matter: empty, duplicate, partial, out of order, very large?
- What runs in the background or on a schedule?
- Where does this logic live (backend, frontend, database, worker)?

### API / Integration
- What does this system expose, to whom, and in what style (REST, GraphQL, RPC, events)?
- Which external systems does it call, and what happens when they're slow or down?
- How are errors returned to callers?
- How will the contract change over time without breaking existing callers?
- Sync or async between components? Webhooks, queues, polling?

### UI
- What are the main screens and user flows?
- What does each screen show while loading, when empty, and on error?
- Which platforms and devices: web, mobile, desktop, CLI?
- How does the user know an action worked or failed?
- Is there an existing design system or component library?

### Security
- How do users prove who they are (authentication)?
- Who can do what (authorization, roles, tenancy)?
- Where do secrets live, and how are they rotated?
- What untrusted input reaches the system, and how is it validated?
- What is the worst thing an attacker could do, and what stops it?

### Compliance / Privacy
- What personal or sensitive data is collected, and is all of it needed?
- Which regulations apply (GDPR, HIPAA, PCI, SOC 2, local laws)?
- How long is data kept, and how is it deleted on request?
- What needs an audit trail?
- Where must data physically reside?

### Performance
- Expected load: users, requests per second, data volume, now and in a year?
- Latency targets for the important actions?
- What will be cached, where, and how is the cache invalidated?
- Where are the likely bottlenecks?
- Rate limits, both ours and those of the services we call?

### Reliability
- What happens when each dependency fails?
- Retries, timeouts, idempotency: what is safe to repeat?
- Backups: how often, where, and has a restore been tested?
- Acceptable downtime and data loss (uptime target, recovery time, recovery point)?
- Can the system run in a degraded mode instead of failing completely?

### Observability
- What gets logged, and what must never be logged (secrets, personal data)?
- Which metrics show the system is healthy?
- What triggers an alert, and who receives it?
- How would someone debug a problem in production?
- Tracing across services, if there are several?

### Infrastructure / Deployment
- Where does it run (cloud, on-premises, serverless, containers, edge)?
- Which environments exist (dev, staging, prod), and how do they differ?
- How does code get from a merge to production (CI/CD)?
- How is a bad release rolled back?
- Is infrastructure defined as code?

### Testing
- What gets unit, integration, and end-to-end tests?
- Where does test data come from?
- What must pass before a release?
- How are external services handled in tests (mocks, sandboxes, contracts)?
- Any performance, security, or accessibility testing?

## Situational layers

Add a layer when you see its signs.

| Layer | Signs it's needed | What it covers |
|---|---|---|
| **Accessibility / i18n** | Public-facing UI, many languages or regions, legal accessibility duty | Screen readers, keyboard navigation, contrast, translation, time zones, currencies, date formats |
| **State / concurrency** | Real-time features, several users editing the same thing, background jobs, money or stock levels | Locking, conflict resolution, race conditions, ordering, exactly-once processing |
| **Configuration / feature flags** | Gradual rollouts, per-customer settings, A/B tests | Where settings live, who can change them, flag cleanup |
| **Cost** | Paid third-party APIs, heavy compute or storage, tight budget | Expected monthly spend, cost per user, what drives cost up, spending limits |
| **Data migration** | Replacing an existing system, schema changes to live data | Moving data across, backfills, running old and new side by side, cutover and rollback |
