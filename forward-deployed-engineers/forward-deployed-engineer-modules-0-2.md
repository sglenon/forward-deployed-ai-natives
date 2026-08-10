# Forward-Deployed Engineering
## Modules 0 to 2, consolidated

Master learner-facing reference for the Forward-Deployed Engineer course. Each `##` heading is designed to become one LMS item.

Delivery is individual and self-paced, with live practice and mentor review. Items are in dependency order within each module.

---
---

# Module 0: The Role and Its Edges

Half a day. Complete before joining a client session. Not skippable.

Everything later in the program is a technique. This module is the judgment those techniques serve. An engineer who skips it becomes faster at building whatever was asked for without becoming better at knowing whether it should be built.

---

## 0.1 Why this role exists

Most product engineering begins after someone has translated the problem. You receive a roadmap item, a design, a ticket, an acceptance criterion, or at least a product manager who owns the ambiguity. The system boundary is mostly visible and the team around you holds the customer context.

Forward-deployed engineering starts earlier and stays later.

You work where the client's operation, people, data, policy, and software meet. The stated request is evidence, not a specification. You are responsible for finding the real constraint, choosing the narrowest useful intervention, putting it into the client's world, and staying long enough to prove it works and can be owned without you.

This role became necessary wherever a powerful general platform met a highly specific customer reality. The platform was rarely the hard part. Translation was. Someone had to understand the customer's operation deeply enough to configure, integrate, and extend the technology around it. That person needed the technical range to build and the client judgment to avoid building the wrong thing.

AI makes this translation problem more obvious. General capability is abundant. Reliable application inside a real organization is not.

> **THE PART PEOPLE GET WRONG**
>
> Forward-deployed does not mean "the engineer who travels," "the engineer on sales calls," or "the person who makes custom demos."
>
> **Your work changes a real operation and survives your departure.** That is the distinction.

### Our version of the bet is specific to you

The role has two halves.

1. **Technical range.** Enough breadth to move across an unfamiliar application, data model, integration, deployment path, and operational failure.
2. **Client translation.** Enough judgment to understand how work actually happens, find the problem behind the request, make tradeoffs legible, and move a group of people toward a decision they can own.

You already have the first half. You can read unfamiliar code, reason about systems, and ship production changes. This program does not reteach those skills.

> **THE PREMISE OF THIS PROGRAM**
>
> Your technical strength becomes more valuable when you can delay solutioning, learn from operators, and explain consequences without hiding behind implementation detail.

You are not becoming a salesperson or a product manager. You are acquiring the client and operational judgment required to own the space between a vague need and a durable outcome.

### The three ownership tests

Before calling work forward-deployed, ask:

1. **Did you learn how the operation really works from the people doing it?**
2. **Did your technical choices follow from evidence rather than the first request?**
3. **Can the client run, support, and extend the result when you leave?**

If any answer is no, the work may still be useful. It is not yet complete.

---

## 0.2 The two states of your work

Because your work ships, one distinction carries the whole role.

> **Everything you build is in one of two states, and you always know which one. Moving between them is a decision someone signs off on, never something that just happens.**

| | State A: Discovery build | State B: Production work |
|---|---|---|
| **Purpose** | Reduce a named uncertainty | Create an outcome people can depend on |
| **Lifespan** | Days | Indefinite |
| **Fictions** | Deliberate and catalogued | Defects or explicit temporary risks with owners |
| **Bar** | Enough evidence to decide | Secure, observable, maintainable, adopted, and operable |
| **Success** | A better decision, including "stop" | The outcome moves and the client can own it |

These are not two quality levels. They are different jobs.

A stubbed integration may be exactly right in State A when the question is whether an operator understands the workflow. The same stub is disqualifying in State B. Conversely, building full identity, observability, and recovery before you know whether the workflow is useful can destroy the speed that makes discovery valuable.

Strong engineers often dislike deliberate fictions. That instinct protects production systems, but applied too early it produces expensive evidence. The discipline is not "always build it properly." The discipline is **build exactly enough for the state you are in and label it honestly.**

### The four State A questions

Every discovery build answers one primary question.

1. **Are we solving the right operational problem?** A request such as "we need a dashboard" may be a symptom of delayed data, unclear responsibility, or an approval bottleneck.
2. **Will the people in the workflow use this shape of solution?** The sponsor's approval does not answer this. Operators do.
3. **Can the client's real data and systems support it?** A field in a slide deck is not evidence that the field exists, is reliable, is accessible, or may legally be used.
4. **Is the value large enough to justify production work?** Technical feasibility and economic usefulness are separate questions.

Write the primary question at the top of the engagement brief. If the build cannot change a decision, it is not a discovery build. It is a demo.

