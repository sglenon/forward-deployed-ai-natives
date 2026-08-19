# CAST Product Engineering — Curriculum

**Single source of truth for the CAST Product Engineering course.**

This file replaces `core-doc.md` and `cast-product-engineering-modules-0-2.md` for authoring and maintenance. The older files remain on disk as reference.

Delivery: 4–6 engineers per cohort, over 8 weeks, alongside normal delivery work.

---

## Table of Contents

1. [Thesis](#1-thesis)
2. [Prerequisites and the Technical Gate](#2-prerequisites-and-the-technical-gate)
3. [The Six Product-Ownership Skills and the Product-Ownership Loop](#3-the-six-product-ownership-skills-and-the-product-ownership-loop)
4. [Module 0: The Role and Its Edges](#4-module-0-the-role-and-its-edges)
5. [Module 1: Customer and Operational Literacy](#5-module-1-customer-and-operational-literacy)
6. [Module 2: From Ambiguity to a Product Decision](#6-module-2-from-ambiguity-to-a-product-decision)
7. [Workshop: Practiced Conversations and UI/UX Literacy](#7-workshop-practiced-conversations-and-uiux-literacy)
8. [Modules 3–6: Summaries](#8-modules-36-summaries)
9. [Levels After the Program / What the Organization Has to Supply / Risks Worth Watching](#9-levels-after-the-program--what-the-organization-has-to-supply--risks-worth-watching)
10. [Future Direction: On-the-Fly Client Collaboration](#10-future-direction-on-the-fly-client-collaboration)

---

## 1. Thesis

### Start with the client-value filter

Before discussing technology, asking for a state, or writing a brief, ask:

> **What does the client want to get from this work?**

Most answers fit one of three categories:

- save money;
- make money; or
- automate manual work.

These are practical filters, not vague strategy statements. Use them from the first client conversation through the whole engagement. If work cannot be connected to one of them, ask why it is being done. This is the starting question, not a question for the end of discovery.

### State A and State B

A normal product engineer usually receives a translated problem: a ticket, design, acceptance criterion, or system boundary. A CAST engineer works before that translation is complete. They spend enough time in the client's operation to find out whether the request is incomplete, wrong, or aimed at a symptom. They then stay involved long enough to put a durable change into use.

The program teaches a repeatable way to make product and technical decisions under client pressure:

1. observe before proposing;
2. turn uncertainty into claims that can be tested;
3. choose the smallest useful change; and
4. stay responsible until the client can use and own the result.

A CAST engineer starts with an unclear operational need. They clarify it, define the desired product outcome, select the right intervention, and check that it works in the real operation.

The engineer does not replace the product, design, commercial, or client teams. Within the agreed boundary, the engineer owns the product thread. This connects user evidence, product decisions, technical work, adoption, and outcomes.

If the work stops at advice, discovery, or a demo, it is consulting or prototyping under another name. The governing rule is:

> **Everything you build is in one of two states, and you must always know which state it is in. Moving between states requires an explicit sign-off. It must never happen by accident.**

#### State A: Discovery build

Purpose: reduce a named uncertainty.

Lifespan: usually days.

Deliberate fictions are allowed. For example, sample data, a stubbed integration, or a manual step may be the right choice. The build only needs to provide enough evidence for a decision, including a decision not to build.

A State A build may answer these questions:

1. Are we solving the right operational problem?
2. Will the people in the workflow use this type of solution?
3. Can the client's real data and systems support it?
4. Is the value large enough to justify production work?

#### State B: Production work

Purpose: create an outcome that people can depend on.

Lifespan: indefinite.

Fictions and shortcuts are defects unless they are clearly documented temporary risks with owners. The work must be secure, observable, maintainable, adopted, and operable by someone other than the person who built it.

State B succeeds when the intended users can use it, the client can run it, and the agreed outcome improves without unacceptable regressions. This includes changes to a live client system and any discovery build that has been formally promoted.

#### Promotion: the only transition

A discovery build becoming production work is often the right result. It may happen only when:

1. a named decision owner approves the promotion;
2. all fictions and unresolved risks are written down; and
3. hardening and adoption are planned as real work with real cost.

Without this step, the work can drift into production. The artifact may look technically sound while operational, security, support, and ownership work is still missing.

### Vocabulary

When leadership or clients say **POC**, they mean a State A discovery build. When they say **production**, they mean State B production work. The terms map directly. The State A/State B discipline keeps the difference clear even when people use different words.

### Philosophy and tone

This is an in-house program. It is intentionally not a copy of the Palantir-originated forward-deployed engineer model.

The focus is humanity and empathy in client work: understand the operation and the people in it. The goal is not to create proprietary lock-in or dependence on one platform or tool.

---

## 2. Prerequisites and the Technical Gate

### Who this course is for

This course is for an already-proficient full-stack engineer. You must be able to ship production software independently, read an unfamiliar codebase, and spend as much time with users as with code. This is not an entry-level engineering course.

### Technical skill areas: entry gate, not course content

These are prerequisites. The course does not teach them; it starts after them.

- **Linux:** shell, filesystem, processes, environment, and scripting
- **Frontend:** web UI development, components, state, and browsers
- **Backend:** server-side development, APIs, databases, and services
- **Data structures, algorithms, and system design:** scale, complexity, and tradeoffs
- **AI engineering:** cloud platforms, infrastructure as code, and production use of models and AI services
- **DevOps:** CI/CD, containers, deployment patterns, and observability tools

These skills are covered by external roadmaps and learning paths. They are admission requirements, not course modules. A participant who cannot work independently in most of these areas is not ready for this course.

### Assumptions in this draft

Changing these assumptions will not change the structure, but it may change the pace.

- **Cohort:** 4–6 engineers working together.
- **Duration:** 8 weeks, about 6–8 hours per week, alongside delivery work.
- **Support:** each cohort has one senior CAST engineer for technical and engagement judgment, one senior client lead for commercial and relationship questions, and access to a designer or product partner for workflow and usability review. Mentors are not full-time on the cohort.
- **Tooling:** participants use the client's approved stack and AI tools. Claude Code, Codex, or another coding agent may speed up delivery, but no specific tool is the point of the course.
- **Existing assets:** an engagement brief, discovery-build starter, security and data-handling rules, decision-log template, and AI Excellence Playbook. If these do not exist, program leadership must create them in Week 0.

---

## 3. The Six Product-Ownership Skills and the Product-Ownership Loop

The course teaches six connected skills.

1. **Own the problem.** Learn how the operation works. Do not treat the first request as the requirement.
2. **Clarify ambiguity.** Find unanswered questions that could change value, scope, safety, adoption, or cost.
3. **Specify the outcome.** Define the user flow, user stories, acceptance conditions, non-goals, and success measures.
4. **Set priorities.** Choose work using value, risk, uncertainty, dependencies, and effort. Do not choose only what is easy to code.
5. **Guide decisions.** Show options and consequences, include the right owners, and record the decision and its reason.
6. **Own the outcome.** Check usage, adoption, exceptions, and operational results after release. Recommend whether to stop, change, expand, or transfer the work.

### The product-ownership loop

Use this loop in every course exercise and client engagement:

1. Observe one recent case.
2. Map the current user flow.
3. Separate the request, symptom, problem, and outcome.
4. List important unknowns.
5. Ask questions that can change a decision.
6. Define the target user flow.
7. Write user stories and acceptance conditions.
8. Select the smallest useful slice.
9. State priorities, non-goals, assumptions, and stop conditions.
10. Build or simulate the slice.
11. Test it with operators.
12. Measure the result.
13. Recommend the next action: stop, change, expand, promote, or transfer.

The documents are evidence of product judgment. They are not the product. The learner must explain why the work matters, why it is ordered this way, and what evidence could change the plan.

### Product thinking is the decision layer

Product thinking is not a set of ceremonies, and it does not require acting like a product manager. It means making clear choices about:

- who matters;
- which problem is worth solving;
- what should change in user behavior or the operation; and
- how the organization will know that the change created value.

For each proposed intervention, answer these questions:

| Product question | Evidence to seek | Decision it supports |
|---|---|---|
| Who does the job and who feels the pain? | Recent cases, role observation, workflow evidence | Whose problem is primary and whose needs are constraints? |
| What is the job, not just the request? | Trigger, workaround, desired outcome | What problem are we actually solving? |
| Why change this now? | Baseline, frequency, cost, risk, strategic context | Whether to act, wait, or do nothing |
| What alternatives exist? | Process change, configuration, existing product, integration, build | Which intervention has the best value and ownership profile? |
| What behavior or operational result should change? | Target flow, adoption evidence, outcome metric | What success means and how to observe it |
| What must be true for the intervention to work? | Desirability, feasibility, viability, safety, and adoption assumptions | What to test before committing more effort |
| Who owns it after delivery? | Support model, technical owner, process owner, rollout plan | Whether the result can survive the engagement |

The engineer is not expected to make every decision alone. They must make the decision visible, explain the options and tradeoffs, involve the right owner, and keep the work connected to a user and an outcome.

---

## 4. Module 0: The Role and Its Edges

Half a day. Complete before joining a client session. This module is required.

Everything later is a technique. This module explains the judgment behind those techniques. Without it, an engineer may become faster at building what was requested without becoming better at deciding whether it should be built.

### 0.1 Why this role exists

Most product engineering starts after someone has translated the problem. You receive a roadmap item, design, ticket, acceptance criterion, or product manager who owns the ambiguity. The system boundary and customer context are mostly already understood.

CAST engineering starts before that translation is finished and stays involved longer. You work where the client's operation, people, data, policy, and software meet. The request is evidence, not a specification. You must find the real constraint, choose the narrowest useful intervention, put it into the client's environment, and stay long enough to show that it works and can be owned without you.

This role is needed when a general platform meets a specific customer operation. Translating the platform into that operation requires someone who understands the customer's processes well enough to configure, integrate, or extend the technology. That person needs both technical range and client judgment.

AI makes this problem more visible: general capability is widely available, but reliable use inside a real organization is still difficult.

> CAST does not mean “the engineer who travels,” “the engineer on sales calls,” or “the person who makes custom demos.” Your work must change a real operation and continue to work after you leave.

#### The two halves of the role

1. **Technical range:** enough breadth to work across an unfamiliar application, data model, integration, deployment path, and operational failure.
2. **Client translation:** enough judgment to understand real work, find the problem behind the request, explain tradeoffs, and help people reach a decision they can own.

You already have the first half. You can read unfamiliar code, reason about systems, and ship production changes. This course does not reteach those skills.

Your technical skill becomes more valuable when you can delay solutioning, learn from operators, and explain consequences without hiding behind implementation details.

You do not replace product, design, commercial, or client teams. You own the product thread inside the agreed boundary. You connect user evidence, product decisions, technical work, adoption, and outcomes.

#### The three ownership tests

Before calling work CAST, ask:

1. Did you learn how the operation really works from the people doing it?
2. Did your technical choices come from evidence rather than the first request?
3. Can the client run, support, and extend the result after you leave?

If any answer is no, the work may still be useful, but it is not complete.

The six skills and product-ownership loop are in Section 3. This module assumes you have read them. The documents remain evidence of judgment, not the product itself.

### 0.2 The two states of your work

Because your work ships, this distinction controls the whole role:

> **Everything you build is in one of two states, and you must always know which one. Moving between states requires an explicit sign-off.**

| | State A: Discovery build | State B: Production work |
|---|---|---|
| **Purpose** | Reduce a named uncertainty | Create an outcome people can depend on |
| **Lifespan** | Days | Indefinite |
| **Fictions** | Deliberate and listed | Defects, or temporary risks with named owners |
| **Required bar** | Enough evidence to decide | Secure, observable, maintainable, adopted, and operable |
| **Success** | A better decision, including “stop” | The outcome improves and the client can own it |

These are different jobs, not two quality levels.

A stubbed integration may be correct in State A if the question is whether an operator understands the workflow. The same stub is unacceptable in State B. On the other hand, building complete identity, monitoring, and recovery before knowing whether the workflow is useful can destroy the speed that makes discovery valuable.

Good production engineering habits can be harmful when applied too early. Build enough for the state you are in, and label it honestly.

#### The four State A questions

Every discovery build must answer at least one primary question:

1. **Are we solving the right operational problem?** A request for a dashboard may really be a data-delay, ownership, or approval problem.
2. **Will the people in the workflow use this solution?** Sponsor approval does not answer this. Operators do.
3. **Can the client's real data and systems support it?** A field in a slide does not prove that it exists, is reliable, accessible, or legally usable.
4. **Is the value large enough to justify production work?** Technical feasibility and economic value are separate questions.

Write the primary question at the top of the engagement brief. If the build cannot change a decision, it is a demo, not a discovery build.

#### Preserve the risky part

The test must include the uncertainty that could make the direction fail.

- If data quality is the risk, a polished UI over invented clean data proves nothing.
- If adoption is the risk, an API benchmark proves nothing.
- If integration permissions are the risk, a local stub proves nothing.
- If model accuracy on client documents is the risk, a generic benchmark proves nothing.

You may fake surrounding plumbing, but preserve the part that is genuinely risky.

#### What State A is not

- **Not a foundation:** reuse is a later decision, not a hidden requirement.
- **Not an estimate:** discovery speed does not predict production effort.
- **Not an architecture commitment:** the fastest way to learn may not be the right durable design.
- **Not a sales promise:** evidence may support a proposal, but it cannot authorize one.
- **Not production because an engineer wrote it:** clean code does not provide security review, operations, adoption, or ownership.

#### What State B requires beyond deployment

State B is not complete when CI is green or the release reaches production. The following must be true:

- intended users can complete the operational task;
- failure behavior and manual fallback are known;
- access, audit, retention, and privacy follow the client's controls;
- monitoring shows both system health and outcome failure;
- a named team receives alerts and knows how to respond;
- rollback and recovery have been exercised at a suitable level; and
- the client can maintain and extend the result without routing every change through you.

#### Promotion: the only legal way across

Promotion is an explicit review:

1. **A named owner decides.** Enthusiasm in a demo is not approval.
2. **The evidence is reviewed.** The decision must not be stronger than the evidence.
3. **Fictions and risks are listed.** Include stubs, shortcuts, sample data, manual steps, untested conditions, and missing owners.
4. **Hardening and adoption are scoped.** Security, operations, data, UX, rollout, training, and support are real work.
5. **The artifact changes state.** It now follows the client's production controls.

“The code is already pretty solid” is not enough. Production readiness belongs to the whole operating system around the code, not just the code.

### 0.3 Seven common failures

Each later module prevents one or more of these failures.

#### 1. The solution reflex — a discovery failure

The client says reconciliation takes three days. Before the operator finishes explaining, you draw an event pipeline and propose automated matching. The actual delay is a policy that requires a manager to review exceptions in a spreadsheet each afternoon.

**Why it happens:** engineers are trained and rewarded to converge, and familiar technical shapes feel like progress.

**What prevents it:** Module 1 requires following one recent case from start to finish before proposing a system.

#### 2. The technically correct wrong answer — an outcome failure

The integration is secure, tested, observable, and matches the requirements. Nobody uses it because it adds a second queue to a team measured on clearing the first queue.

**Why it happens:** the requirements described the feature but not the incentives and workflow around it.

**What prevents it:** operator observation, stakeholder mapping, and an outcome measure agreed before building.

#### 3. The accidental commitment — a commercial failure

A sponsor asks whether production is “basically another sprint.” You say the core logic is straightforward. The meeting notes turn that into a one-sprint commitment.

**Why it happens:** technical confidence is heard as organizational commitment, and qualifiers disappear when the answer is repeated.

**What prevents it:** the never-alone list and a rehearsed holding phrase.

#### 4. The clean-code promotion — drift in the artifact

The discovery build has types, tests, and a tidy architecture. Someone connects it to real data without reviewing retention, support, rollback, or human approval of AI output.

**Why it happens:** engineering quality creates a strong signal that hides missing operational work.

**What prevents it:** state labels, a faked list, and formal promotion review.

#### 5. The hero loop — drift in ownership

You know the client system best, so every difficult request comes to you. Six months later, reliability depends on your memory and the client team waits for you.

**Why it happens:** rescue behavior feels helpful and is often rewarded in the short term.

**What prevents it:** start ownership transfer on day one. Module 5 checks whether the client can operate without you.

#### 6. The invisible decision-maker — a relationship failure

The sponsor and operators approve the solution. Security blocks production access because no security owner was involved until release week.

**Why it happens:** enthusiasm is mistaken for authority, and stakeholder mapping is treated as administration.

**What prevents it:** name every owner whose approval, data, system, or team the work depends on.

#### 7. The outcome-free deployment — a State B failure

The service is live and dashboards are green, so the project is declared complete. The manual process continues because the team was not trained and a common exception is unsupported.

**Why it happens:** deployment is visible and easy to timestamp; adoption and operational change are slower and shared across teams.

**What prevents it:** outcome monitoring, an adoption plan, and an explicit client owner.

### 0.4 Where your authority ends

You may understand the implementation best. That does not make every related decision yours.

#### The never-alone list

Never decide these alone:

1. **Price, timeline, and contract scope.** Technical effort informs them but does not authorize them.
2. **Feasibility guarantees.** A promising test is not a guarantee across real data, load, policy, or adoption.
3. **Production access and release.** Follow the client's named owners and controls, even if you have credentials and can technically proceed.
4. **Data-use exceptions.** Do not reinterpret classification, consent, retention, residency, or approved-tool rules.
5. **Compliance or legal meaning.** Explain system behavior; do not declare compliance.
6. **Promotion.** You may recommend State B, but named owners authorize investment and risk.
7. **Long-lived architecture and ownership.** If the client inherits maintenance or lock-in, their technical owner must participate.

#### Why expertise does not expand authority

Expertise gives your words more weight. That makes casual answers more dangerous in a client setting.

“Technically possible” may be heard as “included.” “The data is encrypted” may be heard as “approved.” “I can ship this Friday” may be heard as a commitment. Make the missing decision visible without becoming evasive.

Escalation protects the real decision owners. It is part of good ownership. Advancement in this program requires evidence that you escalated something you could technically have done alone.

#### Escalation paths

Replace every placeholder with a real person before publishing the course.

| Question type | Goes to | When |
|---|---|---|
| Price, timeline, contract, or scope | *[senior client lead]* | Before responding |
| Promotion to State B | *[client decision owner]* + *[senior client lead]* + *[technical owner]* | Before commitment |
| Production access or release | *[client technical owner]* | Before action |
| Data classification or tool approval | *[security/data owner]* | Before data is accessed or moved |
| Compliance or legal interpretation | *[named compliance/legal owner]* | Before stating a position |
| Long-lived architecture | *[client technical owner]* + *[CAST lead]* | Before implementation |
| Client relationship problem | *[senior client lead]* | Immediately |
| Question you cannot categorize | *[CAST lead]* | Immediately |

#### The holding phrase

Use a sentence that separates a technical answer from a commitment:

> “I can tell you what the evidence says technically. Before we turn that into a delivery or compliance commitment, I need to involve the person who owns that decision.”

Write your own version and say it aloud. If it sounds like a refusal, make it more helpful. If it sounds like a promise, make the boundary clearer.

### 0.5 Framing exercise

**Assessed.**

A discovery build looks like software. Your technical credibility can make clients assume the hard part is finished. Replace that assumption with a clear evaluation frame.

Write five or six sentences for the first time you show a discovery build. Write for speech.

#### Version A — fails

> “This is an early prototype, but the architecture is pretty clean and the main integration works. We still need proper auth, monitoring, and some edge cases. Assuming there are no surprises in the client environment, production should be fairly straightforward.”

This sounds reasonable sentence by sentence, but together it creates a commitment. “Early” and “fairly straightforward” are vague. It does not say what decision the build supports. It presents an incomplete list of production work and suggests that only finishing work remains.

#### Version B — works

> “This build answers one question: can we match fields in your actual intake files reliably enough to remove the first manual sorting step? It uses the approved sample set, and a person still reviews every proposed match. The queue, identity, and downstream write are simulated because they do not affect that question. Today, we want your operations team to try the difficult files and show us where a suggested match would cause the wrong action. If the evidence is strong, the next step is a separate production review covering security, integration, operations, and rollout.”

The artifact is the same. The framing is different: the question comes first, the main risk is preserved, fictions are explained, the client has a specific job, and promotion remains a separate decision.

#### Your version must include

- one primary question in the first sentence;
- the real evidence or representative material being used;
- every relevant fiction stated plainly;
- why those fictions do not invalidate the test;
- a specific job for the client or operator;
- the possible next decision, without assuming the result; and
- no estimate, guarantee, or implied promotion.

Read it aloud. If it sounds like a demo narration, rewrite it. If it invites the client to challenge a claim, it is ready.

### 0.6 Close

Carry these five ideas into Module 1:

1. Your first answer is a hypothesis. Experience makes it better, not certain.
2. Always know the state. State A reduces uncertainty; State B creates a dependable outcome.
3. The client's operation is part of the system. People, incentives, approvals, workarounds, and policy matter.
4. Ownership includes leaving. If the result depends on your presence, the engagement is not finished.
5. Do not be unnecessarily cautious. State A mistakes are recoverable and should produce learning. Repeated failure without changing direction is not acceptable. Deliberate fictions create room to move, but they do not change the never-alone list or escalation duties.

Before Module 1, arrange access to one operator and one recent real example of their work. A process deck is not a substitute.

---

## 5. Module 1: Customer and Operational Literacy

Weeks 1–2. Twelve items, in dependency order.

### 1.1 What this module is for

Learn the operation before turning it into a software problem.

This may sound slower than building, but it is usually the fastest route to useful work. Discovering that the bottleneck is an approval rule can prevent a month spent optimizing the system that waits for approval.

#### What you are building toward

- a current-state workflow based on a real example;
- a stakeholder map with real decision rights;
- a problem statement that separates evidence from assumptions;
- an outcome measure with a baseline;
- a playback that the client recognizes as their reality;
- questions that can change a decision; and
- a current user flow that includes exceptions and manual work.

The people who perform the work judge the final assessment. Your mentor is not the only judge.

#### The stance

You will form hypotheses constantly. Hold them lightly enough that evidence can change them.

Use this format:

> “My current hypothesis is ____. The evidence is ____. The fastest way to prove me wrong is ____.”

This makes uncertainty useful and gives people something specific to correct.

### 1.2 Start with a recent real example

People describe ideal processes. Real cases contain the exceptions, workarounds, and missing information that affect the design.

Ask an operator to choose one recent case and walk through it from the event that started the work to the point where they considered it complete.

#### Questions that reveal the work

- What happened immediately before this reached you?
- What did you receive, and in what form?
- What did you check before acting?
- Which system did you open first, and why?
- What information was missing or unreliable?
- Where did you wait, ask, copy, retype, or leave the official system?
- What made this case easy or difficult?
- What happened when the normal path failed?
- Who received the work next?
- How did you know it was complete?

Do not read these as a questionnaire. Follow the case and keep asking “what happened next?” until the outcome is real.

#### Artifacts are better than memory

When policy allows, inspect the actual redacted file, screen, queue, form, message, or report. “The same spreadsheet” may arrive in twelve layouts. “An API” may be a nightly file export. “Approval” may mean a message to one particular person.

Handle artifacts under the client's data rules. If access is not approved, do not improvise. Record the limitation and use a client-prepared example.

#### Output

Write a case trace:

| Step | Person | Action | System or artifact | Friction or decision |
|---|---|---|---|---|
| Trigger | | | | |
| … | | | | |
| Outcome | | | | |

One case is the first evidence, not a complete picture of the process.

### 1.3 Map the current workflow

Combine the case trace with interviews and system evidence into a current-state map.

#### Include five types of information

1. **People:** the role doing the work, not only the department.
2. **Actions:** what the person actually does.
3. **Systems and artifacts:** applications, spreadsheets, inboxes, files, paper, and side channels.
4. **Data:** what enters, changes, and leaves.
5. **Boundaries:** handoffs, approvals, access changes, and ownership changes.

Start with the operation, not a service diagram. A service diagram can show data movement while hiding the manager who approves exceptions once a day.

Mark these items:

- wait time;
- repeated entry or copying;
- rework and loops;
- decisions and their criteria;
- exceptions and escalation;
- manual reconciliation;
- late information;
- work outside the official system; and
- steps nobody owns.

#### Documented versus actual process

Both views matter. The documented process shows what the organization believes should happen and may contain controls that must be preserved. The actual process shows how outcomes are produced today.

Record the difference without blaming the operator. Workarounds are often rational responses to systems that do not fit the work.

### 1.4 Build the stakeholder and decision map

“The client” includes several roles. One person may hold several roles, and several people may share one role.

| Role | What they own |
|---|---|
| Sponsor | Desired business result and organizational backing |
| Buyer or commercial owner | Contract and budget |
| Operator | Daily work and exceptions |
| Process owner | Workflow rules and performance |
| Technical owner | Systems, architecture, release, and maintenance |
| Data owner | Access, quality, permitted use, and lifecycle |
| Security/compliance owner | Controls and interpretation process |
| Administrator/support owner | Configuration, incidents, and user help |
| Adoption owner | Training, communication, and process change |

For each stakeholder, record:

- the outcome they want;
- what they fear losing;
- what evidence they trust;
- what decision they can make;
- what decision they can block; and
- when they need to be involved.

#### Enthusiasm is not authority

A sponsor may be excited but not control security. An operator may validate usability but not approve process change. A technical owner may approve architecture but not own adoption.

Every required decision needs a named owner. “The client will decide” is incomplete.

#### Missing-chair check

Before a decision meeting, check which affected teams, data owners, or budget holders are absent. Their absence may block work that appeared approved.

### 1.5 Separate request, symptom, problem, and outcome

These are related but different:

| Layer | Example |
|---|---|
| **Request** | “Build us a reconciliation dashboard.” |
| **Symptom** | “Reconciliation takes three days.” |
| **Problem** | “Analysts cannot identify the owner of unmatched records until two delayed files are manually combined.” |
| **Outcome** | “Analysts route unmatched records to the right owner during the same working day, with an auditable reason.” |

The request is useful evidence of the solution the client imagines. Do not dismiss it, but do not confuse it with the problem.

#### Working problem statement

Use this structure:

> **[Person or role]** cannot **[complete an operational job]** when **[condition]**, because **[evidence-backed constraint]**. This causes **[measured or observable consequence]**. We believe **[intervention hypothesis]** may improve **[outcome]**, and we need to test **[uncertainty]**.

If a field is unknown, write `unknown`. Do not turn an assumption into a plausible-sounding fact.

#### Baseline before target

Measure the current condition at a suitable level:

- time from trigger to outcome;
- active effort versus waiting;
- frequency and volume;
- error or rework rate;
- cost or revenue effect;
- risk exposure; and
- user or customer consequence.

Avoid false precision. “In eight sampled cases, five waited overnight for owner assignment” is stronger than an invented percentage.

### 1.6 Frame the product opportunity

Understanding the problem is necessary but not enough. Product thinking asks whether the problem is worth changing, for whom, and what intervention is responsible.

#### Do not call everyone “the user”

The operator may use the workflow, the customer may receive the result, the sponsor may fund it, the buyer may approve it, and the process owner may be accountable for performance. Their interests may conflict.

| Role | Question to answer |
|---|---|
| Operator | What job are they trying to complete, and what makes it difficult? |
| End user or customer | What result do they experience, and what would improve or worsen it? |
| Sponsor or buyer | Why does this matter now, and what investment or risk will they accept? |
| Process owner | Which outcome, policy, or service level do they own? |
| Technical, data, or security owner | What must be true for the intervention to be safe and supportable? |

#### Consider all intervention types

Do not assume the answer is a new feature. Consider:

- changing the process or policy;
- clarifying ownership or an approval rule;
- configuring an existing capability;
- buying or integrating an existing product;
- building a new capability; and
- intentionally doing nothing for now.

A custom build is justified only when it creates more value than the alternatives and the client can own the resulting obligation.

#### Product hypothesis

> We believe **[user or role]** struggles to **[job]** because **[evidence-backed constraint]**. If we **[intervention]**, they will **[behavior or operational change]**, resulting in **[measurable outcome]**. We will test this with **[evidence]**, and change direction if **[disconfirming signal]**.

Keep the product hypothesis separate from the technical hypothesis. “The API can process the file” is not the same as “the operator can complete the job faster and with acceptable risk.”

#### Output

Add a product opportunity note to the case trace:

1. primary user and affected roles;
2. job, pain, and consequence of inaction;
3. alternatives considered;
4. product hypothesis;
5. outcome, behavior, and guardrail measures; and
6. decision owner.

### 1.6a Surface the ideal end result

This is an account-management skill, separate from gathering requirements. Requirements describe what the client asks for. This exercise finds what the client wants to achieve, including possibilities they have not named.

Ask directly:

- “If this engagement went perfectly, what would your operation look like six months from now—not just the tool, but how the team works?”
- “Is there something you wish you could fix here but have not mentioned because it seemed too ambitious or out of scope?”
- “What must be true for you to call this a clear success, beyond what we have discussed?”

Also offer possibilities you notice. If observation reveals an adjacent problem or higher-leverage intervention, say so. The client hired you partly to see things they may be too close to notice. Naming a possibility is not scope creep: explain the tradeoffs and let the decision owner choose.

Keep this brief. One or two good questions and one or two specific suggestions are enough. The goal is an accurate ideal outcome, not a wishlist.

### 1.7 Ask questions that change decisions

Good discovery questions make a decision easier. Weak questions only collect opinions.

#### Prefer behavior over preference

Weak: “Would an automated summary help?”

Better: “Show me the last summary you created. What did you include, who read it, and what decision did they make?”

Weak: “How often does this happen?”

Better: “Looking at last week, which cases followed this path?”

Weak: “What features do you need?”

Better: “What must you know before you can take the next action?”

#### Clarify vague words

When someone says *usually, quickly, accurate, secure, simple, compliant, real time,* or *the business*, ask what it means here:

- “Usually: what happened in the cases that did not?”
- “Accurate enough for which decision?”
- “Real time compared with what deadline?”
- “Who specifically is ‘the business’ in this step?”

Ask one question, then allow silence. Do not answer your own question or offer architecture choices.

#### Record the effect of the answer

For each important answer, record:

- the question;
- the answer;
- the person or artifact that supplied it;
- the decision it affects; and
- the next action or owner.

A clarification question is useful when its answer can change scope, priority, user flow, safety control, acceptance condition, or stop condition.

### 1.8 Explain a system in the client's terms

Explain architecture, constraints, and failures in language that lets non-engineers participate.

Use this order:

1. **Outcome:** what this enables or prevents.
2. **Operational path:** who does what and when.
3. **Boundary:** where data, authority, or responsibility changes.
4. **Mechanism:** only the technical detail needed for the decision.
5. **Tradeoff:** what improves, what becomes harder, and who owns the consequence.

Instead of:

> “We will use an asynchronous event-driven pipeline with idempotent consumers.”

Say:

> “When a file arrives, the client system records it immediately and processes it in the background. If the same file arrives twice, it will not create two cases. This makes intake more reliable, but the operations team needs a queue for files that cannot be processed automatically.”

The second explanation exposes the consequence that needs a decision.

Draw two connected diagrams:

1. the operational view: people, actions, systems, data, and boundaries; and
2. the technical view: components, interfaces, stores, trust boundaries, and runtime ownership.

If a technical component cannot be tied to an operational need, ask why it exists. If an operational step has no technical or human owner, you found a risk.

### 1.9 Run and close a client session

A session is useful when it changes shared understanding or enables a decision.

#### Before

- Name the decision or artifact the session should produce.
- Invite the people needed for that purpose.
- Send material early enough to inspect.
- Assign a facilitator and note owner when possible.
- Decide what sensitive material may be shown or recorded.

#### During

- State the purpose and time limit.
- Separate facts, assumptions, decisions, and open questions in the notes.
- Park topics that matter but do not serve this session.
- Notice who is not speaking and whose work is being described by someone else.
- With ten minutes left, stop creating branches and converge.

#### Close

Read back:

1. decisions made;
2. evidence learned;
3. unresolved questions;
4. owner and due point for every follow-up; and
5. the next decision or session, with a named owner and date.

Send a short written playback while memory is fresh. Use the client's language and ask for corrections. The goal is to expose disagreement before code hides it, not to produce polished minutes.

### 1.10 Handle disagreement and uncertainty

Disagreement often reveals different incentives, definitions, or authority. Treat it as information.

#### Identify the disagreement

Ask which type it is:

- **Fact:** what is true today?
- **Prediction:** what is likely to happen?
- **Value:** which outcome matters more?
- **Risk tolerance:** what downside is acceptable?
- **Authority:** who has the right to decide?
- **Language:** are people using the same word differently?

More logs may resolve a fact dispute. They cannot decide who accepts a compliance risk.

#### Make options clear

For a technical choice, show:

| Option | Outcome enabled | Cost or constraint | Risk | Reversibility | Owner needed |
|---|---|---|---|---|---|
| | | | | | |

Do not hide your preferred option inside a supposedly neutral comparison. State your recommendation and reasoning, then name the decision owner.

#### Say “I do not know” completely

Weak: “I’m not sure.”

Better:

> “I do not know whether the source retains the field long enough for this audit. I will check the schema and retention policy with the data owner. That answer will determine whether we use the source or record the value ourselves.”

This acknowledges uncertainty and gives a concrete way to resolve it.

### 1.11 Assessment: play back the operation

**Task:** observe a real or simulated workflow and play it back to the people involved.

#### Deliverables

1. one recent case trace;
2. current-state workflow map;
3. stakeholder and decision map;
4. problem statement separating evidence and assumptions;
5. baseline and proposed outcome measure;
6. open questions with named owners;
7. one-page written playback;
8. product opportunity note with alternatives and product hypothesis;
9. clarification record showing how answers changed the problem, flow, or decision; and
10. note on the ideal end result, including possibilities you surfaced.

#### Live playback

You have ten minutes. Cover:

- where the work begins and ends;
- the people and systems involved;
- where time, error, risk, or rework enters;
- what you think the actual problem is;
- what remains uncertain; and
- what decision should happen next.

#### How it is judged

The strongest signal is that operators say, “Yes, that is how it actually works,” and then correct something specific. Correction is useful. A playback so vague that nobody can disagree has failed.

Your mentor also checks whether you:

- used real examples, not only general claims;
- proposed an outcome owned by the client, not by the software;
- separated operator, customer, sponsor, buyer, and decision owner where needed;
- considered process change, existing capability, and doing nothing alongside custom build;
- linked a behavior change to an operational outcome;
- identified missing decision-makers;
- kept evidence that contradicted your first idea;
- avoided promising a solution before Module 2;
- asked questions that could change the work; and
- asked about the ideal end result and suggested possibilities the client had not named.

---

## 6. Module 2: From Ambiguity to a Product Decision

Weeks 2–3. Twelve items, in dependency order.

### 2.1 Where this module fits

Module 1 created a shared view of the operation. Module 2 turns that view into a product decision and the smallest responsible piece of work.

Writing code can feel like certainty. A repository, schema, and plan can hide unresolved questions without answering them.

> **Every technical choice must point to evidence, an explicit assumption, or a named constraint.**

#### By the end, you can

- write a one-page engagement brief;
- write a product hypothesis and compare intervention options;
- choose one primary State A question or State B outcome;
- estimate value as a range, not a guarantee;
- define a target user flow;
- write and prioritize user stories;
- define observable acceptance conditions and non-goals;
- define outcome, behavior, and guardrail measures;
- check that the work still matches the problem;
- map the client systems, data, access, and ownership required;
- test risky assumptions before committing architecture;
- choose a thin slice that produces useful evidence or value;
- use AI coding tools within client data and review boundaries; and
- define stop conditions before momentum takes over.

This is not architecture astronautics, a generic discovery sprint, or permission to build a bespoke platform for a first request. The output is a bounded intervention with visible reasoning.

### 2.2 Write the engagement brief

The brief is the smallest shared contract between client reality and technical action. Keep it to one page when possible.

#### Required fields

**Operation**

- Who does what today?
- What event starts the workflow?
- What outcome ends it?

**Problem and evidence**

- What prevents the outcome?
- What recent examples support that claim?
- What is the baseline?

**Product case**

- Why act now?
- Who is the primary user, and who else is affected?
- What alternatives were considered: process change, configuration, buy, integrate, build, or do nothing?
- What is the product hypothesis, and what evidence would disprove it?
- What is the estimated value range if the intervention works? (See 2.4a.)

**Target outcome**

- What observable condition should change?
- Who owns the measure?
- When and how will it be checked?

**State and question**

- Is this State A or State B?
- If State A, what single uncertainty should the build reduce?
- If State B, what approved outcome and production controls apply?

**Boundaries**

- in scope and explicitly out of scope;
- approved data and environments;
- dependencies and decision owners; and
- never-alone decisions the work may reach.

**Assumptions and stop conditions**

- What are we treating as true?
- What evidence would stop or redirect the work?

#### Weak brief

> Build an AI assistant that reads claims, extracts details, and updates the case-management system. Use the existing model API and finish a prototype for stakeholder review.

This describes a solution but hides the operator, problem, evidence, permissions, risky assumption, and decision.

#### Working brief

> Claims analysts spend the first hour of each case copying six fields from emailed PDFs into the case system. In eight observed cases, three PDFs used layouts the current parser did not recognize, causing later rework. This State A build asks whether the approved model can propose the six fields from a representative redacted sample accurately enough to make analyst review faster than manual entry. The model will not write to the case system; the downstream action is simulated. We will stop or redesign if critical-field errors exceed the process owner's threshold, if the sample is not approved for the tool, or if review time is not lower than the baseline. Promotion is out of scope.

The second brief can be challenged. That is why it is useful.

### 2.3 Specify the operational change

Describe the operation, not only the software.

#### Choose the intervention before the implementation

The first product decision is not which framework or model to use. It is which intervention best balances user value, feasibility, safety, adoption, viability, and ownership.

| Option | Value created | Main tradeoff or risk | Reversibility | Owner after change | Why selected or rejected |
|---|---|---|---|---|---|
| Change process or policy | | | | | |
| Configure existing capability | | | | | |
| Buy or integrate | | | | | |
| Build | | | | | |
| Do nothing or defer | | | | | |

If an option is not credible, say why. The table makes the recommendation and consequences visible.

#### Define the target user flow

Start with the current flow from Module 1. Define:

- user;
- trigger;
- actions and decisions;
- normal result;
- common exceptions;
- unsafe result to prevent;
- manual or fallback steps; and
- final outcome.

Show what changes and what stays the same. Mark assumptions and open questions. Review the flow with the operators who do the work.

#### Write user stories

> As a **[user]**, I need to **[take an action]** when **[condition]**, so that I can **[reach an operational outcome]**.

Each story must have one user and one outcome. Do not write stories for a database, service, model, or internal component. Those may support a story, but they do not receive value.

#### Define acceptance conditions

For each story, define:

1. starting condition;
2. user action;
3. expected result;
4. result for a common exception;
5. unsafe result the design must prevent; and
6. evidence showing whether the story is useful.

“Works well,” “is easy,” and “is accurate” are not acceptance conditions. Define what they mean for this user and operation.

#### State non-goals

A non-goal is work the slice will not do. Write non-goals before implementation. They prevent polite requests and technical curiosity from expanding the work.

#### Set priorities

Rank stories using:

- user value;
- risk if an assumption is false;
- uncertainty;
- safety;
- adoption;
- dependencies; and
- effort.

Put the smallest useful end-to-end story first. Do not put infrastructure first unless it blocks that story. Record why each story is first, later, or out of scope, and what evidence could change the order.

#### Check alignment

Compare the brief, target flow, stories, acceptance conditions, success measure, and non-goals.

Ask:

- Does every story support the target outcome?
- Does every acceptance condition test the story?
- Does the first story preserve the main uncertainty?
- Does any planned work lack a user or outcome?
- Does any important exception lack an owner or response?
- Did a solution assumption become a hidden requirement?

Fix gaps before technical planning.

### 2.4 Choose the decision and evidence

A discovery build exists to change a decision. Write that decision before choosing the implementation.

#### Decision statement

> After this work, **[named owner]** should be able to decide whether to **[stop / test further / choose an approach / propose production work]** based on **[specific evidence]**.

Examples:

- The process owner can decide whether assisted extraction is worth proposing for production based on field accuracy and analyst review time across a representative sample.
- The technical owner can choose batch or event integration based on the required decision deadline, source availability, and failure recovery.
- The sponsor can stop the dashboard proposal if operators confirm that the delay occurs before data reaches the reporting system.

#### Measure value, behavior, and guardrails

| Measure type | What it tells you | Example |
|---|---|---|
| Outcome | Whether the operation improved | Time from intake to correct owner assignment |
| Behavior or adoption | Whether people use the change as intended | Share of eligible cases using the new path |
| Quality or guardrail | Whether improvement causes unacceptable harm | Critical-field errors, unresolved exceptions, or added review time |
| Operating cost | Whether the result is sustainable | Support effort, vendor cost, latency, or remaining manual work |

For each measure, name the baseline, target or threshold, observation window, source, and owner. A feature being available is a delivery fact, not a value measure.

#### Evidence table

| Claim | Observation needed | Source | Pass/redirect condition | Decision owner |
|---|---|---|---|---|
| | | | | |

Define this before building. Otherwise the team may treat whatever the build happens to show as evidence.

#### Match confidence to evidence

One operator session can reveal a workflow and create hypotheses. It cannot prove adoption across a department. Twenty clean sample documents cannot prove performance on rare formats that are not in the sample.

State conclusions only as strongly as the evidence allows.

### 2.4a Size the value before building

State A Question 4 is often left unanswered. This section gives a method.

#### Why size value in State A

This is not a business case or a return guarantee. It is a check that the problem is worth solving at its actual scale. A technically interesting intervention that saves two minutes per month per analyst may not justify production. One that saves 400 hours per year for a team of 20 might.

The estimate is advisory input for the decision owner. It is a hypothesis with a stated confidence level, never a commitment.

#### Estimate a range

Choose the main value mechanism:

| Mechanism | Estimate structure |
|---|---|
| Time saved | Cases or tasks per day × minutes saved per case × loaded hourly rate × working days |
| Error cost avoided | Case volume × current error rate × average rework or correction cost |
| Throughput or revenue enabled | Additional capacity × unit value per case or transaction |
| Risk exposure reduced | Probability of bad outcome × cost of outcome × reduction factor |

Use one mechanism or several if they are independent and additive. Report a range, not a precise number. Weak evidence requires a wider range; a month of production data may support a narrower one.

#### Example: claims analysts

> Each analyst handles about 60–80 cases per day. The current extraction step takes 45–60 minutes of active effort. If assisted extraction reduces this to 10–15 minutes, and the team has 12 analysts, annual time savings may be about 1,800–3,600 hours. At the agreed loaded rate, this is a direct-labor saving of [figure]–[figure] per year. Three of eight observed cases had parsing errors that caused about 90 minutes of rework. If the true error rate is about 10–15%, avoided rework may add [figure]–[figure] per year. Combined annual value range: [lower]–[upper]. Confidence: low to moderate, based on eight cases and operator estimates; a larger sample would narrow the range.

This is enough for a promotion discussion. It is not an audited figure and must not be presented as one.

#### Boundaries

Do not present this estimate as a commitment or feasibility guarantee. Commercial framing and feasibility guarantees belong to named owners under the never-alone list. If the estimate may enter a commercial conversation, route it through the senior client lead first.

When the intervention reaches production, compare the estimate with the realized measures from Sections 2.4 and 2.6. The gap shows how good the initial observation was; it is not by itself a verdict on the intervention.

### 2.5 Perform technical reconnaissance

Technical reconnaissance checks whether the client's real environment supports the intervention. It is not a complete architecture phase.

#### Map the terrain

| Component or data | Owner | Interface | Environment | Access path | Constraint or unknown |
|---|---|---|---|---|---|
| | | | | | |

Include:

- source and destination systems;
- identity and permission boundaries;
- data stores and lifecycle;
- interfaces and rate limits;
- deployment and release path;
- logging, monitoring, and audit sources;
- human review or approval points;
- vendor and licensing dependencies; and
- client teams expected to maintain the result.

#### Trace one representative record

Using approved data, follow one record from origin to outcome. Check:

- where each required field originates;
- whether the field means what people think it means;
- when it becomes available;
- whether it changes later;
- who may read or write it;
- which identifier links systems;
- how duplicates and corrections appear; and
- how failure becomes visible.

Reconnaissance means calling the approved interface with a representative case and checking semantics. It does not mean merely confirming that an API exists.

#### Read before replacing

If the client has an existing system, learn its conventions, tests, deployment controls, and ownership model. A locally elegant pattern that the client's team cannot maintain is an operational regression.

### 2.6 Classify data and access before using them

Client access is not permission to move information wherever it is convenient.

Before using data or tools, record:

- data classification;
- approved source and destination;
- permitted purpose;
- allowed people and service identities;
- retention and deletion expectations;
- residency constraints;
- whether prompts, logs, traces, or vendors retain content;
- whether synthetic or redacted data is required; and
- the named owner who approved the path.

> **No client credential, production record, personal data, confidential document, or restricted code may enter a repository, prompt, model, log, screenshot, or environment unless that exact use is approved.**

Approval for one path does not approve another. Production database access does not authorize copying records to local development. Approval for one model vendor does not authorize a different coding agent.

If the data path is unclear, stop, record the question, and ask the data or security owner. Do not quietly substitute your own judgment.

### 2.7 Find and test the riskiest assumption

List assumptions in five areas:

1. **Desirability:** operators will use or trust the intervention.
2. **Feasibility:** systems, data, and model behavior can support it.
3. **Viability:** the result justifies cost and ongoing ownership.
4. **Safety:** security, privacy, compliance, and operational risks can be controlled.
5. **Adoption:** the organization can change and support the workflow.

For each assumption, consider:

- impact if false;
- uncertainty;
- cost and time to test; and
- reversibility of proceeding without an answer.

Test high-impact, high-uncertainty assumptions early. Do not polish around an integration permission that may never be granted.

Preserve the real uncertainty: use poor scans if poor-scan behavior is risky; show suggestions to users if trust is risky; test the approval path if access is risky. A proxy is useful only when you can explain how it represents the real uncertainty.

### 2.8 Choose the thinnest useful slice

A thin slice crosses the operation from a real trigger to a meaningful outcome for a narrow case. It is not merely the easiest component to code.

Constrain four dimensions:

- **User:** one role or small group
- **Case:** one common, bounded path
- **System path:** minimum interfaces needed to preserve the risk
- **Outcome:** one observable improvement or decision

The slice must support the first user story. If it does not, change the slice or priority. Do not add technical work just because it may be useful later.

#### Useful thin slice

An analyst uploads one approved document type, reviews six proposed fields, corrects them, and exports a structured result. This can test extraction quality and review effort without writing to production.

#### Thin component, not a useful slice

A generic extraction API tested only on synthetic examples may provide technical information, but it does not show whether the operator can review the output or whether real documents contain the required information.

#### Manual steps are allowed in State A

A person may move a file, start a job, review an exception, or copy a result behind the scenes when that does not invalidate the question. Put every manual step in the faked list immediately so it is not mistaken for production architecture.

State what the slice cannot prove. Every slice excludes some evidence, and those exclusions must be visible before anyone sees the result.

### 2.9 Design the intervention with the client

Do not disappear after discovery and return with a finished solution.

Use artifacts as questions:

- Workflow map: “Where is this account wrong?”
- Technical map: “Which boundary or owner is missing?”
- Prototype: “What action would you take here?”
- Data sample: “Which values would make this unsafe to trust?”
- Option table: “Which consequence is unacceptable?”
- Runbook draft: “Who would receive this alert?”

Include the people who inherit the consequences:

- operators shape workflow and exception behavior;
- design or product partners review usability and service coherence;
- technical owners shape integration and maintainability;
- security and data owners define permitted handling;
- support and administrators define operating needs; and
- sponsors and process owners define outcomes and adoption.

Not everyone needs to attend every session. Everyone needed for a decision must be involved before the decision becomes expensive to change.

### 2.10 Use AI coding tools inside the boundary

Coding agents can speed up reconnaissance and implementation. They can also create confident claims, broad changes, and new data paths faster than you can notice them.

> **The AI Excellence Playbook governs this item. If this section differs from the Playbook, the Playbook wins.**

Delivery may involve directing several AI coding agents instead of writing every line by hand. This means fewer keystrokes and more architecture, review, and verification. It does not change accountability. A human with deep system understanding must direct and verify the work. These rules apply regardless of how many agents produce the output.

#### Give the agent grounded context

Provide only approved material:

- engagement brief;
- repository instruction files;
- specific acceptance evidence;
- the smallest relevant code and system context;
- explicit non-goals and protected boundaries; and
- verification commands.

A broad context window is not a substitute for a scoped task.

#### Separate modes

- **Reconnaissance:** find relevant code, interfaces, tests, and conventions. Check important claims directly.
- **Options:** propose approaches and tradeoffs. Treat them as hypotheses, not approval.
- **Scaffolding:** create a disposable State A structure quickly.
- **Constrained change:** define what may change, what must not change, and how success is checked.
- **Review:** use an independent pass to find edge cases, security issues, and mismatch with the brief. Independence helps but does not replace human accountability.

#### Before execution

- Compare proposed tasks with the brief, user flow, and stories.
- Remove tasks that do not support an agreed story.
- Add missing work for acceptance, exceptions, adoption, and measurement.
- Read the plan and inspect intended files and commands.
- Check network, secret, client-system, and broad-filesystem access.
- Reject unexplained dependencies and infrastructure changes.
- Commit or create a reversible checkpoint.

#### After execution

- Read the diff.
- Run proportionate tests.
- Verify behavior against the brief and evidence plan.
- Check changes outside the obvious path.
- Record every fiction or new assumption.

#### Never do this

- paste client credentials or restricted material into an unapproved tool;
- accept claims about the client's system without checking them;
- blanket-approve actions in a client repository;
- let generated polish expand the agreed scope; or
- call generated code production-ready because tests pass.

### 2.11 Assessment: defend the product decision

You receive a messy client request, a representative codebase or environment, and simulated stakeholders.

#### Deliverables

1. engagement brief, including a value range in the Product case field;
2. product hypothesis and alternatives table;
3. primary decision and evidence table;
4. value sizing with confidence;
5. measurement plan with outcome, behavior, guardrail, and operating-cost measures;
6. technical reconnaissance map;
7. data and access record;
8. ranked assumptions;
9. thin-slice plan;
10. faked list started before implementation;
11. stop or redirect conditions;
12. target user flow;
13. prioritized user stories;
14. acceptance conditions and non-goals;
15. alignment check; and
16. written client playback.

#### Review

In fifteen minutes, defend:

- why this is the right problem to act on;
- who the first user is and what outcome they need;
- why this intervention is better than process change, configuration, buying, integrating, or doing nothing;
- why the first story is first;
- the value range and how it was estimated;
- how value, adoption, quality, and operating cost will be measured;
- what was excluded;
- how acceptance conditions test value and failure;
- why this is State A or State B;
- what the work will and will not prove;
- which uncertainty is preserved;
- which parts are deliberately fake or manual;
- which owners and approvals are required;
- what evidence would make you stop; and
- how the client can own the next step.

#### How it is judged

- **Traceability:** technical choices point to evidence, assumptions, or constraints.
- **Thinness:** the slice is as small as possible while preserving the real risk.
- **Safety:** data, access, authority, and production boundaries are explicit.
- **Decision value:** the result helps a named owner make a better decision.
- **Product judgment:** the intervention is based on value, evidence, adoption, viability, and ownership, not a default choice to build.
- **Value sizing:** the estimate is a credible, evidence-based range with stated confidence.
- **Client fit:** operators and inheriting teams shaped the intervention.
- **Product ownership:** flow, stories, priorities, and acceptance conditions support the outcome.
- **Intellectual honesty:** unknowns and limitations are visible without becoming empty disclaimers.

The assessment rewards the clearest path from client evidence to a responsible next decision, not the most sophisticated architecture.

---

## 7. Workshop: Practiced Conversations and UI/UX Literacy

Half a day, after Module 2 and before Module 3. About 4 hours.

This workshop develops two skills that are difficult to learn by reading: handling client conversations under pressure, and recognizing usability problems well enough to brief and critique a design partner. Certification and deep specialization are not required. Deliberate practice is.

### Half A — Conversation practice drills

**About 60 minutes. Facilitated peer role-play with rotating partners. Not solo reading.**

Each drill is short and repeated across pairs. The goal is muscle memory, not performance. If a drill feels easy on the first attempt, it is probably too easy.

#### Drill 1 — The holding phrase

One person plays a client asking for price, delivery, or feasibility. The other gives a technically useful answer without making a commitment, using a version of the Module 0.4 phrase.

The drill fails if the answer is only a refusal or if it states a number or timeline as authoritative. Rotate after three rounds.

#### Drill 2 — One question, then silence

One person plays an operator. The other asks one discovery question from 1.7 and waits. The drill fails if the questioner speaks first or fills the silence with an architecture-based multiple-choice answer.

Run five rounds per pair with a different question each time.

#### Drill 3 — Name the disagreement, then show options

One person states a position. The other names the disagreement type—fact, prediction, value, risk tolerance, authority, or language—then shows two or three options using the 1.10 table. Make the recommendation and decision owner visible.

The drill fails if the disagreement type is skipped or the response argues without naming the owner.

#### Drill 4 — Say “I do not know” completely

One person asks a question the other cannot fully answer. The response must state what is unknown, identify the source that can resolve it, and name the next action. It must not be vague or evasive. Rotate after four rounds.

### Half B — UI/UX recognition-level literacy

**About 180 minutes. Use the creative-partner model.**

Engineers should be able to recognize and discuss usability problems and brief or critique a design partner. They are not expected to produce final UI/UX craft. That remains the design partner's job.

Out of scope: visual or brand craft, design-system authorship, production polish, and deep accessibility compliance work. Those belong to the design partner or accessibility specialist.

#### Part 1 — Visual hierarchy and core usability heuristics

Users scan screens rather than reading every word. Teach Z-pattern and F-pattern scanning. Compare a page with a clear focal point, logical order, and useful whitespace with a page where everything has equal weight and no next action is clear.

Teach these five heuristics. For each one, show a good and bad generic example and ask engineers to name the user harm.

1. **Visibility of system status:** users should know whether work is loading, processing, failed, or complete.
2. **Match to real-world language:** use client vocabulary, not internal system terms. “Unmatched record” is better than “entity resolution failure” for an analyst.
3. **Error prevention:** make wrong actions difficult or impossible. A form that accepts invalid dates and fails later is a prevention failure.
4. **Recognition over recall:** users should not need to remember information from another screen. A case number that disappears in a second tab creates a recall burden.
5. **User control and freedom:** users need undo, cancel, or back options. A form without cancel or save-draft removes control.

#### Part 2 — Form and error-state conventions

These conventions reduce operational errors; they are not merely style preferences.

- Place labels above fields, not inside them.
- Validate as early as possible with a specific message and a fix.
- Show inline errors next to the field that caused them, not only at the top.
- Confirm destructive or irreversible actions and describe the consequence.
- Explain why a list is empty and what the user should do next.
- Show loading for actions longer than one second. For actions longer than five seconds, show progress or an estimated time.

Participants critique one good and one problematic sample form using this vocabulary.

#### Part 3 — Accessibility red flags

This is spotting, not remediation. Flag these risks to a designer or accessibility specialist:

- **Color-only signals:** red-only errors are invisible to some color-blind users.
- **Tiny targets:** controls smaller than about 44×44 points are hard to tap, especially under stress or on mobile.
- **No keyboard path:** mouse-only actions block keyboard and assistive-technology users.
- **Poor contrast:** light text on a light background is hard to read, especially placeholder text and secondary labels.

Engineers must name the risk, describe the user harm, and flag it in critique or code review.

#### Part 4 — Brief and critique a design partner

A design brief should include:

- the user and operating context;
- the job to complete;
- the user's success condition;
- known constraints such as data classification, system conventions, and approved components;
- open questions for the design partner to decide or test; and
- what is out of scope.

A useful critique:

1. describes what you observed without interpretation;
2. names the heuristic or convention at risk;
3. describes the specific operational harm; and
4. asks a question rather than prescribing a fix.

Checklist:

- [ ] Is status visible at every step?
- [ ] Do labels and messages use client vocabulary?
- [ ] Can the user undo or cancel without losing work?
- [ ] Is the wrong action harder than the right action?
- [ ] Are errors next to the relevant field and specific about the fix?
- [ ] Do empty and loading states tell the user what to do next?
- [ ] Is any accessibility red flag present?

#### Part 5 — Hands-on practice

**Exercise A: critique a real client screen.** Use an approved client screen or a comparable public operational tool, not a consumer app. Apply the heuristics and explain what you would flag to a design partner.

**Exercise B: critique a peer's discovery prototype.** Check whether the UI could distort adoption evidence:

- Could polish create a false positive because the prototype looks finished?
- Could roughness create a false negative because users reject execution quality rather than the workflow?

Record at least one finding in each direction. The goal is to tune the prototype as evidence, not to improve its appearance.

#### Buffer

About 30 minutes for debrief, facilitator questions, and exercises that run over.

---

## 8. Modules 3–6: Summaries

**Full learner content for Modules 3–6 is not yet drafted. These are summaries for future authoring, not learner-facing content.**

### Module 3: Evidence, Verification, and Production Safety

**Weeks 3–4. The most important module in the program.**

The central risk is that a technically working system can still be wrong for the operation, unsafe, or impossible for the client to own.

#### 3.1 Evidence in State A

Define the observation that could change the decision before building. Test with operators, not only sponsors. Test the product hypothesis: can the intended user complete the job, will they choose the new path, and is the value enough to justify ownership?

Use representative edge cases. Record how sample data limits the conclusion. Keep an evidence log with claim, observation, source, confidence, and implication. List every fiction as soon as it is introduced.

**Assessment:** another participant tries to disprove the discovery claim. Passing means the claim becomes narrower and more accurate, not that it remains unchanged.

#### 3.2 Production safety in State B

Cover threat modeling, privacy review, access control, auditability, data lifecycle, failure modes, retries, idempotency, graceful degradation, manual fallback, and observability tied to outcome, adoption, and guardrails—not only infrastructure health.

Also cover feedback loops, migration, rollback, feature flags, support ownership, runbooks, performance, cost limits, realistic load, client release processes, and change controls. Client controls take priority over personal preference.

**Assessment:** release a representative change through a production-like process. Provide test evidence, threat and failure-mode review, observability view, rollback exercise, and operator-ready runbook.

### Module 4: The Client Conversation

**Weeks 4–5.**

Build instincts that product teams often spread across product management, design, sales, and customer success:

- **Question before answer:** establish the event, person, workaround, and desired change before responding to a feature request.
- **Precision without jargon:** explain architecture and tradeoffs in client language without becoming inaccurate.
- **Managing disagreement:** name the consequence, show evidence, and make the decision owner visible.
- **No accidental commitments:** route estimates, pricing, scope changes, compliance positions, and guarantees through their owners.
- **Showing State A:** frame the question and invite a specific test; never let polish imply readiness.
- **Showing State B:** demonstrate the operational path, failure behavior, monitoring, and ownership, not only the happy path.
- **Reading the room:** notice missing decision-makers, hidden risk, threatened teams, and polite agreement without commitment.
- **Technical writing:** write playbacks, briefs, handoffs, runbooks, and decision logs for a reader who will not have you there to explain them. Use client vocabulary, separate fact from assumption and recommendation, and state the open question and next owner.

**Assessment:** lead a simulated session where the request is not the real problem, stakeholders disagree, and the sponsor asks for an immediate commitment. Scoring covers discovery, clarity, boundaries, and written playback.

### Module 5: Adoption, Handoff, and Promotion

**Weeks 5–6.**

Deployment is a technical event. Adoption and ownership are the actual outcome.

#### 5.1 Handoff of a discovery build

Required deliverables:

- evidence log, including source and strength;
- faked list, including what a real version requires;
- decision log with choices, assumptions, constraints, and deferrals;
- open questions and why they matter;
- product case with user, outcome, alternatives, adoption conditions, and ownership implications; and
- recommendation: stop, test again, build a different slice, or propose promotion.

#### 5.2 Handoff of production work

Name the service, support, data, and business owners. Document decisions and operating procedures, not a tour of code already in the repository. Train administrators and support staff. Name an adoption owner and agree how usage, outcome movement, exceptions, and feedback will be reviewed.

Prove monitoring, alert routing, rollback, recovery, and manual fallback. Close engagement access and return or remove client data according to policy. Hold an end-of-engagement review covering outcome, remaining risks, debt, ownership, and the next decision.

#### 5.3 Run a promotion

Record the decision with a named owner. The evidence must be strong enough for the proposed investment. Include the value range from 2.4a and compare it with actual production effort and cost.

Turn the faked list into the hardening work list. Include security, data, compliance, operations, UX, and adoption gaps. Scope delivery and ongoing ownership before work starts. Agree measures, guardrails, review cadence, and stop or rollback conditions. Relabel the artifact State B and apply production controls.

**Assessment:** run a promotion review. Passing requires making the real work visible, including the option not to promote.

### Module 6: Capstone

**Weeks 6–8.**

A real, narrow, supervised engagement. The participant owns discovery, technical reconnaissance, delivery, and playback. A senior owns the commercial relationship and boundaries. The client must provide access to real operators and a technical owner.

Deliverables:

- engagement brief and stakeholder map;
- current-state workflow and technical reconnaissance map;
- build labeled State A or State B;
- verification and evidence record;
- decision log, faked list, and open questions;
- adoption or handoff plan; and
- recorded client playback and written next decision.

Start the debrief with the client outcome, not the architecture. What changed for the people doing the work? What evidence supports that? What happens after the engineer leaves?

---

## 9. Levels After the Program / What the Organization Has to Supply / Risks Worth Watching

### Levels after the program

Graduation does not mean permission to run a client engagement alone. Levels reflect the client authority, system risk, and ambiguity a person is trusted to handle.

| Level | Client responsibility | Trusted with | Can decide |
|---|---|---|---|
| **Shadow** | Observes and owns bounded follow-up | Paired State A tasks | Technical implementation inside an agreed plan |
| **Supported** | Leads discovery and delivery with a senior at decision points | State A end to end; State B in an approved design and release path | Reversible technical choices inside scope |
| **Embedded** | Runs day-to-day engagement | State A and State B within agreed outcomes and controls | Delivery choices inside scope; escalates never-alone decisions |
| **Lead** | Owns engagement shape and coaches others | Multi-workstream or high-risk delivery | Recommends scope, promotion, and architecture; named owners still approve |

Advancement is not based on time served or code volume. It requires evidence that the engineer:

1. changed direction when client evidence contradicted a technical preference;
2. escalated something they could have handled quietly; and
3. left the system and relationship operable without them.

The Supported → Embedded gate is mainly about judgment under ambiguity. Technical strength is required, but it is not what separates people who advance.

### What the organization must supply

The cohort cannot supply these prerequisites:

- real operators with protected time;
- a senior CAST engineer with mentoring time;
- a senior client lead for scope, pricing, and relationship escalation;
- access to design, security, data, and compliance partners at defined gates;
- an approved discovery environment and suitable representative data;
- versioned templates for the brief, evidence log, faked list, decision log, and production-readiness review;
- a safe first engagement with narrow scope, a cooperative client, reversible change, and no critical-path launch;
- a support and ownership policy for after the CAST engineer leaves; and
- a commercial answer for discovery work that creates unplanned production demand.

### Risks worth watching

**Solution reflex:** engineers turn the first sentence into architecture. Reward strong disconfirmation, not only fast output.

**Hero loop:** one engineer becomes the only person who understands the solution. Measure transferred ownership.

**Technical truth mistaken for the whole truth:** a technically correct statement may ignore incentives, workflow, policy, or adoption. Require operator evidence as well.

**Friendly scope change:** direct access makes small requests feel harmless. If the outcome, data use, or ongoing obligation changes, scope changed.

**Discovery theater:** interviews happen and notes are written, but the team builds the original idea anyway. Every brief should show what evidence changed.

**Sponsor-only validation:** a buyer approves something operators cannot or will not use. Do not recommend production without workflow evidence.

**Prototype laundering:** clean State A code looks safer than it is. Clean code does not replace threat modeling, support ownership, data controls, rollout, or adoption.

**Permanent embed:** every hard problem returns to the CAST engineer. The role succeeds when client capability increases, not dependence.

---

## 10. Future Direction: On-the-Fly Client Collaboration

**Future direction, not yet taught. Approximate horizon: 6–12 months after initial launch.**

A longer-term goal is live prototyping during client conversations. An engineer could create a working or near-working artifact during a discovery or alignment session: fill in a template, generate a first flow slice, or make a proposal concrete enough to test immediately. AI tools with product-thinking capability make this increasingly possible. Ready-to-fill templates and fixed structures will help.

This direction is still being explored. The tools and methods are not final. When ready, it may become an advanced module or Layer 2 of the capstone. It will not replace the observation, brief, and evidence-gathering disciplines in Modules 1 and 2. Those remain the foundation, regardless of delivery speed.

---

*End of CAST Product Engineering Curriculum.*
