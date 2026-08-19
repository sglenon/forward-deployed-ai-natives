# CAST Product Engineering
### A course for CAST engineers who must own the problem, the product decision, and the outcome

---

## Assumptions in this draft

Change these and the structure still holds, but the pacing will shift.

- **Cohort:** 4–6 engineers, run together rather than individually.
- **Duration:** 8 weeks, roughly 6–8 hours per week, alongside existing delivery work.
- **Support:** each cohort has one senior CAST engineer (technical and engagement judgment), one senior client lead (commercial and relationship questions), and access to a designer or product partner for workflow and usability review. Mentors are not full-time on this.
- **Prerequisites:** able to ship production software independently, comfortable reading an unfamiliar codebase, and willing to spend as much time with users as with code. This is not an entry-level engineering course.
- **Tooling:** participants use the client's approved stack and AI tooling. Claude Code, Codex, or another coding agent can accelerate delivery, but no particular tool is the point of the program.
- **Existing assets:** an engagement brief template, a discovery-build starter, security and data-handling rules, a decision-log template, and the AI Excellence Playbook. If these do not exist, building them is Week 0 and belongs to program leadership, not the cohort.

---

## The thesis of the program

A product engineer is usually given a problem that has already been translated: a ticket, a design, an acceptance criterion, a system boundary. A CAST engineer works before that translation is complete. They sit close enough to the client's operation to see where the stated request is wrong, incomplete, or aimed at a symptom, then stay responsible long enough to put a durable change into use.

The program teaches a repeatable form of product and technical judgment under client pressure: observe before proposing, turn ambiguity into testable claims, select the smallest useful change, and stay responsible until the client can use and own the result.

The course changes the starting point: where a product engineer typically receives a translated requirement, a CAST engineer starts with an unclear operational need and must clarify it, define the product outcome, select the right intervention, and verify that it works in the operation.

The engineer does not replace every product, design, commercial, or client role. The engineer owns the product thread inside the agreed boundary. This thread connects user evidence, product decisions, technical work, adoption, and outcomes.

If involvement stops at advice, discovery, or a demo without shipping, the work is consulting or prototyping under a different title. The governing idea is therefore the same one that anchors the related design program:

> **Everything you build is in one of two states, and you always know which one. Moving between them is a decision someone signs off on, never something that just happens.**

### State A: Discovery build

Purpose: reduce a named uncertainty. Lifespan: days. Fictions are deliberate: sample data, a stubbed integration, or a manual step may be correct craft. The bar is enough evidence to decide, including deciding not to build.

The four questions a State A build is allowed to answer:

1. Are we solving the right operational problem?
2. Will the people in the workflow use this shape of solution?
3. Can the client's real data and systems support it?
4. Is the value large enough to justify production work?

### State B: Production work

Purpose: create an outcome people can depend on. Lifespan: indefinite. Any fiction or shortcut is a defect. The work must be secure, observable, maintainable, adopted, and operable by someone other than you. Success requires that the intended users can use it, the client can run it, and the agreed outcome moves without unacceptable regressions.

This covers changes to a client's live system and any discovery build that has been formally promoted.

### Promotion: the only legal transition

A discovery build becoming production work is often the right outcome. It happens exactly one way: a named decision owner approves it, the fictions and unresolved risks are written down, and a hardening and adoption pass is scoped as real work with real cost.

The alternative is drift, where the artifact appears technically sound before the operational, security, and support work is complete.

---

## The product ownership skills

The course teaches six connected skills.

1. **Own the problem.** Learn how the operation works. Do not treat the first request as the requirement.
2. **Clarify ambiguity.** Find the unanswered questions that can change value, scope, safety, adoption, or cost.
3. **Specify the outcome.** Define the user flow, user stories, acceptance conditions, non-goals, and success measures.
4. **Set priorities.** Select work by user value, risk, uncertainty, dependencies, and effort. Do not select work only because it is easy to code.
5. **Guide decisions.** Show options and consequences. Include the correct owners. Record the decision and its reason.
6. **Own the outcome.** Check use, adoption, exceptions, and operational results after release. Recommend whether to stop, change, expand, or transfer the work.

