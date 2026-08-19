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
8. [Module 3: Evidence, Verification, and Production Safety](#8-module-3-evidence-verification-and-production-safety)
9. [Module 4: The Client Conversation](#9-module-4-the-client-conversation)
10. [Module 5: Adoption, Handoff, and Promotion](#10-module-5-adoption-handoff-and-promotion)
11. [Module 6: Capstone](#11-module-6-capstone)
12. [Levels After the Program / What the Organization Has to Supply / Risks Worth Watching](#12-levels-after-the-program--what-the-organization-has-to-supply--risks-worth-watching)
13. [Future Direction: On-the-Fly Client Collaboration](#13-future-direction-on-the-fly-client-collaboration)

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

**Scenario.** You have just shown a State A extraction build to a client sponsor. The build worked on the sample files. The sponsor is pleased and wants to plan.

**The client says:**

> “This looks basically done. Can we have it live for the whole claims team by the end of next month? And roughly what would that cost?”

**You must:** give a technically useful answer about what the evidence shows, separate it from the delivery and cost commitment, and route the commitment to its owner — using your own version of the Module 0.4 holding phrase.

**Version A — fails:**

> “Probably, yes. The core logic is solid, so a month sounds realistic. Cost-wise it shouldn’t be huge — most of the work is already there.”

Every sentence sounds helpful. Together they commit a timeline and a price that are not yours to give, and “most of the work is already there” hides security, operations, adoption, and support.

**Version B — works:**

> “I can tell you what the evidence shows: on the approved sample, the extraction was accurate enough that analyst review beat manual entry. What I can’t give you is a delivery date or a cost, because production needs a separate review — security, integration, rollout, support. That decision belongs to [senior client lead] and your technical owner. I’ll flag it today so you get a real answer, not my guess.”

The client gets a genuine technical answer, the missing decision is named, and the next step has an owner.

The drill fails if the answer is only a refusal or if it states a number or timeline as authoritative. Rotate after three rounds.

#### Drill 2 — One question, then silence

**Scenario.** You are in discovery with an operator who processes intake files. You suspect the delay is upstream of the tool, but you do not know.

**The client (operator) says:**

> “Honestly, the system is just slow. If you could speed it up, that would fix most of it.”

**You must:** ask exactly one discovery question from 1.7 — behavior over preference — and then stay silent until the operator finishes. Example openers: “Walk me through the last file that was slow. What happened, step by step?” or “Looking at last week, which cases waited the longest, and where were they waiting?”

**The drill fails if** the questioner speaks first, stacks a second question onto the first, or fills the silence with an architecture-based multiple-choice answer (“Is it the database, the network, or the batch job?”). The role-player should pause for several seconds before answering, to make the silence uncomfortable on purpose.

Run five rounds per pair with a different question each time.

#### Drill 3 — Name the disagreement, then show options

**Scenario.** A process owner and a technical owner are in the same session and are talking past each other about a proposed automated routing step.

**The client (process owner) says:**

> “We can’t let the system route cases automatically. If it routes one wrong, that’s on my team. It has to stay manual.”

**You must:** first name the disagreement type aloud — this one is risk tolerance, possibly mixed with authority — then show two or three options using the 1.10 option table (for example: fully manual, suggested routing with human confirm, automatic routing with a review queue). State your recommendation and name who owns the decision.

**Version A — fails:**

> “The error rate is really low though. In testing it got 96% right, so the risk is small. I think automatic routing is fine.”

This argues the fact while the objection is about risk tolerance and accountability. The process owner heard “your concern is wrong,” and no owner was named.

**Version B — works:**

> “I think we disagree about acceptable risk, not about what the system can do — so let me show the options instead of arguing accuracy. Option one: keep routing manual, no new risk, no time saved. Option two: the system suggests a route and your team confirms it — most of the time saving, and a wrong suggestion is caught before it acts. Option three: automatic routing with a daily review queue — the fastest, but a wrong route acts before anyone sees it. My recommendation is option two for now. Whether that risk is acceptable is your call as process owner, not mine.”

The drill fails if the disagreement type is skipped or the response argues without naming the owner.

#### Drill 4 — Say “I do not know” completely

**Scenario.** During a playback, a data owner asks a question you cannot answer from evidence you have.

**The client says:**

> “Does the source system keep the original document long enough to satisfy our seven-year audit requirement?”

**You must:** state plainly what you do not know, name the source or person who can resolve it, and name the next action with an owner and a rough time. Vague hedging (“I’d have to look into that”) and confident guessing both fail.

**Version A — fails:**

> “I believe so — most systems like this keep documents for years. I wouldn’t worry about it.”

A guess presented as reassurance, on a compliance-adjacent question. This is exactly where expertise makes a casual answer dangerous.

**Version B — works:**

> “I do not know. I have not seen the retention configuration, and I won’t guess on an audit requirement. I’ll check the retention policy with your data owner this week. The answer decides whether we can rely on the source or need to store the document ourselves — so it changes the design, and I’ll bring it back before we commit to either.”

Rotate after four rounds.

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

**Worked example — a client screen with a hierarchy problem.** A claims work-queue screen shows forty columns of equal width, all in the same font size and weight. The one thing the analyst needs first — “which cases must move today?” — is a due-date column in position 31, formatted like every other column. Analysts scroll horizontally on every case and keep a paper note of urgent case numbers beside the screen. The fix is not a redesign: promote the due date and case status to the first scan position (top-left, where the F-pattern starts), give overdue rows one strong visual weight, and demote the reference columns behind a detail view. The paper note disappears because the screen now answers the analyst’s first question first.

#### Part 2 — Form and error-state conventions

These conventions reduce operational errors; they are not merely style preferences.

- Place labels above fields, not inside them.
- Validate as early as possible with a specific message and a fix.
- Show inline errors next to the field that caused them, not only at the top.
- Confirm destructive or irreversible actions and describe the consequence.
- Explain why a list is empty and what the user should do next.
- Show loading for actions longer than one second. For actions longer than five seconds, show progress or an estimated time.

**Worked example — a bad and a good error state.** An analyst submits a case-update form. The bad version: the page reloads, and a single red line at the top says “Validation error.” The analyst does not know which of eleven fields failed, the entered data in two fields is gone, and the case number they were working from is no longer visible. The good version: the form validates on the way in, keeps every entered value, marks the failing field inline — “Date of loss cannot be after today’s date (you entered 2027-03-14)” — and states the fix next to the field. Same form, same validation rule. One costs a re-key and a support call; the other costs one corrected field.

Participants critique one good and one problematic sample form using this vocabulary.

#### Part 3 — Accessibility red flags

This is spotting, not remediation. Flag these risks to a designer or accessibility specialist:

- **Color-only signals:** red-only errors are invisible to some color-blind users.
- **Tiny targets:** controls smaller than about 44×44 points are hard to tap, especially under stress or on mobile.
- **No keyboard path:** mouse-only actions block keyboard and assistive-technology users.
- **Poor contrast:** light text on a light background is hard to read, especially placeholder text and secondary labels.

Engineers must name the risk, describe the user harm, and flag it in critique or code review.

**Worked example — spotting one red flag.** A review screen shows proposed field matches. Matches the model is unsure about are marked only by turning the row text red; confident matches stay black. A color-blind analyst cannot tell the two apart, and this is the exact decision the screen exists to support — which rows need human attention. The correct flag to the design partner: “Uncertain matches are signaled by color only. An analyst who cannot distinguish red from black would review low-risk rows and skip high-risk ones. Can we add a non-color signal — an icon, a label, or a separate section?” Note the shape: risk named, harm described, question asked, no prescribed pixel-level fix.

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

**Worked example — briefing a design partner (short transcript).**

> **Engineer:** “The user is a claims analyst working through a queue of 60–80 cases a day, usually under time pressure and often interrupted. The job on this screen is: confirm or correct six extracted fields, then send the case forward. Success for the analyst is confirming a clean case in under a minute without fear of sending a wrong critical field. Constraints: the data is classified as confidential, so no third-party embeds; the client has an approved component library we must use; and the ‘policy number’ field has a legacy format we cannot change. Open questions for you: how should uncertain fields ask for attention without training analysts to ignore the signal, and should corrections happen inline or in a side panel? Out of scope for now: the queue screen and any mobile layout.”
>
> **Designer:** “Useful. One thing missing — what happens when the analyst rejects all six fields? Is that a normal path or an exception?”
>
> **Engineer:** “Good catch. It happened in two of eight observed cases, so it is a normal path. I will add it to the brief.”

Note what made the brief useful: user, context, job, success condition, constraints, open questions, and non-goals — and the engineer treated the designer’s question as a gap in the brief, not a challenge.

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

## 8. Module 3: Evidence, Verification, and Production Safety

Weeks 3–4. **The most important module in the program.**

The central risk of this role is that a technically working system can still be wrong for the operation, unsafe, or impossible for the client to own. Module 2 taught you to plan the evidence before building. Module 3 teaches you to collect it honestly in State A and to make State B safe to depend on.

The two halves of this module are different disciplines for the two states from Module 0.2. Do not mix them. Applying State B rigor to a two-day discovery build destroys its speed. Applying State A looseness to a production release creates the clean-code promotion failure from Module 0.3.

### 3.1 Evidence in State A

A discovery build exists to change a decision. Evidence discipline is what makes the change legitimate. Without it, the build shows whatever the builder hoped to see.

#### Define the decisive observation before building

Before writing code, write the observation that could change the decision. Use the evidence table from 2.4. If you cannot name an observation that would make you stop or redirect, you are building a demo, not a discovery build.

> **A discovery build that cannot fail is not evidence. It is theater.**

Ask, for the primary State A question from 0.2:

- What would we see if the answer is yes?
- What would we see if the answer is no?
- Who has to see it for the observation to count?

If the answer to the third question is “the sponsor,” look again. Sponsors validate enthusiasm. Operators validate workflows.

#### Test with operators, not only sponsors

The product hypothesis from 1.6 has three parts, and each needs its own observation:

| Hypothesis part | Observation that tests it | Observation that does not |
|---|---|---|
| The intended user can complete the job | An operator finishes a real task with the build, unassisted | A guided demo where you drive |
| They will choose the new path | An operator picks the new path when the old one is still available | An operator says “this looks useful” |
| The value justifies ownership | Measured time, error, or throughput change against the 1.5 baseline | A feature list mapped to the request |

Run sessions with the people who do the work. Give them their real task, on representative material, and watch without steering. The moment you explain a step, record it: an explained step is a step the design has not yet earned.

#### Use representative edge cases and state the sample limit

Clean samples produce clean lies. Include the difficult material on purpose: the poor scans, the twelve spreadsheet layouts from 1.2, the cases that took the workaround path.

Then state, in writing, what the sample cannot prove. Twenty documents from one region cannot prove behavior on another region's formats. Eight cases from one week cannot prove seasonal exceptions. This is the match-confidence-to-evidence rule from 2.4 applied at collection time, not at playback time.

#### Keep an evidence log

Record every meaningful observation as it happens, in this structure:

| Claim | Observation | Source | Confidence | Implication |
|---|---|---|---|---|
| | | | | |

Rules:

- One row per claim, not per session.
- The source is a person, artifact, or measurement — never “the team feels.”
- Confidence is stated in words tied to sample size, not invented percentages.
- The implication names the decision the row affects.

#### Worked example: evidence log for the claims-extraction build

The State A build from the 2.2 working brief, after three operator sessions:

| Claim | Observation | Source | Confidence | Implication |
|---|---|---|---|---|
| Assisted extraction is faster than manual entry for standard layouts | 14 of 16 standard-layout cases reviewed in 8–12 min vs 45–60 min baseline | Timed sessions, 3 analysts, redacted sample | Moderate — one office, standard layouts only | Supports the review-time pass condition in the brief |
| The model misses the claim date on scanned faxes | 4 of 5 fax-sourced documents required manual date entry | Session recordings, analyst B | Moderate — small fax sample, consistent failure | Fax path may need its own rule or stay manual; raise with process owner |
| Analysts trust the suggestions too quickly | Analyst C accepted 2 incorrect field proposals without checking the source document | Observation, session 3 | Low — one analyst, one session | Guardrail risk. Review UI must make checking cheaper than accepting; retest |
| Real intake volume is higher than reported | Queue export shows 90–110 cases/day vs "60–80" stated in interviews | Queue system export, week of [date] | High — system data, full week | Value range in 2.4a is understated; recompute before promotion talk |

Notice what the log does. Row 3 is bad news about the build and is recorded anyway, with a retest action instead of a defense. Row 4 corrects an earlier interview claim with system data — the log holds evidence that contradicts your own inputs. A log that contains only good news is a sales document.

#### List every fiction as soon as it is introduced

The faked list started in 2.11 is live during the build, not reconstructed afterward. Every stub, manual step, sample-data substitution, and skipped control gets a line the moment it exists, with what a real version would require. A fiction recorded late looks like a fiction hidden.

#### Adversarial review: narrowing a claim

Before evidence leaves the team, another participant tries to disprove the discovery claim. The reviewer's job is to attack the inference, not the person: sample bias, missing edge cases, observer effect, sponsor-only validation, proxy risk from 2.7.

Passing this review does not mean the claim survived unchanged. It means the claim came out narrower and more accurate.

#### Worked example: a claim narrowed, not killed

**Original claim:** “Assisted extraction makes analyst review faster than manual entry.”

**Reviewer:** “All sixteen timed cases came from the metropolitan office. The regional offices are the ones with the fax intake — and your own log says the model misses dates on faxes. Also, your three analysts volunteered. Volunteers are not the median analyst.”

**Weak response (fails):** “The fax cases are rare, and the volunteers weren't unusually senior. The claim basically holds.”

**Strong response (works):** “Both points change the claim. Revised: *for typed standard layouts, which are about 70% of metropolitan intake, assisted review beat manual entry across three analysts. Fax-sourced documents are not yet supported, and regional-office layouts are untested.* The recommendation changes too: the promotion case rests on the metropolitan typed path only, and the regional question becomes a named open item for the process owner.”

The narrowed claim is smaller and more useful. The decision owner can now act on it without inheriting a hidden overreach.

#### 3.1 Assessment: defend the evidence

**What you hand in:**

1. the evidence log for your Module 2 thin slice, with at least one row that contradicts your own earlier assumption;
2. the live faked list, with the real-version requirement per fiction;
3. a one-paragraph statement of what the sample cannot prove; and
4. the written claim you intend to give the decision owner, before and after adversarial review.

**How it is judged:**

- Another participant runs the adversarial review live. **Passing means the claim becomes narrower and more accurate, not that it remains unchanged.** A claim that survives review word-for-word is treated as a review that failed, unless the reviewer's attacks were answered with evidence already in the log.
- The mentor checks that operators, not only sponsors, supplied the decisive observations; that confidence language matches sample size; that fictions were logged when introduced; and that bad news appears in the log with an action, not a defense.

### 3.2 Production safety in State B

State B work must be safe to depend on and possible for the client to own. This item covers the review disciplines that the promotion checklist in 0.2 assumes exist. The client's own controls take priority over everything here: **if the client's release process and this section differ, the client's process wins.**

#### Threat model the operation, not just the code

Before a State B change ships, walk the operational path and ask, at each step: who could do the wrong thing here, what data is exposed, and what does the system do when the step lies, fails, or repeats?

Cover, at minimum:

- access control and ownership checks on every read and write path;
- auditability: who did what, when, visible to the client's audit function;
- data lifecycle: classification, retention, deletion, and residency from 2.6, now enforced rather than recorded;
- privacy review for any personal data the change touches; and
- the human approval points the workflow map from 1.3 says must be preserved.

#### Worked example: threat and failure-mode walkthrough for a release

The promoted claims-extraction service is about to write proposed fields into the case system for the first time. The walkthrough table for the release review:

| Path step | What can go wrong | Consequence | Control | Owner |
|---|---|---|---|---|
| Email intake receives a PDF | A crafted attachment reaches the parser | Parser compromise inside the client network | Sandboxed parsing, file-type allowlist, no macro execution | Client technical owner |
| Model proposes six fields | A wrong critical field is proposed confidently | Wrong payout routing downstream | Analyst confirmation is mandatory; no unreviewed write path exists | Process owner |
| Duplicate email arrives | The same case is created twice | Two analysts work one claim; conflicting records | Idempotent case creation keyed on source message ID | Engineer / technical owner |
| Case system write fails | Confirmed fields are lost after analyst review | Analyst re-keys work; trust in the tool drops | Retry with backoff; on exhaustion, park in a visible exception queue with the confirmed values preserved | Support owner |
| Model vendor is unavailable | No proposals for incoming cases | Intake stalls if the tool is the only path | Manual fallback: the pre-existing manual entry path stays available and documented | Process owner |
| Audit asks who confirmed a field | No record of the confirming analyst | Audit finding | Confirmation events logged with analyst identity and timestamp, retained per policy | Data owner |

Two things to notice. First, every row has a named owner — a control without an owner is a wish. Second, the manual fallback row exists because State B success in 0.2 includes “failure behavior and manual fallback are known.” A system whose failure mode is “the operation stops” has exported its risk to the operators.

#### Engineer for failure: retries, idempotency, degradation

Assume every dependency will fail, repeat, and lie at some point:

- **Retries** must be bounded and visible. An invisible infinite retry is an outage that reports success.
- **Idempotency** at every boundary where the same trigger can arrive twice. The 1.8 example — “if the same file arrives twice, it will not create two cases” — is the standard, stated in client language.
- **Graceful degradation** means the operation continues, worse, rather than stopping. Define what “worse” looks like with the process owner before it happens.
- **Manual fallback** is a documented, trained path — not the memory of whoever built the system.

#### Observe outcomes, not only infrastructure

Green dashboards caused the outcome-free deployment failure in 0.3. Monitoring must answer three questions, in this order:

1. **Outcome:** is the operational measure from 2.4 moving? (Time to correct owner assignment, error rate, throughput.)
2. **Adoption and guardrails:** are eligible cases using the new path, and are the guardrail measures inside their thresholds? (Share of cases through the tool; critical-field error rate; exception-queue depth.)
3. **System health:** latency, errors, saturation, cost.

Most monitoring stacks answer only the third. If outcome and adoption are not observable, the promotion review in 5.3 has nothing to check the 2.4a value estimate against.

#### Worked example: an alert tied to an outcome

Infrastructure-only alert (insufficient): *“extraction-service error rate > 2% for 5 minutes.”* True, actionable for an engineer, and silent about the operation.

Outcome-tied addition (required): *“exception-queue depth > 25 cases OR share of intake cases completed through assisted review < 60% for one business day → notify support owner and process owner.”* This fires when the operation is degrading even if every service is healthy — for example, when analysts have quietly gone back to manual entry because trust dropped. That signal is invisible to infrastructure monitoring and is exactly the signal the adoption owner needs.

#### Rollback, migration, and feature flags

- Every State B change needs a rehearsed way back. “We would restore from backup” is a hypothesis until it has been exercised at a suitable level.
- Migrations get a tested reverse path or an explicit, owner-approved statement that the change is one-way, with the consequence written down.
- Feature flags let adoption ramp gradually and cut exposure fast, but every flag is operational debt: record who owns each flag and when it dies.

#### Support ownership and runbooks

A runbook is written for the person on support at 02:00 who has never met you. It states: the symptom as the operator sees it, how to confirm the cause, the safe action, the rollback trigger, and who to call past which point. Documenting decisions and operating procedures beats narrating code that is already in the repository.

#### Performance, cost, and realistic load

Test at the volume the queue export showed, not the volume the interviews claimed (see the 3.1 log, row 4). Set a cost limit with an owner before launch — model-backed services can fail financially while succeeding technically.

#### 3.2 Assessment: release through a production-like process

**What you hand in:**

Release a representative change through a production-like process — the client's real process where available, the program's template process otherwise. The package contains:

1. test evidence proportionate to the change;
2. the threat and failure-mode review table, with a named owner per control;
3. the observability view showing outcome, adoption/guardrail, and system-health measures;
4. the record of a rollback actually exercised, with what was observed; and
5. an operator-ready runbook.

**How it is judged:**

- The mentor and, where available, a client technical owner run the release review as they would a real one. The change does not pass because the code is good; it passes because the operating system around the code is complete.
- Specific checks: does every failure mode have a control and an owner; does monitoring answer the outcome question before the infrastructure question; was the rollback exercised rather than described; could a support person who has never seen the code act on the runbook; and did the client's controls take priority over the engineer's preferences anywhere they differed.
- One planted gap is common in this assessment (for example, a migration with no reverse path). Finding and naming a gap the reviewers know about scores higher than a polished package that walks past it.

---

## 9. Module 4: The Client Conversation

Weeks 4–5.

By this point you can find the problem, plan the evidence, and build safely. This module trains the conversations in which all of that either survives or dies. It consolidates instincts that product companies usually spread across product management, design, sales, and customer success — because in a CAST engagement, you are often the only person in the room from your side.

Nothing here replaces the never-alone list from 0.4. This module teaches you how to sound while honoring it.

### 4.1 Question before answer

When a feature request arrives, the trained reflex is to respond with a solution shape. Replace it with a short factual reconstruction: establish the event, the person, the current workaround, and the desired change — then respond.

> **Client:** “Can you add an export-to-spreadsheet button on the queue?”
>
> **Weak:** “Sure, that's a small change. CSV or Excel format?”
>
> **Better:** “Probably — help me understand it first. What happened last time you needed that export? Who used the spreadsheet, and what did they do with it?”
>
> **Client:** “Every Friday, Maria copies the open cases into a sheet for the regional call, because the queue can't show last week's closed cases next to this week's open ones.”

The request was a button. The fact is a weekly manual report built on a missing comparison view. The button would have shipped, worked, and left Maria copying cells every Friday. One question changed what should be built — and this is Skill 1 and 2 from Section 3 executed in ten seconds of conversation.

### 4.2 Precision without jargon

Use the 1.8 ladder — outcome, operational path, boundary, mechanism, tradeoff — under conversational pressure, without becoming inaccurate. Jargon has two failure modes and both lose the room: the client stops participating, or the client nods and later discovers they agreed to something they did not understand.

> **Client (technical owner):** “Why is the nightly sync sometimes missing records?”
>
> **Weak (jargon):** “There's an eventual-consistency window on the replica, so reads during the sync can be stale.”
>
> **Weak (dumbed down, now inaccurate):** “Sometimes computers just lag a bit. It always sorts itself out.”
>
> **Better:** “The copy of the data we read from can run a few minutes behind the system your team writes to. If the sync starts inside that window, it misses the newest records — they arrive the next night, so nothing is lost, but Monday's report can be short. If a same-day guarantee matters for that report, we can read from the primary system instead; the tradeoff is more load on it during business hours, which is your call to accept or refuse.”

Precision survived — the mechanism, the consequence, and the tradeoff are all intact — and the sentence ends by handing the decision to its owner.

### 4.3 Managing disagreement

Apply the 1.10 discipline live: name the disagreement type, show evidence, make options and consequences visible, and name the decision owner. The Workshop's Drill 3 practiced the mechanics; this item adds the judgment about consequence.

The key addition: **name the consequence of each position, not the weakness of each person.** “If we route automatically and a route is wrong, a case acts before anyone sees it — and that lands on your team's numbers” advances the conversation. “You're being too cautious” ends it.

When the disagreement is between two client stakeholders, do not become the referee. Restate each position in its owner's terms, show the option table, and route the decision to whoever owns that consequence. You are the person who makes the disagreement precise, not the person who wins it.

### 4.4 No accidental commitments

The accidental commitment from 0.3 is the most expensive sentence in this role. Estimates, pricing, scope changes, compliance positions, and guarantees all route through their owners — and the routing must sound helpful, not evasive.

The pattern that works has three parts: give the technical fact, name the missing decision, name the owner and the next step.

> **Client sponsor:** “So if we sign next week, this is live in a month, right?”
>
> **Weak:** “That should be doable if nothing surprising comes up.” *(Heard as: one month, committed.)*
>
> **Weak:** “I can't discuss timelines.” *(Heard as: this person is hiding something.)*
>
> **Better:** “Here's what I can say from the evidence: the extraction quality question is answered for typed documents, and the remaining work is integration, security review, and rollout — real work whose size depends on your release process. Timeline and commercial terms belong to [senior client lead]; I'll brief them today with the technical picture so you get a date that will actually hold.”

Watch for the repeat trap: a qualified answer loses its qualifiers each time someone repeats it. “Should be roughly a month, assuming access” becomes “a month” in the meeting notes and “promised in four weeks” in the steering deck. If a number must not travel, do not say the number.

### 4.5 Showing State A

Presenting a discovery build applies the 0.5 framing exercise to a live audience. The rules, condensed:

- the primary question comes first, before anyone sees a screen;
- fictions are stated plainly, with why they do not invalidate the test;
- the client gets a specific job — “try your difficult files and show us where a suggested match would cause the wrong action” — not an invitation to admire; and
- the next decision is named without assuming its outcome.

**Never let polish imply readiness.** If the audience starts planning rollout during the demo, that is your cue, not a compliment:

> “Before we plan anything — a reminder of what this is. It answers one question about extraction quality. The queue, identity, and downstream write on this screen are simulated. Whether this becomes a production system is a separate review with its own owners, and today's evidence is one input to it.”

Saying this while the room is excited is the skill. Saying it after the meeting notes are written is damage control.

### 4.6 Showing State B

A State B demonstration is not a happy-path tour. It demonstrates that people can depend on the system, which means showing the parts that only matter when things go wrong:

1. the operational path, driven by an operator where possible, not by you;
2. the failure behavior: what a stuck case looks like, where the exception queue is, what the manual fallback is;
3. the monitoring view, starting from the outcome and adoption measures of 3.2, not from CPU graphs; and
4. the ownership: who gets the alert, who runs the runbook, who owns adoption.

A useful test for the session: could the client's support owner, watching this demonstration, take the pager tonight? If the honest answer is no, the demonstration is showing a feature, not production work.

### 4.7 Reading the room

Four signals to watch for, each with the move it demands:

| Signal | What it looks like | Your move |
|---|---|---|
| Missing decision-maker | Security, data, or the affected team's lead is not present while their domain is being decided | Run the missing-chair check from 1.4 aloud: “Before we treat this as decided — this touches data retention. Should [data owner] see it first?” |
| Hidden risk | A vague deflection: “that part's a bit political,” “let's not open that today” | Do not force it in the room. Note it, and follow up privately with the person who deflected |
| Threatened team | Operators go quiet when automation of their work is discussed; questions turn hostile on details | Name what stays human, honestly. If the intervention does reduce roles, that is a sponsor conversation, not a thing to soften with false reassurance |
| Polite agreement without commitment | “Sounds good” from everyone, and no one takes an action item | Convert agreement to ownership before closing: “Who owns the sample-file pull, and by when?” If no one does, the agreement was not real |

Silence is data. In the 1.11 playback, the strongest signal was operators correcting you. In any session, the person whose work is being described and who says nothing is the person to ask directly.

### 4.8 Technical writing

Write playbacks, briefs, handoffs, runbooks, and decision logs for a reader who will not have you there to explain them. In a CAST engagement your documents travel further than you do: into steering meetings, procurement reviews, and the inbox of the engineer who inherits the system.

Rules that apply to every document type:

- use client vocabulary, not internal system terms (the 1.8 discipline in writing);
- separate fact, assumption, and recommendation — visibly, not by tone;
- state every open question with its owner and the decision it blocks; and
- write the next decision, its owner, and its date. A document that ends without a next step is a report, not an instrument.

#### Worked example: weak vs strong written playback

**Weak:**

> “Great session today! The demo went well and everyone was positive about the direction. A few small issues came up around data that we'll iterate on. Next steps: continue building and sync again soon.”

Nothing in this can be corrected, actioned, or audited. “Everyone was positive” hides who committed to what. “A few small issues around data” may be the retention question that decides the architecture. There is no owner, date, or decision anywhere.

**Strong:**

> “**What we tested:** three analysts reviewed assisted extraction on 16 typed cases and 5 fax cases from the approved sample.
>
> **Facts:** typed-case review took 8–12 minutes against a 45–60 minute baseline. 4 of 5 fax cases required manual date entry. Queue data shows 90–110 cases/day, above the 60–80 estimated in interviews.
>
> **Assumptions we are still making:** regional-office layouts behave like metropolitan ones. Untested.
>
> **Recommendation:** the promotion case should rest on the typed metropolitan path only.
>
> **Open questions:** (1) Does source-system retention meet the seven-year audit rule? Owner: [data owner], blocks the storage design. (2) Is the fax path in scope? Owner: [process owner].
>
> **Next decision:** [process owner] decides fax-path scope by [date]. Corrections to any fact above are welcome — that is what this document is for.”

The strong version is barely longer. Every sentence can be verified, corrected, or acted on — and the last line invites the correction that 1.9 says a playback exists to provoke.

### 4.9 Assessment: lead the session

**Task:** lead a simulated client session, played by mentors and peers. By design: the request on the table is not the real problem, two stakeholders disagree, and the sponsor pushes for an immediate commitment. You will not be told which is which.

**What you hand in:**

1. your session plan (purpose, invited roles, and the decision the session should produce, per 1.9);
2. the session itself, observed live or recorded;
3. the written playback, sent within one working day, in the 4.8 structure; and
4. a short self-review: which signals from 4.7 you caught, which you missed, and what you would say differently.

**How it is judged:**

- **Discovery:** did you reconstruct the event, person, workaround, and desired change before responding to the planted request?
- **Clarity:** did explanations survive the 4.2 test — accurate, in client language, tradeoffs and owners visible?
- **Boundaries:** did the commitment push get the three-part response from 4.4 — fact, missing decision, owner — without a number escaping? Any accidental commitment fails the attempt outright, however well the rest went.
- **Disagreement:** did you name the type, show consequences, and route the decision to its owner rather than winning the argument?
- **Written playback:** judged with the 4.8 example as the bar — facts separated from assumptions, open questions owned, a next decision named.
- Scoring rewards recovering well over performing smoothly. Catching your own accidental commitment and correcting it in the room scores higher than a session where the role-players simply failed to trap you.

---

## 10. Module 5: Adoption, Handoff, and Promotion

Weeks 5–6.

**Deployment is a technical event. Adoption and ownership are the actual outcome.** This module covers the three endings an engagement can have: handing off a discovery build, handing off production work, and running a promotion between the two. Each ending is real work with its own deliverables — not a wind-down.

The failure this module prevents is the hero loop from 0.3. Ownership transfer starts on day one; this module is where it is proven.

### 5.1 Handing off a discovery build

A discovery build's product is a decision, so the handoff package must let a named owner decide — possibly months later, possibly without you in the room. The artifact itself may be deleted; the evidence must survive.

#### Required deliverables

1. **Evidence log** — the 3.1 log, with source and strength per claim, including the claims that went against your preference.
2. **Faked list** — every fiction, with what a real version requires. This becomes the hardening work list if promotion happens (5.3).
3. **Decision log** — the choices made, with the assumption or constraint behind each, and what was deliberately deferred.
4. **Open questions** — each with why it matters and which decision it blocks.
5. **Product case** — user, outcome, alternatives considered, adoption conditions, and what ownership would cost the client (from 1.6 and 2.3).
6. **Recommendation** — exactly one of: stop, test again, build a different slice, or propose promotion — with the evidence rows that support it.

#### Worked example: handoff excerpt for the extraction build

> **Evidence log (excerpt):** “Typed metropolitan cases: assisted review 8–12 min vs 45–60 min baseline across 3 analysts, 16 cases. Confidence moderate (one office). Fax documents: 4 of 5 required manual date entry — fax path unsupported as tested.”
>
> **Faked list (excerpt):** “(1) Case-system write is simulated — a real version needs the write API, idempotent case creation, and the process owner's approval of an assisted-write path. (2) Sample was pre-redacted by the client — a real version needs a redaction step or an approved data path for raw documents. (3) Analyst corrections are not persisted — a real version needs correction storage, which triggers the seven-year retention question (open item 1).”
>
> **Decision log (excerpt):** “Chose review-and-confirm over auto-write: analyst C's unchecked acceptances (evidence row 3) made an unreviewed path indefensible. Deferred multi-language support: zero non-English documents in the observed sample; revisit only with regional evidence.”
>
> **Recommendation:** “Propose promotion, scoped to the typed metropolitan path. Fax and regional paths: test again before any commitment. This recommendation is input to the 5.3 review, not an approval.”

Note the connective tissue: the faked list points at open questions, the decision log cites evidence rows, and the recommendation stays inside the never-alone boundary from 0.4.

#### How to hand it over

Walk the decision owner through the package in one session, in this order: question, evidence, recommendation, what the evidence cannot say. Then confirm in writing who holds the package and where it lives in the client's own systems. A handoff that lives only in your drive has not happened.

### 5.2 Handing off production work

State B handoff is complete when the client can run, support, and extend the result without routing changes through you — the third ownership test from 0.1, now with proof.

#### Name every owner

| Ownership | Named person confirms |
|---|---|
| Service owner | “I own this system's availability and change process.” |
| Support owner | “My team receives the alerts and can act on the runbook.” |
| Data owner | “The data paths, retention, and access match what I approved.” |
| Business/process owner | “I own the outcome measure and the workflow.” |
| Adoption owner | “I own training, communication, and usage review.” |

“The client will own it” is the same incomplete sentence 1.4 warned about. Every row needs a name, and each named person confirms in the handoff review — not in absentia.

#### Document decisions, train people, prove operations

- Documentation covers decisions and operating procedures — why the system is shaped this way, what to do when it misbehaves. It is not a tour of code already visible in the repository.
- Train the administrators and support staff on the real system, with a real exception, before you leave. Watching them handle one exception unassisted is the test; a slide deck is not.
- Prove, live in the handoff review: monitoring shows the 3.2 outcome and guardrail measures; an alert reaches the support owner's actual channel; rollback and manual fallback have been exercised; and the adoption owner has a review cadence for usage, outcome movement, exceptions, and feedback.

#### Worked example: the alert that proved the handoff

At a handoff review, the engineer triggered a synthetic stuck-case alert. It fired correctly — into the engagement channel that would be archived two weeks later. On paper, monitoring was done; in reality, every future alert would have gone to a dead room. The fix took ten minutes. The lesson is the discipline: **prove the operational path end to end with the people who will own it, in the channels they will actually watch.** A checklist inspects artifacts; a handoff review exercises them.

#### Close cleanly

Close engagement access and return or remove client data according to policy — your credentials still working three months later is a security finding, not a convenience. Hold an end-of-engagement review covering the outcome against the 2.4 measures, remaining risks and debt with owners, the ownership map, and the next decision the client faces without you.

### 5.3 Running a promotion

Promotion is the only legal transition from State A to State B (0.2). This item turns that rule into a runnable review.

#### The promotion review, step by step

1. **A named owner decides.** Confirm before the meeting who can authorize the investment and risk. If no one in the room can, the meeting is a briefing, not a review.
2. **Evidence is weighed against the investment.** The evidence log and its confidence limits on one side; the real cost of production on the other.
3. **The value estimate meets the cost estimate.** Bring the 2.4a value range forward and put it next to the actual promotion investment — hardening, integration, rollout, training, and ongoing ownership, not just build effort. The comparison is the heart of State A Question 4, now with real numbers on both sides. If the realized evidence moved the range (as in the 3.1 log, where measured volume exceeded interview estimates), recompute before the review, and say which way it moved.

   > **Example:** “The 2.4a estimate was 1,800–3,600 analyst-hours saved per year; measured intake volume raises the lower bound to roughly 2,400. The promotion investment is an estimated 10–14 engineer-weeks of hardening and integration plus a support obligation the client technical owner sizes at a quarter of one administrator. Even at the bottom of the value range, the investment recovers in well under a year — the case holds without optimistic assumptions. If it only held at the top of the range, the honest recommendation would be to narrow the range first, not to promote.”

4. **The faked list becomes the hardening work list.** Every fiction gets a task, an owner, and a place in scope: security, data, compliance, operations, UX, and adoption gaps included. A fiction with no task is a defect being smuggled into production.
5. **Delivery and ongoing ownership are scoped before work starts.** Who builds, who reviews, who supports, at what cost — agreed, not implied.
6. **Measures, guardrails, cadence, and stop conditions are agreed.** The 2.4 measurement plan becomes the production scoreboard; the review sets thresholds and a stop-or-rollback condition with an owner.
7. **The artifact changes state.** Relabel it State B and apply the client's production controls from that moment. There is no “mostly promoted.”

#### Worked example: promotion review walkthrough

> **Decision owner (process owner, confirmed in advance):** “Walk me through it.”
>
> **Engineer:** “The question this build answered: can assisted extraction beat manual entry for typed metropolitan cases? Evidence says yes — 8 to 12 minutes against a 45 to 60 minute baseline, three analysts, moderate confidence. It says nothing about fax or regional paths; those stay out of this proposal.
>
> The value range, recomputed on measured volume, is [lower]–[upper] per year. The investment is 10–14 weeks of hardening plus the support obligation your technical owner sized. The case holds at the bottom of the range.
>
> The faked list is now the work list: real case-system write with idempotent creation, the redaction step, correction storage pending the retention answer — that open question blocks the storage design and belongs to [data owner] before week two.
>
> Guardrail for the rollout: critical-field error rate above your threshold for two consecutive weeks stops the assisted path and reverts to manual, and you own that trigger.
>
> **The alternative is not promoting.** The build answered its question; stopping here costs nothing but the opportunity. If the retention answer comes back badly, stopping is my recommendation.”

Passing this review requires making the real work visible — including the option not to promote. A review where “no” was never a live option was theater, and the reviewers score it as such.

### 5.4 Assessment: run the ending

**What you hand in:**

Using your Module 2–3 engagement (real or simulated):

1. the complete discovery handoff package from 5.1;
2. a production handoff plan from 5.2 — ownership table with names, runbook, training plan, monitoring proof plan, access-closure checklist; and
3. a promotion review, run live, with a mentor or client stakeholder as the named decision owner. The value-versus-investment comparison from 5.3 step 3 must appear explicitly.

**How it is judged:**

- **Decision-readiness:** could the named owner decide from the package alone, with you out of the room? The reviewer will test this by asking a question whose answer must be in the package, not in your head.
- **Honesty of the faked list:** planted or self-introduced fictions missing from the list fail the attempt. A fiction found and listed late scores below one listed when introduced, but above one hidden.
- **Value-versus-investment reasoning:** the comparison uses the range honestly — a case that only holds at the top of the range must say so.
- **The no-promotion option:** the review must show what stopping looks like and when it would be the right call. If “stop” was never presented as a real option, the review fails regardless of polish.
- **Ownership transfer:** every ownership row has a name and a confirmation, and at least one operational path (alert, rollback, or fallback) is proven live rather than described.

---

## 11. Module 6: Capstone

Weeks 6–8.

The capstone is a real, narrow, supervised client engagement — not a classroom exercise. The participant owns discovery, technical reconnaissance, delivery, and playback end to end. A senior owns the commercial relationship and the boundaries. Everything from Modules 0–5 is in play at once, on a real operation, with real people inheriting the result.

Because it is real, the engagement must be chosen carefully. A bad capstone assignment fails the participant, the client, or both.

### 6.1 Selecting a capstone engagement

The organization supplies the engagement (see Section 12). Program leadership screens candidates against these criteria before assignment. Sharpened for the capstone specifically:

| Criterion | What it means for a capstone | Reject when |
|---|---|---|
| Narrow scope | One workflow, one primary operator group, one bounded outcome — completable inside three weeks alongside supervision | The engagement needs multiple workstreams or touches several departments' workflows |
| Cooperative client | The client knows this is a supervised training engagement and accepts the cadence | The client expects a normal delivery team and would experience supervision as friction |
| Reversible change | Any change made can be rolled back or switched off without residue | The intervention includes a one-way migration or an irreversible process change |
| No critical-path launch | The engagement is not on anyone's launch, audit, or regulatory deadline | A slipped week would damage the client or the relationship |
| Real operators available | Named operators with protected time, per Section 12 — the 1.11 and 3.1 assessments are impossible without them | Operator access is “we'll find someone when you need them” |
| A real but bounded decision at stake | A named client owner genuinely needs the answer the engagement produces — a real State A question, or a small real State B outcome | The client is doing the cohort a favor and no decision hangs on the result (discovery theater by design) |
| Low blast radius | If everything goes wrong, the damage is one team's wasted time and a rollback — never data loss, compliance exposure, or customer-visible failure | The workflow touches regulated data paths, payments, or customer-facing commitments the participant would have to get right first try |
| A technical owner who engages | The client's technical owner attends recon and the promotion or handoff review | No technical counterpart exists, so ownership cannot transfer |

The tension to manage: the decision must be real enough that evidence matters, and small enough that a wrong turn is recoverable. An engagement that fails the “real decision” test teaches performance. One that fails the “blast radius” test gambles the client relationship on a trainee.

### 6.2 Week-by-week cadence

The capstone runs weeks 6–8, alongside the participant's remaining delivery load. The senior attends the marked checkpoints; between them, the participant runs the engagement.

**Week 6 — Discovery, brief, and reconnaissance.**

- Days 1–2: operator sessions; one recent case traced (1.2); current-state workflow map (1.3); stakeholder and decision map (1.4).
- Day 3: problem statement, baseline, product opportunity note, ideal-end-result questions (1.5–1.6a). **Checkpoint: senior reviews the stakeholder map and never-alone exposure before any client playback.**
- Days 4–5: engagement brief with value range (2.2, 2.4a); technical reconnaissance and one traced record (2.5); data and access record (2.6). **Checkpoint: brief review with senior and client decision owner. The brief must name the single State A question or the bounded State B outcome. No building before this sign-off.**

**Week 7 — Build, test, evidence.**

- Days 1–3: thin slice built (2.8), faked list live from the first fiction (3.1), AI tools inside the 2.10 boundary.
- Days 3–4: operator evidence sessions; evidence log maintained per 3.1. For State B work: threat and failure-mode review per 3.2. **Checkpoint: mid-week evidence review with senior — is the risky part still preserved, or has the build drifted toward a demo?**
- Day 5: adversarial review of the discovery claim by a cohort peer (3.1). The claim that leaves week 7 is the narrowed one.

**Week 8 — Recommendation, handoff, playback.**

- Days 1–2: handoff package assembled (5.1 or 5.2 as the state requires); recommendation written; if promotion is proposed, the value-versus-investment comparison prepared (5.3).
- Day 3: **Checkpoint: dry-run of the playback with the senior.** Accidental-commitment risks rehearsed out.
- Day 4: recorded client playback; promotion or next-decision review with the named client owner; written playback sent within one working day (4.8).
- Day 5: access closure, data return per policy (5.2), and the program debrief (6.5).

If the engagement produces a “stop” recommendation in week 7, the cadence does not collapse — weeks 7–8 complete the evidence, the handoff package, and the playback for the stop decision. **A well-evidenced stop is a passing capstone.** Manufacturing a build to have something to show is a failing one.

### 6.3 Deliverables

The full set, labeled and dated:

- engagement brief and stakeholder map;
- current-state workflow map and technical reconnaissance map;
- the build, labeled State A or State B;
- verification and evidence record (the 3.1 log, plus 3.2 artifacts for State B work);
- decision log, faked list, and open questions;
- adoption or handoff plan (5.1 or 5.2); and
- recorded client playback and the written next decision.

Every deliverable already has a quality bar defined in its home module. The capstone adds no new formats — it tests whether you produce them under real conditions without being asked.

### 6.4 Grading rubric: the three advancement proofs

Advancement after the program (Section 12) requires evidence that the engineer (1) changed direction when client evidence contradicted a technical preference, (2) escalated something they could have handled quietly, and (3) left the system and relationship operable without them. The capstone is designed to be the place where all three proofs are produced. The senior grades against this rubric:

| Proof | What the capstone must show | Where the evidence lives | Fails when |
|---|---|---|---|
| **Changed direction on evidence** | At least one place where operator or system evidence overturned the participant's initial hypothesis or preferred design, and the work visibly changed | Evidence log rows that contradict the brief's first hypothesis; decision log entries citing them; the narrowed claim from the adversarial review | The final build matches the day-one idea and the log contains only confirming evidence (discovery theater) |
| **Escalated beyond their reach** | At least one never-alone item (0.4) that the participant could technically have resolved alone was routed to its owner instead — a data-path question, a scope change, a commitment push, a promotion call | The escalation itself: the message to the owner, the open-questions list, the 5.3 review where the owner decided | Three weeks of client contact produced zero never-alone moments — which means one was missed, not that none occurred |
| **Left it operable without them** | The named client owners can run the result — or act on the stop/promotion decision — with the participant gone | The confirmed ownership table; the exercised alert/rollback/fallback (5.2); a handoff package that survived the reviewer's “answer must be in the package” test | Any path where the honest answer to “what happens when X breaks?” is “they'd call the participant” |

Each proof is graded **demonstrated / partially demonstrated / not demonstrated**, with the citation into the deliverables. “Partially demonstrated” on one proof can pass with a documented follow-up; “not demonstrated” on any proof means the capstone is not passed, whatever the build's quality. Technical excellence with all three proofs missing is precisely the profile this program exists to correct.

### 6.5 Debrief

**The debrief starts with the client outcome, not the architecture.** The opening questions, in order:

1. What changed for the people doing the work?
2. What evidence supports that?
3. What happens after you leave?

Only after those three does the conversation reach how the thing was built.

#### What you hand in

1. the full deliverables set from 6.3;
2. the recorded playback and the written playback as sent to the client;
3. a self-assessment against the three proofs in 6.4, citing your own deliverables — claiming a proof without a citation counts as not claiming it; and
4. the senior's observation notes from the checkpoints.

#### How it is judged

- The senior and one program lead run the debrief. The participant answers the three opening questions first, unaided by slides.
- The 6.4 rubric is scored with citations, in the participant's presence — the reasoning is part of the teaching.
- Client-side signal is collected directly: did the decision owner get a decision they could act on; do the named owners confirm they can operate the result; would the operators have the participant back? The last question is asked of operators, not sponsors.
- The outcome of the debrief is a level recommendation per Section 12 (Shadow, Supported, Embedded), with the evidence for it. Graduation does not mean permission to run a client engagement alone; the debrief says what the participant is trusted with next, and why.

### 6.6 Example capstone scenarios

Three illustrations of the shape a good capstone takes. Each is one operation, one operator group, one bounded decision, low blast radius.

**Insurance claims intake (State A).** A claims team's analysts spend the first hour of each case re-keying fields from emailed PDFs. The bounded decision: is assisted extraction accurate enough on the client's real document mix to justify a production proposal? The build proposes fields on an approved redacted sample; an analyst confirms every field; the case-system write is simulated. Operators are available, the process owner genuinely needs the answer, and if the answer is no, the client has lost nothing but a few analyst-hours of sessions. This is the course's running example scaled to exactly capstone size.

**Field-service scheduling exceptions (State A).** A utility contractor's dispatchers manually re-plan the day whenever a job overruns, phoning technicians in sequence. The stated request is “an AI scheduler.” The bounded decision: where does re-planning time actually go, and would a suggested-next-technician view change dispatcher behavior? The build reads a day's completed jobs from an export and shows suggestions beside — never instead of — the existing board. Reversible, no write path to the dispatch system, and a real chance the evidence says the bottleneck is the phone calls, not the planning — a direction-change proof waiting to happen.

**Accounts-payable invoice matching (small State B).** A finance team already validated, in an earlier discovery, that a three-way-match exception report saves reconciliation time. The bounded outcome: put the report into production for one business unit — real access controls, an exception queue with a trained owner, an exercised fallback to the manual process, and an outcome measure (reconciliation hours) with a baseline. Scope is one report and one unit; rollback is switching the report off. This variant exercises the 3.2 and 5.2 disciplines rather than discovery, and suits a participant whose Module 1–2 work was strong but whose production-safety evidence is thinner.

---

## 12. Levels After the Program / What the Organization Has to Supply / Risks Worth Watching

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

## 13. Future Direction: On-the-Fly Client Collaboration

**Future direction, not yet taught. Approximate horizon: 6–12 months after initial launch.**

A longer-term goal is live prototyping during client conversations. An engineer could create a working or near-working artifact during a discovery or alignment session: fill in a template, generate a first flow slice, or make a proposal concrete enough to test immediately. AI tools with product-thinking capability make this increasingly possible. Ready-to-fill templates and fixed structures will help.

This direction is still being explored. The tools and methods are not final. When ready, it may become an advanced module or Layer 2 of the capstone. It will not replace the observation, brief, and evidence-gathering disciplines in Modules 1 and 2. Those remain the foundation, regardless of delivery speed.

---

*End of CAST Product Engineering Curriculum.*
