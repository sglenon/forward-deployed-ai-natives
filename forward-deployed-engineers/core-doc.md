# Forward-Deployed Engineering
### A training program for converting strong product engineers into engineers who can discover, deliver, and own outcomes inside a client's environment

---

## Assumptions in this draft

Change these and the structure still holds, but the pacing will shift.

- **Cohort:** 4–6 engineers, run together rather than individually.
- **Duration:** 8 weeks, roughly 6–8 hours per week, alongside existing delivery work.
- **Support:** each cohort has one senior forward-deployed engineer (technical and engagement judgment), one senior client lead (commercial and relationship questions), and access to a designer or product partner for workflow and usability review. Mentors are not full-time on this.
- **Prerequisites:** able to ship production software independently, comfortable reading an unfamiliar codebase, and willing to spend as much time with users as with code. This is not an entry-level engineering course.
- **Tooling:** participants use the client's approved stack and AI tooling. Claude Code, Codex, or another coding agent can accelerate delivery, but no particular tool is the point of the program.
- **Existing assets:** an engagement brief template, a discovery-build starter, security and data-handling rules, a decision-log template, and the AI Excellence Playbook. If these do not exist, building them is Week 0 and belongs to program leadership, not the cohort.

---

## The thesis of the program

A product engineer is usually given a problem that has already been translated: a ticket, a design, an acceptance criterion, a system boundary. A forward-deployed engineer works before that translation is complete. They sit close enough to the client's operation to see where the stated request is wrong, incomplete, or aimed at a symptom, then stay responsible long enough to put a durable change into use.

The program is not about making engineers more charismatic. It is about teaching a repeatable form of technical judgment under client pressure: observe before proposing, turn ambiguity into testable claims, ship the thinnest useful thing, and leave the client's system stronger than you found it.

Forward-deployed means the work ships. If involvement stops at advice, discovery, or a demo, this is consulting or prototyping with a different title. The governing idea is therefore the same one that anchors the forward-deployed designer program:

> **Everything you build is in one of two states, and you always know which one. Moving between them is a decision someone signs off on, never something that just happens.**

### State A: Discovery build

Purpose: reduce a named uncertainty. Lifespan: days. Fictions are deliberate: sample data, a stubbed integration, or a manual step may be correct craft. The bar is *enough evidence to decide*. Success is a better decision, including deciding not to build.

The four questions a State A build is allowed to answer:

1. Are we solving the right operational problem?
2. Will the people in the workflow use this shape of solution?
3. Can the client's real data and systems support it?
4. Is the value large enough to justify production work?

### State B: Production work

Purpose: create an outcome people can depend on. Lifespan: indefinite. Fictions are defects. The bar is *secure, observable, maintainable, adopted, and operable by someone other than you*. Success is not merely deployment. It is that the intended users can use it, the client can run it, and the agreed outcome moves without unacceptable regressions.

This covers changes to a client's live system and any discovery build that has been formally promoted.

### Promotion: the only legal transition

A discovery build becoming production work is often the right outcome. It happens exactly one way: a named decision owner approves it, the fictions and unresolved risks are written down, and a hardening and adoption pass is scoped as real work with real cost.

The alternative is **drift**. Drift is particularly dangerous for engineers because the artifact can look technically credible long before it is operationally safe.

---

## Module 0: The role and its edges
**Half day. Complete before joining a client session.**

Content:

- Why the role exists: the failure is usually translation between a general capability and a specific operation, not a shortage of features.
- The distinction between product engineering, solutions engineering, consulting, and forward-deployed engineering. The boundaries overlap; ownership through production use is the defining feature here.
- State A, State B, the four discovery questions, and the promotion rule.
- **Authority boundaries.** The things a forward-deployed engineer never decides alone: commercial commitments, scope changes, production access, data-use exceptions, compliance interpretations, promotion, and long-lived architecture that the client will inherit.
- The escalation path, with actual names and response expectations attached.

Output: each participant writes and says aloud a short explanation of a discovery build to a hypothetical client. It must name the question, the evidence sought, and what is intentionally absent. If it sounds like a disclaimer or a sales pitch, it has failed.

---

## Module 1: Customer and operational literacy
**Weeks 1–2**

The goal is not to turn engineers into account managers. It is to make them capable of understanding a client's operation without prematurely translating everything into software.

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

### 1.4 Explaining systems without hiding behind jargon

- Start with what the system enables, then explain mechanism only as far as the audience needs.
- Translate tradeoffs into consequences: time, reliability, access, cost, reversibility, and ownership.
- Draw the system as people, actions, systems, data, and boundaries before drawing services and queues.
- Say "I don't know yet" with a concrete plan to find out.

### 1.5 Client-room mechanics

- Set an agenda around a decision, not a tour of topics.
- Ask one question at a time and allow silence.
- Close every session with decisions, open questions, owners, and dates.
- Send a concise written playback while disagreements are still cheap.

**Module assessment:** observe a real or simulated workflow, produce a one-page workflow map and stakeholder map, then play back the problem and desired outcome to the people involved. The assessment passes only if the operators say, "Yes, that is how it actually works."

---

## Module 2: From ambiguity to a buildable intervention
**Weeks 2–3**

Engineers are rewarded for converging. Client discovery requires staying open long enough to avoid converging on the wrong thing. This module provides the bridge: a disciplined path from messy evidence to a narrow build.