### The product ownership loop

Use this loop in each course exercise and client engagement.

1. Observe one recent case.
2. Map the current user flow.
3. Separate the request, symptom, problem, and outcome.
4. List important unknowns.
5. Ask clarification questions that can change a decision.
6. Define the target user flow.
7. Write user stories and acceptance conditions.
8. Select the smallest useful slice.
9. State priorities, non-goals, assumptions, and stop conditions.
10. Build or simulate the slice.
11. Test it with operators.
12. Measure the result.
13. Recommend the next action: stop, change, expand, promote, or transfer.

The documents serve as evidence of product judgment, not as the product itself. The learner must explain why the work matters, why it has this order, and what evidence can change the plan.

### Product thinking is the decision layer

Product thinking is not a set of ceremonies or a requirement to behave like a product manager. It is the habit of making explicit choices about who matters, which problem is worth solving, what should change in their behavior or operation, and how the organization will know the change created value.

For every proposed intervention, the learner should be able to answer:

| Product question | Evidence to seek | Decision it supports |
|---|---|---|
| Who has the job and who experiences the pain? | Recent cases, role observation, workflow evidence | Whose problem is primary and whose needs are constraints? |
| What is the job, not just the request? | Trigger, current workaround, desired outcome | What problem are we actually addressing? |
| Why is this worth changing now? | Baseline, frequency, cost, risk, strategic context | Whether to act, wait, or do nothing |
| What alternatives exist? | Process change, configuration, existing product, integration, build | Which intervention has the best value and ownership profile? |
| What behavior or operational result should change? | Target flow, adoption evidence, outcome metric | What success means and how it will be observed |
| What must be true for the intervention to work? | Desirability, feasibility, viability, safety, and adoption assumptions | What to test before committing more effort |
| Who will own it after delivery? | Support model, technical owner, process owner, rollout plan | Whether the result can survive the engagement |

The engineer is not expected to make every decision alone. They are expected to surface the decision, make the options and tradeoffs legible, bring in the right owner, and keep the work connected to a user and an outcome.

---

## Module 0: The role and its edges
**Half day. Complete before joining a client session.**

Content:

- Why the role exists: the failure is usually translation between a general capability and a specific operation, not a shortage of features.
- The distinction between product engineering, solutions engineering, consulting, and CAST engineering. The boundaries overlap; ownership through production use is the defining feature here.
- State A, State B, the four discovery questions, and the promotion rule.
- **Authority boundaries.** The things a CAST engineer never decides alone: commercial commitments, scope changes, production access, data-use exceptions, compliance interpretations, promotion, and long-lived architecture that the client will inherit.
- The escalation path, with actual names and response expectations attached.

Output: each participant writes and says aloud a short explanation of a discovery build to a hypothetical client. It must name the question, the evidence sought, and what is intentionally absent. If it sounds like a disclaimer or a sales pitch, it has failed.

---

## Module 1: Customer and operational literacy
**Weeks 1–2**

The goal is to make engineers capable of understanding a client's operation without prematurely translating everything into software.

### 1.1 Observation before solutioning

- Follow the work from trigger to outcome, including handoffs, exceptions, and rework.
- Ask for a recent real example instead of a generalized description.
- Separate the documented process from the process people actually use.
- Notice spreadsheets, side channels, duplicated entry, waiting, and approvals. These are usually where the real system boundary lives.
- Do not live-design while a user is still explaining. Capture first; synthesize second.

### 1.2 Stakeholders, users, and decision rights