### Preserve the risky part

Discovery only works if the test includes the uncertainty.

- If data quality is the risk, a polished UI over invented clean data proves nothing.
- If operator adoption is the risk, an API benchmark proves nothing.
- If integration permissions are the risk, a local stub proves nothing.
- If model accuracy on the client's documents is the risk, a generic benchmark proves nothing.

Fake the surrounding plumbing. Preserve the thing that could make the proposed direction fail.

### What State A is not

- **Not a foundation.** Reuse is a possible later decision, not a hidden requirement.
- **Not an estimate.** Discovery speed does not predict production effort.
- **Not an architecture commitment.** The fastest learning path may be the wrong durable design.
- **Not a sales promise.** Evidence can support a proposal; it cannot authorize one.
- **Not production because an engineer wrote it.** Professional code style does not provide security review, operations, adoption, or ownership.

### What State B requires beyond deployment

State B is not complete when CI is green or the release reaches production.

- The intended users can complete the operational task.
- Failure behavior and manual fallback are known.
- Access, audit, retention, and privacy match the client's controls.
- Monitoring reveals both system health and outcome failure.
- A named team receives alerts and knows what to do.
- Rollback and recovery have been exercised at a proportionate level.
- The client can maintain and extend the result without routing everything through you.

### Promotion: the only legal way across

A discovery build can become production work. It happens through an explicit review:

1. **A named owner decides.** Enthusiasm in a demo is not a promotion decision.
2. **The evidence is reviewed.** The decision must be no stronger than the evidence.
3. **The fictions and risks are listed.** Every stub, shortcut, sample, manual step, untested condition, and missing owner becomes visible.
4. **Hardening and adoption are scoped.** Security, operations, data, UX, rollout, training, and support are real work.
5. **The artifact changes state.** From that point forward it follows the client's production controls.

> **THE FAILURE THIS PREVENTS**
>
> Drift begins with "the code is already pretty solid." That statement may be true and still irrelevant. Production readiness is a property of the whole operating system around the code, not the code alone.

---

## 0.3 The seven ways this goes wrong

Every later module prevents one or more of these failures.

### 01. The solution reflex
`DISCOVERY FAILURE`

*A client says reconciliation takes three days. Before the operator finishes explaining, you are drawing an event pipeline and proposing automated matching. The actual delay comes from a policy requiring a manager to review exceptions in a spreadsheet once each afternoon.*

**Why it happens.** Engineers are trained and rewarded to converge. Familiar technical shapes create the feeling of progress.

**What prevents it.** Module 1: follow one recent case end to end before proposing a system.

### 02. The technically correct wrong answer
`OUTCOME FAILURE`

*The integration is secure, tested, observable, and exactly matches the requirements. Nobody uses it because it adds a second queue to a team already measured on clearing the first one.*

**Why it happens.** Requirements described the desired feature but not the incentives and workflow surrounding it.

**What prevents it.** Operator observation, stakeholder mapping, and an outcome measure agreed before build.

### 03. The accidental commitment
`COMMERCIAL FAILURE`

*A sponsor asks whether the production version is "basically another sprint." You explain that the core logic is straightforward. In the meeting notes, the project is now one sprint.*

**Why it happens.** Technical confidence is heard as organizational commitment. Qualifiers disappear when the answer travels.

**What prevents it.** The never-alone list and a rehearsed holding phrase.

### 04. The clean-code promotion
`DRIFT IN THE ARTIFACT`

*The discovery build has types, tests, and a tidy architecture. Someone connects it to real data. No one reviews retention, support, rollback, or whether its AI output needs human approval.*

**Why it happens.** Engineering quality creates a credible signal that overwhelms missing operational work.

**What prevents it.** State labels, a faked list, and the formal promotion review.

### 05. The hero loop
`DRIFT IN OWNERSHIP`

*You know the client system best, so every difficult request comes directly to you. You respond quickly. Six months later, reliability depends on your memory and the client's team has learned to wait for you.*

**Why it happens.** Rescue behavior feels like service and is often praised in the short term.

**What prevents it.** Ownership transfer begins on day one. Module 5 measures whether the client can operate without you.

### 06. The invisible decision-maker
`RELATIONSHIP FAILURE`

*The sponsor and operators approve the solution. Security blocks production access because nobody involved them until release week.*

**Why it happens.** Enthusiasm is mistaken for authority and stakeholder mapping is treated as administration.

**What prevents it.** Item 1.4: name every owner whose approval, data, system, or team the work depends on.

### 07. The outcome-free deployment
`STATE B FAILURE`

*The service is live, dashboards are green, and the project is declared complete. The manual process continues beside it because the team was never trained and one common exception is unsupported.*