> **Insert the AI Excellence Playbook here.** It governs use of coding agents, client data, review, and verification. Tool-specific habits sit beneath it.

### 2.1 The engagement brief

Before code, write one page covering:

- the current workflow and the people affected;
- the problem, its evidence, and the baseline;
- the outcome and how it will be observed;
- the decision this piece of work should enable;
- the named State A question or State B outcome;
- scope, non-goals, dependencies, and authority boundaries;
- data classification and approved environments;
- open assumptions and who can resolve them.

The brief is not a specification. It is the smallest shared contract that keeps technical speed attached to client value.

### 2.2 Technical reconnaissance

- Map systems, owners, interfaces, data stores, environments, and release paths.
- Test access and assumptions early. "The API exists" is not evidence that the required data, permission, latency, or support agreement exists.
- Trace one real record end to end, using approved and redacted data.
- Identify rate limits, data quality, residency, retention, audit, identity, and human-approval constraints.
- Record unknowns. Do not turn missing information into optimistic architecture.

### 2.3 Choosing the thinnest useful slice

- Select one operational path, one user group, and one measurable outcome.
- Preserve the risky part; fake the plumbing around it. A discovery build that mocks the central uncertainty proves nothing.
- Prefer manual operations behind a clean boundary when they buy learning safely.
- State what will not be learned from the slice.

### 2.4 Designing with the client, not for them

- Bring operators and the client's technical team into decisions that affect their work.
- Use prototypes and diagrams as questions, not as presentations to approve.
- Surface constraints while choices are reversible.
- Treat client conventions as part of the requirement. A technically elegant solution the client cannot own is not elegant.

### 2.5 AI-assisted delivery

- Give coding agents the engagement brief, repository rules, and the smallest relevant context.
- Use agents for reconnaissance and options, but verify every claim against the code, environment, or an owner.
- Separate scaffolding from constrained changes.
- Review diffs before running generated code and before showing any output.
- Never put client credentials, production data, or restricted material into an unapproved tool.
- Stop when the tool crosses a boundary you did not intend; speed is not authorization.

**Module assessment:** given a messy client request and access to a representative system, produce an engagement brief, a stakeholder-validated workflow map, a technical reconnaissance map, and a thin-slice plan. Defend what the slice proves, what it cannot prove, and which assumptions would stop the work.

---

## Module 3: Evidence, verification, and production safety
**Weeks 3–4. This is the most important module in the program.**

The core risk is not that an engineer cannot make something work. It is that a technically working system can still be wrong for the operation, unsafe in the environment, or impossible for the client to own.

### 3.1 Evidence in State A

- Define the observation that would change the decision before building.
- Test with the people who perform the work, not only the sponsor.
- Use representative edge cases and record where sample data limits the conclusion.
- Keep an evidence log: claim, observation, source, confidence, and implication.
- Catalog every fiction as it is introduced.

**Assessment:** another participant tries to invalidate the discovery claim. Passing means the claim becomes narrower and more accurate, not that it survives unchanged.

### 3.2 Production safety in State B

- Threat modeling, privacy review, access control, auditability, and data lifecycle.
- Failure modes, retries, idempotency, graceful degradation, and manual fallback.
- Observability tied to the user's outcome, not only infrastructure health.
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

A deployment is a technical event. Adoption and ownership are the outcome.

### 5.1 Handing off a discovery build

Required deliverables:

1. **The evidence log.** What was learned, from whom, and how strong the evidence is.
2. **The faked list.** Everything fictional or manually operated, plus what a real version requires.
3. **The decision log.** Choices, assumptions, constraints, and deliberate deferrals.
4. **The open questions.** What remains unresolved and why it matters.
5. **The recommendation.** Stop, test again, build a different slice, or propose promotion.

### 5.2 Handing off production work

- Name the service owner, support owner, data owner, and business owner.
- Document decisions and operating procedures, not a tour of code the repository already contains.
- Train the people who administer and support the system.
- Prove monitoring, alert routing, rollback, recovery, and manual fallback.
- Close access that was granted for the engagement and return or remove client data according to policy.
- Hold an explicit end-of-engagement review: outcome, remaining risks, debt, ownership, and next decision.

### 5.3 Running a promotion

1. The promotion decision is recorded with a named owner.
2. The evidence is strong enough for the investment being proposed.
3. The faked list becomes the hardening work list.
4. Security, data, compliance, operational, UX, and adoption gaps are included.
5. Delivery and ongoing ownership are scoped before work starts.
6. The artifact is relabeled State B and follows the client's production controls.

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

**The Supported → Embedded gate is judgment under ambiguity.** Technical strength is a prerequisite, not the differentiator.

---

## What the organization has to supply

The program fails without these, and none are the cohort's responsibility.

- Real operators with protected time. Sponsor-only discovery is not discovery.
- A senior forward-deployed engineer with allocated mentoring time.
- A senior client lead who owns scope, pricing, and relationship escalation.
- Access to design, security, data, and compliance partners at defined gates.
- An approved discovery environment and representative, appropriately handled data.
- Versioned templates for the engagement brief, evidence log, faked list, decision log, and production readiness review.
- A safe first engagement: narrow scope, cooperative client, reversible change, and no critical-path launch.
- A policy for support and ownership after the forward-deployed engineer leaves.
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

**Permanent embed.** The client routes every hard problem to the forward-deployed engineer. The role succeeds when client capability increases, not when dependence increases.