- Sponsor, buyer, operator, administrator, security owner, data owner, and approver are different roles even when one person holds several.
- Build a stakeholder map that records incentives, risks, authority, and required involvement.
- Distinguish enthusiasm from authority. The loudest supporter may not be able to approve access, rollout, or process change.
- Identify who experiences the problem and who bears the cost of changing it.

### 1.3 Symptom, problem, and outcome

- Convert a request into a problem statement without losing the client's language.
- Establish a baseline: frequency, delay, error rate, effort, financial cost, or risk exposure.
- Define an outcome measure before choosing a feature.
- Write assumptions as assumptions, not as facts hidden inside a solution proposal.

### 1.4 Product framing and opportunity selection

- Distinguish the operator, end user, customer, sponsor, buyer, and beneficiary. They may be different people with different definitions of value.
- Describe the job the person is trying to complete, the constraint that makes it difficult, and the consequence of leaving it unchanged.
- Consider process or policy change, configuration, an existing product, integration, and doing nothing alongside a custom build.
- Write a product hypothesis: the user, the problem, the proposed intervention, the expected behavior or outcome change, and the evidence that would confirm or disprove it.
- Separate an outcome metric from a feature-completion metric. A shipped workflow is not proof that the operation improved.
- Identify adoption conditions: what the user must trust, stop doing, learn, or receive from another team for the change to work.

### 1.5 Clarification and current user flow

- Identify questions that can change scope, value, safety, adoption, or cost.
- Ask about recent behavior before you ask about preferences.
- Ask one clear question at a time.
- Record the answer, its source, and the decision that it affects.
- Map the main user flow from trigger to outcome.
- Add alternate paths, exceptions, waits, handoffs, and manual work.
- Ask operators to correct the map.

### 1.6 Explaining systems without hiding behind jargon

- Start with what the system enables, then explain mechanism only as far as the audience needs.
- Translate tradeoffs into consequences: time, reliability, access, cost, reversibility, and ownership.
- Draw the system as people, actions, systems, data, and boundaries before drawing services and queues.
- Say "I don't know yet" with a concrete plan to find out.

### 1.7 Client-room mechanics

- Set an agenda around a decision, not a tour of topics.
- Ask one question at a time and allow silence.
- Close every session with decisions, open questions, owners, and dates.
- Send a concise written playback while disagreements are still cheap.

**Module assessment:** observe a real or simulated workflow. Produce a one-page user-flow map, stakeholder map, product framing, and product hypothesis. List the important unknowns and alternatives to building. Ask clarification questions. Then play back the problem, desired outcome, and proposed next decision to the people involved. The assessment passes only if operators confirm the main flow and correct at least one specific detail.

---

## Module 2: From ambiguity to a product decision
**Weeks 2–3**

Engineers are rewarded for converging. Client discovery requires them to stay open long enough to avoid the wrong solution. This module gives a clear path from evidence to a product decision and a narrow build.

> **Insert the AI Excellence Playbook here.** It governs use of coding agents, client data, review, and verification. Tool-specific habits sit beneath it.

### 2.1 The engagement brief

Before code, write one page covering:

- the current workflow and the people affected;
- the problem, its evidence, and the baseline;
- the outcome and how it will be observed;
- why this problem is worth acting on now;
- the product hypothesis and alternatives considered;
- the decision this piece of work should enable;
- the named State A question or State B outcome;
- scope, non-goals, dependencies, and authority boundaries;
- data classification and approved environments;
- open assumptions and who can resolve them.

The brief is the smallest shared contract that keeps technical speed attached to client value.

### 2.2 The target user flow

- Start with the current user flow from Module 1.
- Define the user, trigger, actions, decisions, exceptions, and outcome for the proposed change.
- Show what changes and what stays the same.
- Include human review, manual work, and fallback steps.
- Mark assumptions and open questions.
- Review the flow with the operators who do the work.

### 2.3 User stories and acceptance conditions