**Why it happens.** Deployment is visible and easy to timestamp. Adoption and operational change are slower and shared across teams.

**What prevents it.** Outcome observability, an adoption plan, and an explicit client owner.

---

## 0.4 Where your authority ends

You may be the person in the room who understands the implementation best. That does not make every adjacent decision yours.

There are seven things you never decide alone.

### The never-alone list

1. **Price, timeline, and contractual scope.** Technical effort informs these decisions; it does not authorize them.
2. **Feasibility guarantees.** A promising test is not a guarantee across real data, load, policy, or adoption.
3. **Production access and release.** Follow the client's named owners and controls, even when you have the credentials and can technically proceed.
4. **Data-use exceptions.** Never reinterpret classification, consent, retention, residency, or approved-tool rules yourself.
5. **Compliance or legal meaning.** Explain system behavior. Do not declare it compliant.
6. **Promotion.** Recommending State B is part of your role. Authorizing investment and risk belongs to named owners.
7. **Long-lived architecture and ownership.** If the client inherits the maintenance or lock-in, their technical owner participates in the choice.

### Why expertise does not expand authority automatically

Expertise gives your words weight. In a client setting, that makes casual answers more dangerous, not less.

"Technically possible" may be heard as "included." "The data is encrypted" may be heard as "approved." "I can ship this Friday" may be heard as a delivery commitment. Your job is to make the missing decision visible without becoming evasive.

> **READ THIS TWICE**
>
> **Escalation is not a failure of ownership. It is how you protect the owners of decisions that are not yours.**
>
> Advancement in this program requires evidence that you escalated something you could technically have done alone.

### Your escalation paths

*Replace every placeholder with a real person before publishing the course. A blank path is not a path.*

| Question type | Goes to | When |
|---|---|---|
| Price, timeline, contract, or scope | *[senior client lead]* | Before responding |
| Promotion to State B | *[client decision owner]* + *[senior client lead]* + *[technical owner]* | Before commitment |
| Production access or release | *[client technical owner]* | Before action |
| Data classification or tool approval | *[security/data owner]* | Before data is accessed or moved |
| Compliance or legal interpretation | *[named compliance/legal owner]* | Before representing a position |
| Long-lived architecture | *[client technical owner]* + *[FDE lead]* | Before implementation |
| Client relationship going sideways | *[senior client lead]* | Immediately |
| Something you cannot categorize | *[FDE lead]* | Immediately |

### The holding phrase

You need a sentence that separates a useful technical answer from a commitment.

> "I can tell you what the evidence says technically. Before we turn that into a delivery or compliance commitment, I need to bring in the person who owns that decision."

Write your own version. Say it aloud until it sounds natural. If it sounds like a refusal, make it more helpful. If it sounds like a promise, make the boundary clearer.

---

## 0.5 The framing exercise

**Assessed.**

A working discovery build looks like software. Your technical credibility makes it even easier for a client to assume the hard part is finished. You must replace that assumption with a useful evaluation frame.

> **YOUR TASK**
>
> Write the five or six sentences you would say when first showing a discovery build. Write for speech, not for a document.

### Version A (fails)

> "This is an early prototype, but the architecture is pretty clean and the main integration works. We still need to add proper auth, monitoring, and some edge cases. Assuming there are no surprises in the client environment, turning it into production should be fairly straightforward."

Every sentence sounds reasonable. Together they create a commitment.

"Early" and "fairly straightforward" are vague. The passage never states what decision the artifact supports. It lists missing production work as though the list were complete before a production review has happened. It invites the client to hear that only finishing work remains.

### Version B (works)

> "This build answers one question: can we match the fields in your actual intake files reliably enough to remove the first manual sorting step? It uses the approved sample set, and a person still reviews every proposed match. The queue, identity, and downstream write are simulated because they do not affect that question. Today, I want your operations team to try the difficult files and show us where the suggested match would create the wrong action. If the evidence is strong, the next step is a separate production review covering security, integration, operations, and rollout."

The artifact is the same. The conversation is different.

The question appears first. The central risk is preserved. The fictions are named and justified. The client receives a concrete job. Promotion is described as a separate decision rather than an implied continuation.

### What yours needs

- [ ] One primary question in the first sentence
- [ ] The real evidence or representative material being used
- [ ] Every relevant fiction stated plainly
- [ ] Why those fictions do not invalidate this test
- [ ] A specific job for the client or operator
- [ ] The decision that follows, without assuming the answer
- [ ] No estimate, guarantee, or implied promotion

> **THE TEST**
>
> Read it aloud. If it sounds like a demo narration, rewrite it. If it sounds like an invitation to challenge a claim, you are done.

