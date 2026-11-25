---
name: interrogate
description: Question the user persistently about a plan, decision, or idea until every assumption is surfaced. Use when the user wants their thinking pressure-tested, asks to be interrogated or probed, or wants holes poked in a proposal.
---

Keep questioning the user until the two of you reach common ground. Model the subject as a **decision map**: each choice opens up the further choices that depend on it.

Move through the map in **waves**. The **ready set** is every choice whose dependencies are already resolved: the questions you can put to the user _right now_ without guessing at answers you don't have yet. Put the entire ready set to them in one wave: number every question and attach the answer you'd suggest. Then stop and wait for their replies before starting the next wave.

Lay out a wave like this:

```
🔍 **P1** - **<short label>**: <the question in full, which may run several paragraphs and list options>

💡 <your suggested answer>

---

🔍 **P2** - **<short label>**: <the question in full, which may run several paragraphs and list options>

💡 <your suggested answer>
```

Phrase every question so that replying "yes" adopts your suggested answer.

Each wave of replies changes the map: resolved choices extend the ready set and release the questions that were waiting on them. Work out the new ready set and send the next wave. If a question's answer hinges on another question that is still open in the current wave, it goes in a _later_ wave, not this one.

Gathering _facts_ is always your responsibility, never the user's. If a question in the ready set depends on something the environment can tell you (files, tools, and so on), send a sub-agent to look it up; never ask the user for information you could retrieve yourself. Don't stall while it works: an investigation still in progress counts as an unresolved dependency, so only the questions that rely on its result have to wait; send the rest of the ready set immediately. _Choices_ belong to the user: present each one and wait for their answer.

You are finished when the ready set is empty: every part of the decision map has been explored and no assumption remains unspoken. Don't act on the outcome until the user confirms you have reached common ground.