- Write each story for one user and one operational outcome.
- Use this form: "As a [user], I need to [action] when [condition], so that I can [outcome]."
- Define the starting condition, user action, expected result, and failure result.
- Include common exceptions and unsafe outcomes.
- State non-goals. A non-goal is work that the team will not do in this slice.
- Remove stories that do not support the target outcome.

### 2.4 Clarification and alignment check

- Find vague terms, missing owners, hidden assumptions, and conflicting statements.
- Ask only questions that can change the product or its validation.
- Compare the brief, user flow, stories, acceptance conditions, and success measure.
- Correct gaps before technical planning starts.
- Ask the user, process owner, and technical owner to review the parts that they own.

### 2.5 Product priority

- Rank work by user value, risk, uncertainty, safety, adoption, dependencies, and effort.
- Compare build, buy, configure, process change, and do-nothing options before treating implementation as the default.
- Consider reach or frequency, confidence in the evidence, reversibility, and the ongoing cost of ownership; do not hide judgment inside an unexplained score.
- Put the smallest useful end-to-end story first.
- Do not put infrastructure first unless it blocks the useful story.
- Record why work is first, later, or out of scope.
- State what evidence can change the order.

### 2.6 Product decision and measurement

- State the decision in one sentence: who decides, which options are being considered, and by when.
- Define one outcome measure, one or two behavior or adoption measures, and guardrails for safety, quality, cost, or workload.
- Make the baseline, target, observation window, data source, and owner explicit.
- Distinguish leading signals that tell you whether people are trying the change from lagging signals that show whether the operation improved.
- Include the status-quo option. A product decision is sometimes to stop, defer, simplify, or change the process rather than build.

### 2.7 Technical reconnaissance

- Map systems, owners, interfaces, data stores, environments, and release paths.
- Test access and assumptions early. "The API exists" is not evidence that the required data, permission, latency, or support agreement exists.
- Trace one real record end to end, using approved and redacted data.
- Identify rate limits, data quality, residency, retention, audit, identity, and human-approval constraints.
- Record unknowns. Do not turn missing information into optimistic architecture.

### 2.8 Choosing the thinnest useful slice

- Select one operational path, one user group, and one measurable outcome.
- Preserve the risky part; fake the plumbing around it, because a build that mocks the central uncertainty cannot change the decision.
- Prefer manual operations behind a clean boundary when they buy learning safely.
- State what will not be learned from the slice.

### 2.9 Designing with the client, not for them

- Bring operators and the client's technical team into decisions that affect their work.
- Use prototypes and diagrams as questions, not as presentations to approve.
- Surface constraints while choices are reversible.
- Treat client conventions as part of the requirement, since a solution the client cannot own or maintain fails regardless of its technical quality.

### 2.10 AI-assisted delivery

- Give coding agents the engagement brief, repository rules, and the smallest relevant context.
- Use agents for reconnaissance and options, but verify every claim against the code, environment, or an owner.
- Separate scaffolding from constrained changes.
- Review diffs before running generated code and before showing any output.
- Never put client credentials, production data, or restricted material into an unapproved tool.
- Stop when the tool crosses a boundary you did not intend; moving quickly does not make unauthorized access acceptable.

Before implementation, compare the proposed tasks with the brief, product hypothesis, user stories, and measurement plan. Remove tasks that do not support an accepted story or a necessary learning goal. Add missing work for acceptance, exceptions, adoption, and measurement.

**Module assessment:** use a messy client request and a representative system. Produce an engagement brief, product hypothesis, alternatives table, validated user flow, prioritized user stories, acceptance conditions, measurement plan, technical reconnaissance map, and thin-slice plan. Explain why the first story and intervention are first. Explain which requests you excluded. Defend what the slice proves, what it cannot prove, and which evidence will stop or change the work.

---

## Module 3: Evidence, verification, and production safety
**Weeks 3–4. This is the most important module in the program.**

The core risk is that a technically working system can still be wrong for the operation, unsafe in the environment, or impossible for the client to own.

### 3.1 Evidence in State A