---

## 0.6 Close

Carry four things into Module 1.

1. **Your first answer is a hypothesis.** Technical experience makes it a better hypothesis, not a fact.
2. **Always know the state.** State A reduces uncertainty. State B creates an outcome people can depend on.
3. **The client's operation is part of the system.** People, incentives, approvals, workarounds, and policy are not "non-technical details."
4. **Ownership includes leaving.** If the result depends on your presence, the engagement is not finished.

> **BEFORE MODULE 1**
>
> Arrange access to one operator and one recent real example of their work. A process deck is not a substitute.

---
---

# Module 1: Customer and Operational Literacy

Weeks 1 to 2. Ten items, in dependency order.

---

## 1.1 What this module is for

This module teaches you to understand an operation before turning it into a software problem.

That sounds slower than building. It is usually the fastest route to useful work. A day spent discovering that the bottleneck is an approval rule can prevent a month spent optimizing the system that waits for it.

### What you are building toward

- A current-state workflow grounded in a real example
- A stakeholder map with actual decision rights
- A problem statement that distinguishes evidence from assumption
- An outcome measure with a baseline
- A playback the client recognizes as their reality

The final assessment is not judged by your mentor first. It is judged by the people who perform the work.

### The stance

You are not a passive note-taker. You will form hypotheses constantly. The discipline is to hold each one lightly enough that evidence can change it.

> **USE THIS SENTENCE**
>
> "My current hypothesis is ____. The evidence is ____. The fastest way to prove me wrong is ____."

This phrasing makes uncertainty useful. It gives the room something concrete to correct without turning your first idea into a commitment.

---

## 1.2 Start with a recent real example

People describe idealized processes. Real cases contain the exceptions, workarounds, and missing information that determine the design.

Ask the operator to choose one recent case and walk it from the event that started the work to the point where they considered it complete.

### Questions that reveal the work

- What happened immediately before this reached you?
- What did you receive, and in what form?
- What did you check before acting?
- Which system did you open first? Why?
- What information was missing or unreliable?
- Where did you wait, ask, copy, retype, or leave the official system?
- What made this case easy or difficult?
- What happened when the normal path failed?
- Who received the work next?
- How did you know it was complete?

Do not ask all of these like a questionnaire. Follow the case. Ask "what happened next?" until the outcome is real.

### Artifacts beat recollection

When policy permits, ask to see the actual redacted file, screen, queue, form, message, or report. What people call "the same spreadsheet" may arrive in twelve layouts. What they call "an API" may be a nightly file export. What they call "approval" may mean a message to a particular person.

Handle all artifacts under the client's data rules. If access is not approved, do not improvise. Record the limitation and use a client-prepared example.

### Your output

Write a case trace with five columns:

| Step | Person | Action | System or artifact | Friction or decision |
|---|---|---|---|---|
| Trigger | | | | |
| ... | | | | |
| Outcome | | | | |

One real case is not the whole process. It is the first piece of evidence.

---

## 1.3 Map the current workflow

Now combine the case trace with interviews and system evidence into a current-state map.

### Include five kinds of thing

1. **People.** The role doing the work, not only the department.
2. **Actions.** What the person actually does.
3. **Systems and artifacts.** Applications, spreadsheets, inboxes, files, paper, and side channels.
4. **Data.** What enters, changes, and leaves.
5. **Boundaries.** Handoffs, approvals, access changes, and ownership transitions.

Start with the operation. Do not begin with a service diagram. A service diagram can show where data moves and still hide the manager who approves exceptions once per day.

### Mark these explicitly

- wait time;
- repeated entry or copying;
- rework and loops;
- decisions and their criteria;
- exceptions and escalation;
- manual reconciliation;
- information that arrives late;
- work performed outside the official system;
- steps nobody claims to own.

### Documented process versus actual process

Both matter.

The documented process tells you what the organization believes should happen and may contain controls you must preserve. The actual process tells you how outcomes are produced today. Treating either as the whole truth creates risk.

Record the gap without shaming the operator. Workarounds are often rational responses to systems that do not fit the work.

---

## 1.4 Build the stakeholder and decision map

"The client" is not one person.

At minimum, identify these roles. One person may hold several; several people may share one.

| Role | What they own |
|---|---|
| Sponsor | Desired business result and organizational backing |
| Buyer or commercial owner | Contract and budget |
| Operator | Daily work and exceptions |
| Process owner | Rules and performance of the workflow |
| Technical owner | Systems, architecture, release, and maintenance |
| Data owner | Access, quality, permitted use, and lifecycle |
| Security/compliance owner | Controls and interpretation process |
| Administrator/support owner | Configuration, incidents, and user help |
| Adoption owner | Training, communications, and process change |