- Define the observation that would change the decision before building.
- Test with the people who perform the work, not only the sponsor.
- Test the product hypothesis: can the intended user complete the job, will they choose the new path, and does the change create enough value to justify ownership?
- Use representative edge cases and record where sample data limits the conclusion.
- Keep an evidence log: claim, observation, source, confidence, and implication.
- Catalog every fiction as it is introduced.

**Assessment:** another participant tries to invalidate the discovery claim. Passing means the claim becomes narrower and more accurate, not that it survives unchanged.

### 3.2 Production safety in State B

- Threat modeling, privacy review, access control, auditability, and data lifecycle.
- Failure modes, retries, idempotency, graceful degradation, and manual fallback.
- Observability tied to the user's outcome, adoption, and guardrails, not only infrastructure health.
- A feedback loop that gives the process owner evidence to stop, adjust, expand, or transfer the capability.
- Migration, rollback, feature flags, support ownership, and runbooks.
- Performance, cost limits, and realistic load.
- Client release processes and change controls take precedence over personal preference.

**Assessment:** ship a representative change through a production-like release. Provide test evidence, a threat and failure-mode review, an observability view, a rollback exercise, and an operator-ready runbook.

---

## Module 4: The client conversation
**Weeks 4–5**

This module builds the client instincts that product teams often distribute across product management, design, sales, and customer success.

- **Question before answer.** Respond to a feature request by establishing the event, person, current workaround, and desired change.
- **Precision without jargon.** Explain architecture and tradeoffs in the client's terms without making the explanation false.
- **Managing disagreement.** Name the consequence, show the evidence, and make the decision owner visible. Do not win the technical argument and lose the engagement.
- **No accidental commitments.** Estimates, pricing, scope changes, compliance positions, and guarantees go through their owners.
- **Showing State A.** Frame the question and invite a specific test. Never let polish silently imply readiness.
- **Showing State B.** Demonstrate the operational path, failure behavior, monitoring, and ownership, not only the happy path.
- **Reading the room.** Notice absent decision-makers, unspoken risk, threatened teams, and polite agreement without commitment.

**Assessment:** lead a simulated client session in which the stated request is not the real problem, stakeholders disagree, and the sponsor asks for an immediate commitment. Scored on discovery, clarity, boundary-holding, and the written playback.

---

## Module 5: Adoption, handoff, and promotion
**Weeks 5–6**

Deployment is a technical event; adoption and ownership are the actual outcome.

### 5.1 Handing off a discovery build

Required deliverables:

1. **The evidence log.** What was learned, from whom, and how strong the evidence is.
2. **The faked list.** Everything fictional or manually operated, plus what a real version requires.
3. **The decision log.** Choices, assumptions, constraints, and deliberate deferrals.
4. **The open questions.** What remains unresolved and why it matters.
5. **The product case.** The user, outcome, alternatives considered, adoption conditions, and ongoing ownership implication.
6. **The recommendation.** Stop, test again, build a different slice, or propose promotion.

### 5.2 Handing off production work

- Name the service owner, support owner, data owner, and business owner.
- Document decisions and operating procedures, not a tour of code the repository already contains.
- Train the people who administer and support the system.
- Name an adoption owner and agree how usage, outcome movement, exceptions, and user feedback will be reviewed.
- Prove monitoring, alert routing, rollback, recovery, and manual fallback.
- Close access that was granted for the engagement and return or remove client data according to policy.
- Hold an explicit end-of-engagement review: outcome, remaining risks, debt, ownership, and next decision.

### 5.3 Running a promotion

1. The promotion decision is recorded with a named owner.
2. The evidence is strong enough for the investment being proposed.
3. The faked list becomes the hardening work list.
4. Security, data, compliance, operational, UX, and adoption gaps are included.
5. Delivery and ongoing ownership are scoped before work starts.
6. The outcome measures, guardrails, review cadence, and stop or rollback conditions are agreed.
7. The artifact is relabeled State B and follows the client's production controls.

**Assessment:** run a promotion review. Passing requires making the real work visible, including the option not to promote.

---

## Module 6: Capstone
**Weeks 6–8**

A real engagement, narrowly scoped and supervised. The participant owns discovery, technical reconnaissance, delivery, and playback. A senior owns the commercial relationship and remains accountable for boundaries. The client must supply access to real operators and a technical owner.

Deliverables:

- engagement brief and stakeholder map;
- current-state workflow and technical reconnaissance map;
- the build, explicitly labeled State A or State B;
- verification and evidence record;
- decision log, faked list, and open questions;
- adoption or handoff plan;
- recorded client playback and written next decision.

The debrief starts with the client outcome, not the architecture. What changed for the people doing the work? What evidence supports that? What will happen after the engineer leaves?

---

## Levels after the program

Graduation is not permission to run a client engagement alone. The levels gate the combination of client authority, system risk, and ambiguity a person is trusted to hold.

| Level | Client responsibility | Trusted with | Can decide |
|---|---|---|---|
| **Shadow** | Observes and owns bounded follow-up | State A tasks, paired | Technical implementation inside an agreed plan |
| **Supported** | Leads discovery and delivery with a senior present at decision points | State A end to end; State B within an approved design and release path | Reversible technical choices inside scope |
| **Embedded** | Runs the day-to-day engagement | State A and State B within agreed outcomes and controls | Delivery choices inside scope; escalates the never-alone list |
| **Lead** | Owns engagement shape and coaches others | Multi-workstream or high-risk delivery | Recommends scope, promotion, and architecture; formal owners still approve |

Nobody advances on time served or code volume. Movement requires evidence of three things:

1. they changed direction when client evidence contradicted their technical preference;
2. they escalated something they could have quietly handled alone; and
3. they left a system and relationship operable without them.

The Supported → Embedded gate is primarily about judgment under ambiguity. Technical strength is a prerequisite for reaching it, but it is not what separates people who advance.

---

## What the organization has to supply

The program fails without these, and none are the cohort's responsibility.

- Real operators with protected time; validating with the sponsor alone does not substitute for access to the people doing the work.
- A senior CAST engineer with allocated mentoring time.
- A senior client lead who owns scope, pricing, and relationship escalation.
- Access to design, security, data, and compliance partners at defined gates.
- An approved discovery environment and representative, appropriately handled data.
- Versioned templates for the engagement brief, evidence log, faked list, decision log, and production readiness review.
- A safe first engagement: narrow scope, cooperative client, reversible change, and no critical-path launch.
- A policy for support and ownership after the CAST engineer leaves.
- A commercial answer for discovery that creates unplanned production demand.

---

## Risks worth watching

**The solution reflex.** Engineers convert a client's first sentence into architecture before understanding the operation. Reward high-quality disconfirmation, not only fast output.

**The hero loop.** The engineer becomes the only person who understands the solution and is rewarded for repeatedly rescuing it. This looks like client value until they leave. Measure transferred ownership.

**Technical truth mistaken for the whole truth.** A correct statement about a system can still ignore incentives, workflow, policy, or adoption. Require operator evidence alongside technical evidence.

**The friendly scope change.** Direct access makes small requests feel harmless. If the requested outcome, data use, or ongoing obligation changed, the scope changed.

**Discovery theater.** Interviews are held, notes are written, and the team builds the original idea anyway. Every brief should show what the evidence changed.

**Sponsor-only validation.** The buyer approves something operators cannot or will not use. No production recommendation without evidence from the people in the workflow.

**Prototype laundering.** Good engineering hygiene makes State A code look safer than it is. Clean code does not replace threat modeling, support ownership, data controls, rollout, or adoption work.

**Permanent embed.** The client routes every hard problem to the CAST engineer. The role succeeds when client capability increases, not when dependence increases.