### For each stakeholder, record

- what outcome they want;
- what they fear losing;
- what evidence they trust;
- what decision they can make;
- what decision they can block;
- when they need to be involved.

### Enthusiasm is not authority

A sponsor can be excited and still lack authority over security. An operator can validate usability and still not approve process change. A technical owner can approve architecture and still not own adoption.

Every required decision needs a named owner. "The client will decide" is an incomplete map.

### The missing-chair check

Before a decision meeting, ask: whose team, data, system, risk, or budget is affected but not represented? An empty chair is often the most important fact in the room.

---

## 1.5 Separate request, symptom, problem, and outcome

These four statements are related but not interchangeable.

| Layer | Example |
|---|---|
| **Request** | "Build us a reconciliation dashboard." |
| **Symptom** | "Reconciliation takes three days." |
| **Problem** | "Analysts cannot identify the owner of unmatched records until two delayed files are manually combined." |
| **Outcome** | "Analysts route unmatched records to the correct owner during the same working day, with an auditable reason." |

The request is useful evidence. It tells you what solution the client currently imagines. Do not dismiss it. Do not mistake it for the problem.

### A working problem statement

Use this structure:

> **[Person or role]** cannot **[complete an operational job]** when **[condition]**, because **[evidence-backed constraint]**. This causes **[measured or observable consequence]**. We believe **[intervention hypothesis]** may improve **[outcome]**, and we need to test **[uncertainty].**

If you cannot fill a field, write `unknown`. An honest unknown is safer than a smooth sentence containing an assumption.

### Baseline before target

Measure the current condition at a proportionate level:

- time from trigger to outcome;
- active effort versus waiting;
- frequency and volume;
- error or rework rate;
- cost or revenue effect;
- risk exposure;
- user or customer consequence.

Avoid false precision. "In eight sampled cases, five waited overnight for owner assignment" is stronger than an invented percentage.

---

## 1.6 Ask questions that change decisions

Good discovery questions make a decision easier. Weak questions merely collect opinions.

### Prefer behavior over preference

Weak: "Would an automated summary help?"

Better: "Show me the last summary you created. What did you include, who read it, and what decision did they make?"

Weak: "How often does this happen?"

Better: "Looking at last week, which cases followed this path?"

Weak: "What features do you need?"

Better: "What must you know before you can take the next action?"

### Follow vague words

When someone says *usually, quickly, accurate, secure, simple, compliant, real time,* or *the business*, ask what it means here.

- "Usually: what happened in the cases that did not?"
- "Accurate enough for which decision?"
- "Real time compared with what operational deadline?"
- "Who specifically is 'the business' in this step?"

### Allow silence

Ask one question. Stop. Do not rescue the room by answering your own question or offering a multiple-choice list from your architecture.

---

## 1.7 Explain a system in the client's terms

You will often need to explain an architecture, constraint, or failure to people who should not need your vocabulary to participate.

### Use this order

1. **Outcome:** what this enables or prevents.
2. **Operational path:** who does what and when.
3. **Boundary:** where data, authority, or responsibility changes.
4. **Mechanism:** only the technical detail needed for the decision.
5. **Tradeoff:** what improves, what becomes harder, and who owns the consequence.

### Example

Instead of:

> "We'll use an asynchronous event-driven pipeline with idempotent consumers."

Try:

> "When a file arrives, the client system records it immediately and processes it in the background. If the same file is sent twice, it will not create two cases. That makes intake more reliable, but it also means the operations team needs a queue for files that cannot be processed automatically."

The second version is not less technical. It exposes the consequence that needs a decision.

### Draw two diagrams

First draw the operational view: people, actions, systems, data, and boundaries.

Then draw the technical view: components, interfaces, stores, trust boundaries, and runtime ownership.

The diagrams should connect. If a technical component cannot be tied to an operational need, ask why it is there. If an operational step has no technical or human owner, you found a risk.

---

## 1.8 Run and close a client session

A client session is useful when it changes shared understanding or enables a decision.

### Before

- Name the decision or artifact the session should produce.
- Invite the people required for that purpose.
- Send any material early enough to inspect.
- Assign a facilitator and a note owner when possible.
- Decide what sensitive material may be shown or recorded.

### During

- State the purpose and time boundary.
- Separate facts, assumptions, decisions, and open questions in the notes.
- Park topics that matter but do not serve this session.
- Watch who is not speaking and whose work is being described by someone else.
- At ten minutes remaining, stop creating new branches and converge.

### Close

Read back:

1. decisions made;
2. evidence learned;
3. unresolved questions;
4. owner and due point for each follow-up;
5. the next decision or session.

"We'll circle back" is not an owner or a plan.

### Written playback

Send a concise playback while memory is fresh. Use the client's language. Invite correction explicitly. The purpose is not polished minutes; it is to make disagreement visible before code hardens it.

---

## 1.9 Handle disagreement and uncertainty

Disagreement is information. It often reveals different incentives, definitions, or authority.

### Diagnose the disagreement

Ask which kind it is:

- **Fact:** What is true today?
- **Prediction:** What is likely to happen?
- **Value:** Which outcome matters more?
- **Risk tolerance:** What downside is acceptable?
- **Authority:** Who has the right to decide?
- **Language:** Are two people using the same word differently?

Each requires a different response. More logs can resolve a fact dispute. They cannot resolve who accepts a compliance risk.

### Make options legible

For a technical choice, show:

| Option | Outcome enabled | Cost or constraint | Risk | Reversibility | Owner needed |
|---|---|---|---|---|---|

Do not smuggle your preferred option into a fake neutral comparison. Make your recommendation and reasoning explicit, then name the owner of the decision.

### Say "I don't know" completely

Weak: "I'm not sure."

Working: "I don't know whether the source retains the field long enough for this audit. I will check the schema and retention policy with the data owner, and that answer will determine whether we use the source or record the value ourselves."

Uncertainty plus a resolution path builds trust.

---

## 1.10 Assessment: playback the operation

**The task:** observe a real or simulated workflow and play it back to the people involved.

### What you hand in

1. one recent case trace;
2. a current-state workflow map;
3. a stakeholder and decision map;
4. a problem statement separating evidence and assumptions;
5. a baseline and proposed outcome measure;
6. open questions with named owners;
7. a one-page written playback.

### The live playback

You have ten minutes. Cover:

- where the work begins and ends;
- the people and systems involved;
- where time, error, risk, or rework enters;
- what you believe the actual problem is;
- what remains uncertain;
- what decision should happen next.

### How it is judged

The strongest signal is that operators say, "Yes, that is how it actually works," then correct something specific. Correction is not failure. A playback so vague nobody can disagree with it has failed.

Your mentor also checks:

- Did you use real examples rather than only generalized claims?
- Did the proposed outcome belong to the client rather than to the software?
- Did you identify missing decision-makers?
- Did you preserve uncomfortable evidence that contradicted your first idea?
- Did you avoid promising a solution before Module 2?

---
---

# Module 2: From Ambiguity to a Buildable Intervention

Weeks 2 to 3. Ten items, in dependency order.

---

## 2.1 Where this module sits

Module 1 produced a shared account of the operation. Module 2 turns that account into the smallest responsible piece of work.

The transition is dangerous because writing code feels like certainty. A repository, schema, and plan can make unresolved questions disappear from view without actually resolving them.

> **THE RULE FOR THIS MODULE**
>
> Every technical choice points back to evidence, an explicit assumption, or a named constraint.

### What you will be able to do by the end

- Write a one-page engagement brief
- Select one primary State A question or State B outcome
- Map the client systems, data, access, and ownership needed
- Test the riskiest assumptions before committing architecture
- Choose a thin slice that produces useful evidence or value
- Use AI coding tools inside client data and review boundaries
- Define stop conditions before build momentum takes over

### What this module is not

It is not architecture astronautics, a generic discovery sprint, or permission to create a bespoke platform for one client's first request.

The output is a bounded intervention with visible reasoning.

---

## 2.2 Write the engagement brief

The engagement brief is the smallest shared contract between client reality and technical action. Keep it to one page whenever possible.

### Required fields

**Operation**

- Who is doing what today?
- What event starts the workflow?
- What outcome ends it?

**Problem and evidence**

- What prevents the outcome?
- What recent examples support that claim?
- What is the baseline?

**Target outcome**

- What observable condition should change?
- Who owns that measure?
- When and how will it be checked?

**State and question**

- State A or State B?
- If State A, what single uncertainty should the build reduce?
- If State B, what approved outcome and production controls apply?

**Boundaries**

- In scope and explicitly out of scope
- Approved data and environments
- Dependencies and decision owners
- Never-alone decisions this work may reach

**Assumptions and stop conditions**

- What are we currently treating as true?
- What evidence would stop or redirect the work?

### Weak brief

> Build an AI assistant that reads claims, extracts the relevant details, and updates the case-management system. Use the existing model API and finish a prototype for stakeholder review.

This is a solution description. It hides the operator, problem, evidence, data permission, risky assumption, and decision.

### Working brief

> Claims analysts spend the first hour of each case copying six fields from emailed PDFs into the case system. In eight observed cases, three PDFs used layouts the existing parser did not recognize, causing rework later. This State A build asks whether the approved model can propose the six fields from a representative redacted sample with enough accuracy that an analyst review is faster than manual entry. The model will not write to the case system; the downstream action is simulated. We will stop or redesign if critical-field errors remain above the threshold agreed with the process owner, if the sample cannot be approved for the tool, or if review time is not lower than the baseline. Promotion is out of scope.

The second brief can be challenged. That is what makes it useful.

---

## 2.3 Choose the decision and evidence

A discovery build exists to change a decision. Write the decision before choosing implementation.

### Decision statement

Use this form:

> After this work, **[named owner]** should be able to decide whether to **[stop / test further / choose an approach / propose production work]** based on **[specific evidence].**

Examples:

- The process owner can decide whether assisted extraction is worth a production proposal based on field accuracy and analyst review time across the representative sample.
- The technical owner can choose between batch and event integration based on the required decision deadline, source availability, and failure recovery.
- The sponsor can stop the dashboard proposal if operators confirm the delay occurs before the data reaches the reporting system.

### Evidence table

| Claim | Observation needed | Source | Pass/redirect condition | Decision owner |
|---|---|---|---|---|
| | | | | |

Define this before the build. Otherwise the team will use whatever the build happens to show as evidence.

### Confidence must match evidence

One operator session can reveal a workflow and generate hypotheses. It cannot establish adoption across a department. Twenty clean sample documents cannot establish performance on rare formats they do not contain.

State conclusions at the strength the evidence supports.

---

## 2.4 Perform technical reconnaissance

Technical reconnaissance tests whether the client's real environment supports the proposed intervention. It is not a full architecture phase.

### Map the terrain

For each relevant component, record:

| Component or data | Owner | Interface | Environment | Access path | Constraint or unknown |
|---|---|---|---|---|---|
| | | | | | |

Include:

- source and destination systems;
- identity and permission boundaries;
- data stores and lifecycle;
- integration interfaces and rate limits;
- deployment and release path;
- logging, monitoring, and audit sources;
- human review or approval points;
- vendor and licensing dependencies;
- client teams expected to maintain the result.

### Trace one representative record

Using approved and appropriately handled data, follow one record from origin to outcome.

Check:

- where each required field originates;
- whether the field means what people think it means;
- when it becomes available;
- whether it changes later;
- who may read or write it;
- which identifier links systems;
- how duplicates and corrections appear;
- how failure becomes visible.

"There is an API" is not reconnaissance. Calling the approved interface with a representative case and verifying semantics is reconnaissance.

### Read before proposing replacement

If a client has an existing system, learn its conventions, tests, deployment controls, and ownership model. A locally elegant pattern that the client's team cannot maintain is an operational regression.

---

## 2.5 Classify data and access before using them

Client proximity increases access. Access is not permission to move information wherever it is convenient.

Before any build or tool use, record:

- data classification;
- approved source and destination;
- permitted purpose;
- allowed people and service identities;
- retention and deletion expectation;
- residency constraints;
- whether prompts, logs, traces, or vendor systems retain content;
- whether synthetic or redacted data is required;
- the named owner who approved the path.

### The absolute rule

> **No client credential, production record, personal data, confidential document, or restricted code enters a repository, prompt, model, log, screenshot, or environment unless that exact use is approved.**

Approval for one path is not approval for another. Access to a production database does not authorize copying records into a local development environment. Approval to use one model vendor does not authorize a different coding agent.

### If the data path is unclear

Stop. Record the question. Ask the data or security owner. Do not solve ambiguity by quietly substituting your judgment.

---

## 2.6 Find and test the riskiest assumption

List assumptions across five dimensions:

1. **Desirability:** operators will use or trust the intervention.
2. **Feasibility:** systems, data, and model behavior can support it.
3. **Viability:** the outcome justifies cost and ongoing ownership.
4. **Safety:** security, privacy, compliance, and operational risks can be controlled.
5. **Adoption:** the organization can change the workflow and support it.

### Rank them

For each assumption, score informally:

- impact if false;
- uncertainty;
- cost and time to test;
- reversibility of proceeding without an answer.

Test high-impact, high-uncertainty assumptions early. Do not spend a week polishing around an integration permission that may never be granted.

### Preserve the uncertainty

If the model's behavior on poor scans is risky, use poor scans. If the user's trust in suggestions is risky, put suggestions in front of users. If access is risky, test the approval and connection path. A convenient proxy is only useful when you can defend the connection to the real uncertainty.

---

## 2.7 Choose the thinnest useful slice

A thin slice crosses the operation from a real trigger to a meaningful outcome for a narrowly chosen case. It is not merely the easiest component to code.

### Constrain four dimensions

- **User:** one role or small group
- **Case:** one common and bounded path
- **System path:** the minimum interfaces required to preserve the risk
- **Outcome:** one observable improvement or decision

### Useful thin slice

An analyst uploads one approved document type, reviews six proposed fields, corrects them, and exports a structured result. This can test extraction quality and review effort without writing to production.

### Thin component, not a useful slice

A generic extraction API tested against synthetic examples. It may be technically informative, but it does not show whether the operator can review the output or whether the representative documents contain the required information.

### Manual is allowed in State A

A person can move a file, trigger a job, review an exception, or copy a result behind the scenes when that manual step does not invalidate the question. Put the manual step in the faked list immediately.

Manual work is a discovery tactic, not a secret production architecture.

### State what the slice cannot prove

Every slice excludes evidence. Name the exclusions before anyone sees the result.

---

## 2.8 Design the intervention with the client

Do not disappear after discovery and return with a reveal.

### Use artifacts as questions

- Workflow map: "Where is this account wrong?"
- Technical map: "Which boundary or owner is missing?"
- Prototype: "What action would you take here?"
- Data sample: "Which values would make this unsafe to trust?"
- Option table: "Which consequence is unacceptable?"
- Runbook draft: "Who would actually receive this alert?"

Specific questions produce evidence. "What do you think?" produces politeness.

### Include the people who inherit the consequence

- Operators shape the workflow and exception behavior.
- Design or product partners review usability and service coherence.
- Technical owners shape integration and maintainability.
- Security and data owners shape permitted handling.
- Support and administration shape operating needs.
- Sponsors and process owners shape outcome and adoption.

Not everyone joins every session. Everyone required for a decision joins before it becomes expensive to change.

---

## 2.9 Use AI coding tools inside the boundary

Coding agents can compress reconnaissance and implementation. They can also create confident claims, broad changes, and new data paths faster than you can notice them.

> **The AI Excellence Playbook governs this item. Where tool behavior or this summary differs from the playbook, the playbook wins.**

### Give the agent grounded context

Provide only approved material, including:

- the engagement brief;
- repository instruction files;
- the specific acceptance evidence;
- the smallest relevant code and system context;
- explicit non-goals and protected boundaries;
- commands used for verification.

Do not substitute a giant context window for a clear task.

### Separate modes

**Reconnaissance:** ask the agent to find relevant code, interfaces, tests, and conventions. Verify every important claim directly.

**Options:** ask for approaches and tradeoffs. Treat them as hypotheses, not architecture approval.

**Scaffolding:** establish a disposable State A structure quickly.

**Constrained change:** specify what may change, what must not, and how success is verified.

**Review:** use an independent pass to find edge cases, security issues, or mismatch with the brief. Independence helps; it does not replace human accountability.

### Before execution

- Read the plan.
- Inspect intended files and commands.
- Check whether the tool will access a network, secret, client system, or broad filesystem area.
- Reject unexplained dependencies and infrastructure changes.
- Commit or create a reversible checkpoint.

### After execution

- Read the diff.
- Run proportionate tests.
- Verify behavior against the brief and evidence plan.
- Check what the agent changed outside the obvious path.
- Record any fiction or new assumption.

### Never do this

- paste client credentials or restricted material into an unapproved tool;
- accept a claim about the client's system without checking it;
- blanket-approve actions in a client repository;
- let generated polish expand the agreed scope;
- call generated code production-ready because tests pass.

---

## 2.10 Assessment: defend the intervention

You receive a messy client request, a representative codebase or environment, and access to simulated stakeholders.

### What you hand in

1. engagement brief;
2. primary decision and evidence table;
3. technical reconnaissance map;
4. data and access record;
5. ranked assumptions;
6. thin-slice plan;
7. faked list started before implementation;
8. stop or redirect conditions;
9. written client playback.

### The review

You have fifteen minutes to defend:

- why this is the right problem to act on;
- why this is State A or State B;
- what the work will prove;
- what it cannot prove;
- which real uncertainty is preserved;
- which parts are intentionally fake or manual;
- which owners and approvals are required;
- what evidence would make you stop;
- how the client can own the next step.

### How it is judged

- **Traceability:** do technical choices point to evidence, assumptions, or constraints?
- **Thinness:** is this the smallest slice that still tests the real risk?
- **Safety:** are data, access, authority, and production boundaries explicit?
- **Decision value:** will the result enable a named owner to make a better decision?
- **Client fit:** did operators and inheriting teams shape the intervention?
- **Intellectual honesty:** are unknowns and limitations visible without being used as disclaimers?

The assessment does not reward the most sophisticated architecture. It rewards the clearest path from client evidence to a responsible next decision.
