# Workshop Assessment Bank: Practiced Conversations and UI/UX Literacy

This is the standalone assessment bank for the half-day workshop "Practiced Conversations and UI/UX Literacy" (Section 7 of `curriculum_modules-full.md`), which sits between Module 2 and Module 3. It covers Half A (four conversation drills) and Half B (five UI/UX recognition-literacy topics). Questions are written in structured Markdown Q&A format by explicit request, so a human can read and grade them today and hand-port them into whatever LMS quiz/test-builder tool the organization adopts later. Every question carries an answer key or rubric; every topic carries a one-line pass-bar note consistent with how the rest of the curriculum grades (for example, Module 1's playback pass condition: operators confirm the flow and then correct a specific detail).

---

## Half A: Drill 1 — The Holding Phrase

**Learning objective:** Give a technically useful answer to a price, timeline, or feasibility question without making a commitment, using a version of the Module 0.4 holding phrase.

### Q1 (multiple choice — scenario/judgment)

During a discovery session, the claims operations manager asks: "So realistically, when can this extraction tool be live for the whole team? Can we say end of quarter?"

What should you say?

- **A.** "End of quarter should be doable if nothing unexpected comes up in your environment."
- **B.** "I can't discuss timelines. You'd have to talk to someone else about that."
- **C.** "I can tell you what the evidence says so far: the model handled six of eight sample layouts, and two layouts still fail. Before that becomes a delivery date, I need to bring in the person who owns delivery commitments."
- **D.** "It's hard to say. There are a lot of variables. We'll see how it goes."

**Answer key:** **C.**

- **C is correct:** it follows the holding-phrase pattern — a genuinely useful technical answer (what the evidence shows) plus an explicit boundary that routes the commitment to its owner. It is helpful and non-committal at the same time.
- **A is wrong:** an accidental commitment. "Should be doable" plus a hedge will be heard as "end of quarter, yes." Timeline belongs to the never-alone list.
- **B is wrong:** a pure refusal. The drill explicitly fails if the answer is only a refusal; it gives the client nothing technically useful and damages the relationship.
- **D is wrong:** evasive. It avoids commitment but also avoids being useful, and it makes no boundary or owner visible.

### Q2 (open response — production)

Write your own holding-phrase response, in one to three sentences, for this scenario: a client sponsor asks, "Your prototype already reads our PDFs — surely the production version is basically free at this point?"

**Model answer:** "I can tell you what the prototype shows: on the approved sample, the six fields are proposed correctly often enough that analyst review looks faster than manual entry, but the queue, identity, and downstream write are all simulated. Turning that into a production cost or scope answer is a separate decision, and I'd want to involve [senior client lead / the delivery owner] before we treat it as one."

**Grading criteria (mentor checks all three):**

1. Contains a real, specific technical statement (evidence, current state, or a known limitation) — not just a deflection.
2. Explicitly declines to convert that into a price/scope/feasibility commitment, and names or points to the decision owner.
3. Does not sound like either a refusal ("I can't talk about that") or a promise ("basically yes, pending sign-off").

**Difficulty / pass-bar note:** Pass = a response that is simultaneously useful and non-committal, mirroring the drill's own fail conditions; fail = a bare refusal, an evasive non-answer, or any sentence a client could quote back as a number, date, or guarantee.

---

## Half A: Drill 2 — One Question, Then Silence

**Learning objective:** Ask one behavior-focused discovery question (Section 1.7 style) and hold silence afterward, without answering your own question or offering architecture options.

### Q1 (multiple choice — scenario/judgment)

You are interviewing an operations analyst about case intake. Which is the correct move, per the drill?

- **A.** "Would an automated summary help you? Or maybe a dashboard? We could also do email alerts — which sounds best?"
- **B.** "Show me the last case where intake went wrong. What did you have to do to fix it?" — then wait, even if the pause feels long.
- **C.** "How often does intake go wrong? Probably not that often, right? I imagine it's mostly the PDF layouts."
- **D.** "What features do you need in the new intake screen?"

**Answer key:** **B.**

- **B is correct:** one question, grounded in observed behavior (a specific recent case, per 1.7's "prefer behavior over preference"), followed by silence.
- **A is wrong:** it is a multiple-choice architecture menu — the exact fail condition of the drill. The questioner is answering their own question with solution options.
- **C is wrong:** the questioner fills the silence and supplies the answer ("probably not that often... I imagine it's the PDFs"), which teaches the analyst to confirm rather than inform.
- **D is wrong:** a preference/feature question, not a behavior question; it collects opinions instead of making a decision easier.

### Q2 (open response — production)

An analyst says: "The reconciliation step is usually fine." Write the single follow-up question you would ask before going silent, and state which decision the answer could change.

**Model answer:** Question: "Usually — can you walk me through the last case where it was not fine? What happened and what did you do?" Decision affected: whether the exception path needs to be part of the target user flow and acceptance conditions, or whether it is rare enough to stay a manual step in State A.

**Grading criteria:**

1. Exactly one question, targeting the vague word ("usually") with a request for a concrete recent case, not a preference or frequency guess.
2. No embedded answer, no architecture options, no second question stacked on.
3. Names a real decision the answer could change (scope, priority, user flow, safety control, acceptance condition, or stop condition — per 1.7).

**Difficulty / pass-bar note:** Pass = one behavior-anchored question plus a stated decision it informs; fail = stacked questions, a preference question, or any self-supplied answer that fills the silence.

---

## Half A: Drill 3 — Name the Disagreement, Then Show Options

**Learning objective:** Identify the type of a disagreement (fact, prediction, value, risk tolerance, authority, or language) and respond with two or three legible options, a stated recommendation, and a visible decision owner (per 1.10).

### Q1 (multiple choice — scenario/judgment)

The claims team lead says: "The error rate on the current parser is fine — maybe one case in fifty." Your own eight observed cases showed three with parsing errors. What kind of disagreement is this, and what is the right first move?

- **A.** A value disagreement — argue that accuracy matters more than the team lead thinks.
- **B.** A fact disagreement — propose pulling last month's rework log together, since more data can resolve what is true today.
- **C.** An authority disagreement — escalate to the sponsor to rule on the real error rate.
- **D.** A risk-tolerance disagreement — accept the team lead's number since they own the process.

**Answer key:** **B.**

- **B is correct:** the dispute is about what is true today (the actual error rate), which is a **fact** disagreement, and 1.10 says more logs can resolve a fact dispute. Proposing shared evidence is the correct first move.
- **A is wrong:** misdiagnoses the type. Nobody has disagreed about which outcome matters; they disagree about a number.
- **C is wrong:** escalation is for authority disputes (who has the right to decide). A measurable fact does not need a ruling; it needs measurement.
- **D is wrong:** conceding a fact question as if it were a tolerance question hides the real error rate from the decision it affects.

### Q2 (open response — production)

The client's IT lead wants the extraction tool to write directly into the case system; the operations manager wants analysts to review every proposed field first. Write the response you would give in the room. It must: name the disagreement type, lay out two or three options in legible form (outcome, cost/risk, reversibility, owner), state your recommendation, and name who decides.

**Model answer (shape, not exact wording):** "This sounds like a risk-tolerance disagreement — how much downside from a wrong automated write is acceptable. Option 1: direct write — fastest for analysts, but a critical-field error creates a wrong case action and is hard to reverse; needs the process owner to accept that risk. Option 2: review-first — slower per case, fully reversible, no new failure mode; costs analyst time. Option 3: review-first for the two unrecognized layouts only, direct write for proven layouts — middle cost, bounded risk. My recommendation is Option 2 for State A, because we are still measuring error rates. The decision owner is the operations process owner, with the IT lead on the integration path."

**Grading criteria:**

1. Names a plausible disagreement type from the 1.10 list and it fits the scenario (risk tolerance, or defensibly value/authority — with reasoning).
2. Presents 2–3 options with at least outcome, risk, and reversibility visible for each — not a hidden single option.
3. States a recommendation *and* names the decision owner; does not argue the point without surfacing who decides.

**Difficulty / pass-bar note:** Pass = type named, options legible, recommendation and owner both visible; fail = skipping the type, arguing a position without options, or leaving the decision owner implicit (the drill's own fail conditions).

---

## Half A: Drill 4 — Say "I Do Not Know" Completely

**Learning objective:** Answer a question you cannot fully answer by stating what is unknown, identifying the source that can resolve it, and naming the next action — without vagueness or evasion.

### Q1 (multiple choice — scenario/judgment)

A compliance stakeholder asks: "Does the source system retain the audit field long enough for our seven-year requirement?" You do not know. What should you say?

- **A.** "I'm not sure, but it's probably fine — most systems keep audit data for years."
- **B.** "That's really a question for compliance, not for me."
- **C.** "I don't know whether the source retains that field for seven years. I'll check the schema and the retention policy with the data owner this week; the answer decides whether we can rely on the source or must record the value ourselves."
- **D.** "I'd have to look into it."

**Answer key:** **C.**

- **C is correct:** it is the complete "I do not know" from 1.10 — the unknown is stated precisely, the resolving source is named (schema + retention policy via the data owner), and the next action and its consequence for the design are explicit.
- **A is wrong:** a guess dressed as reassurance. "Probably fine" on a retention question is an accidental compliance position — never-alone territory.
- **B is wrong:** evasive hand-off. It names no unknown, no source, and no next action, and it discards a question the engineer is well placed to help resolve.
- **D is wrong:** vague. It admits ignorance but commits to nothing checkable — no source, no owner, no timeframe, no stated consequence.

### Q2 (open response — production)

An operations analyst asks: "If two analysts open the same case at once, will your tool overwrite one of them?" You have not tested concurrent edits. Write your complete "I do not know" answer.

**Model answer:** "I don't know — we haven't tested two analysts editing the same case at once in this build. I'll check how the case system handles concurrent edits with your technical owner and run a two-user test on the sample environment this week. The answer determines whether we need a lock or a conflict warning before anyone relies on the tool for shared cases."

**Grading criteria:**

1. States the specific unknown (not a general "not sure").
2. Names a concrete resolving source or method (a person, an artifact, or a test) and a next action with an implied or explicit owner/timeframe.
3. States what the answer will decide — connecting the unknown to a design or scope consequence.

**Difficulty / pass-bar note:** Pass = all three parts present (unknown, source, next action) plus the decision the answer affects; fail = a guess, a bare "I'll look into it," or a deflection to someone else with no follow-through named.

---

## Half B: Topic 1 — Visual Hierarchy and Core Usability Heuristics

**Learning objective:** Recognize which of the five taught usability heuristics a screen violates, and name the user harm in operational terms.

### Q1 (multiple choice — scenario/judgment)

A claims analyst submits a batch of cases for reprocessing. The screen shows no change for about 20 seconds, then silently returns to the case list. Analysts have started clicking "Reprocess" two or three times "to make sure it took." Which heuristic is being violated?

- **A.** Match to real-world language
- **B.** Recognition over recall
- **C.** Visibility of system status
- **D.** Error prevention

**Answer key:** **C.**

- **C is correct:** the user cannot tell whether work is loading, processing, failed, or complete — the definition of a status-visibility failure. The repeated clicking is the operational harm it causes (duplicate reprocessing).
- **A is wrong:** no internal jargon is involved; the words are not the problem, the silence is.
- **B is wrong:** nothing forces the user to remember information from another screen.
- **D is wrong:** error prevention is about making wrong actions difficult; the double-click here is a *symptom* of missing status, not of an unguarded destructive control. (A secondary prevention fix could help, but the root heuristic is status.)

### Q2 (open response — identification + fix)

Screen description: an exceptions queue shows every row with the label "Entity resolution failure — code ERF-114." Analysts keep a printed cheat sheet taped to their monitors translating codes into what actually went wrong. Identify the heuristic being violated, describe the operational harm, and propose the fix in one or two sentences.

**Model answer:** Violated heuristic: match to real-world language (with a secondary recognition-over-recall burden — the cheat sheet exists because the screen forces recall of code meanings). Harm: analysts translate before they can act, which slows triage and produces mis-sorted exceptions when the cheat sheet is stale. Fix: label rows in analyst vocabulary — e.g., "Unmatched record: claimant name differs from policy record" — and keep the internal code as secondary detail.

**Grading criteria:**

1. Names match-to-real-world-language (credit recognition-over-recall as a defensible secondary; primary must be language).
2. Describes a concrete operational harm (slower triage, wrong action), not just "it's confusing."
3. Fix replaces internal terms with client vocabulary rather than adding training or a better cheat sheet.

**Difficulty / pass-bar note:** Pass = correct heuristic plus a harm stated as user/operation impact; fail = naming only "bad UX" without a heuristic, or a fix that works around the violation (documentation, training) instead of removing it.

---

## Half B: Topic 2 — Form and Error-State Conventions

**Learning objective:** Spot violations of the workshop's form and error-state conventions and explain why each is an operational-error risk, not a style preference.

### Q1 (multiple choice — scenario/judgment)

A case-entry form uses placeholder text inside each field as its only label, accepts any text in the date-of-loss field, and — on submit — shows a single banner at the top: "3 errors found." Which critique correctly uses the workshop's conventions?

- **A.** "The visual style feels dated; a cleaner font and more color would help analysts."
- **B.** "Labels vanish once analysts start typing, invalid dates get through until submit, and the errors aren't next to the fields that caused them — so analysts hunt for what to fix, and bad dates reach the case record."
- **C.** "The form should be a single-page wizard with autosave, dark mode, and keyboard shortcuts."
- **D.** "It's fine — analysts use this form daily and have learned where everything is."

**Answer key:** **B.**

- **B is correct:** it names three specific convention violations (labels inside fields, late validation with no specific fix, errors not inline) and ties each to an operational error, exactly the vocabulary the workshop teaches.
- **A is wrong:** treats the problems as style preferences — the section explicitly says these conventions reduce operational errors and are not merely style.
- **C is wrong:** prescribes a redesign wish-list unrelated to the observed violations; it is solution reflex, not critique.
- **D is wrong:** "users have adapted" is the recall burden made permanent; adaptation cost is the harm, not evidence of health.

### Q2 (open response — production)

An "Archive case" button immediately archives with no confirmation, and archived cases leave the analyst's queue with no way back. Separately, a filtered case list sometimes shows a blank white area with no text. Using the form/error-state conventions, write the two flags you would raise, each with the convention violated and the fix.

**Model answer:** Flag 1: destructive action without confirmation — convention: confirm destructive or irreversible actions and describe the consequence. Fix: a confirm step stating "This removes the case from your queue; retrieve it via Archived cases," plus an undo window if archiving is reversible. Flag 2: unexplained empty state — convention: explain why a list is empty and what to do next. Fix: "No cases match this filter — clear filters or check the Unassigned queue."

**Grading criteria:**

1. Both violations identified against the taught convention list (destructive-action confirmation; empty-state explanation).
2. Each fix describes the consequence/next action to the user, not just "add a popup."
3. Harm framed operationally (lost cases from the queue, analysts assuming a data outage) rather than aesthetically.

**Difficulty / pass-bar note:** Pass = both conventions named with fixes a designer could act on; fail = catching only one, or fixes that add friction without conveying consequence or next action.

---

## Half B: Topic 3 — Accessibility Red Flags

**Learning objective:** Spot the four taught accessibility red flags (color-only signals, tiny targets, no keyboard path, poor contrast), name the user harm, and flag them for a designer or specialist — without attempting remediation yourself.

### Q1 (multiple choice — scenario/judgment)

In a review of a peer's prototype, you notice failed validations are indicated only by the field border turning red, with no icon or message. What is the correct action, per the workshop?

- **A.** Rewrite the CSS yourself to add icons and ARIA attributes before the next demo.
- **B.** Ignore it — accessibility compliance is out of scope for engineers in this program.
- **C.** Flag it to the design partner: "Errors are signaled by color only, which some color-blind analysts will not see; they'd submit forms not knowing a field failed. Can we pair the color with an icon and message?"
- **D.** Note it as a P3 style preference to revisit after launch.

**Answer key:** **C.**

- **C is correct:** it is spotting, not remediation — name the risk (color-only signal), the user harm (invisible errors for color-blind users), and route it to the design partner as a question. That is exactly the taught behavior.
- **A is wrong:** deep accessibility remediation is explicitly out of scope; the engineer's job is recognition and flagging, and ARIA authorship belongs to the design/accessibility partner.
- **B is wrong:** confuses "deep compliance work is out of scope" with "spotting is out of scope." Spotting these four flags is exactly in scope.
- **D is wrong:** a color-only error signal is a user-harm risk, not polish; deferring it as style misclassifies the finding.

### Q2 (open response — identification)

Screen description: the exceptions dashboard shows secondary case details in light gray text on a white background; the "Escalate" control is a 20×20-pixel icon with no text; and escalation can only be triggered by mouse click — Tab never reaches it. List every accessibility red flag present, and for one of them describe the user harm in one sentence.

**Model answer:** Three flags: (1) poor contrast — light gray on white, hardest on secondary text; (2) tiny target — 20×20 px is well under the ~44×44-point guidance, error-prone under stress or on mobile; (3) no keyboard path — mouse-only escalation blocks keyboard and assistive-technology users. Example harm (flag 3): an analyst using a keyboard or screen reader cannot escalate a case at all, so urgent exceptions sit unactioned.

**Grading criteria:**

1. All three present flags identified (contrast, tiny target, no keyboard path); no invented fourth issue required.
2. At least one harm described as a concrete blocked or degraded user action, not "not accessible."
3. Response frames the output as something to flag to a designer/specialist, not a remediation plan.

**Difficulty / pass-bar note:** Pass = all present flags caught with at least one operational harm; fail = missing the keyboard-path flag (the most commonly missed), or drifting into remediation detail instead of flagging.

---

## Half B: Topic 4 — Brief and Critique a Design Partner

**Learning objective:** Write a design brief containing the six required elements, and deliver a critique that observes without interpretation, names the heuristic at risk, states the operational harm, and asks a question rather than prescribing a fix.

### Q1 (multiple choice — scenario/judgment)

Which of these is a well-formed critique of a design partner's mock, per the workshop's four-step critique structure?

- **A.** "The save flow is confusing. Move the button to the top right and make it blue — that's the standard."
- **B.** "I noticed the draft is discarded when an analyst navigates away, with no warning. That looks like a user-control-and-freedom risk — an analyst could lose twenty minutes of case notes mid-interview. Is there a save-draft or warning state you're planning here?"
- **C.** "I don't love it. It doesn't feel like something our analysts would use."
- **D.** "This violates Nielsen heuristic #3. Please fix before Thursday."

**Answer key:** **B.**

- **B is correct:** all four steps — an observation without interpretation ("draft is discarded... no warning"), the heuristic named (user control and freedom), the specific operational harm (twenty minutes of lost case notes), and a question instead of a prescription.
- **A is wrong:** starts with interpretation ("confusing") and prescribes a fix (position, color) — the exact anti-pattern; the fix is the designer's craft.
- **C is wrong:** pure feeling, no observation, no heuristic, no harm — nothing the designer can act on.
- **D is wrong:** names a heuristic by number but skips the observation and harm, and issues an order rather than a question; it treats the designer as a ticket queue, not a partner.

### Q2 (open response — production)

Write a short design brief (bullet form is fine) for this situation: claims analysts need a screen to review and correct the six machine-proposed fields before a case is created. Constraints you know: the data sample is classified "internal — approved sample only"; the client has an approved component library; keyboard-heavy analysts work through 60–80 cases per day. Include all six required brief elements.

**Model answer (element coverage, not exact wording):**

- **User and context:** claims analysts, high-volume (60–80 cases/day), keyboard-heavy, working case-by-case under time pressure.
- **Job to complete:** review six machine-proposed fields, correct any wrong ones, and confirm before a case is created.
- **User's success condition:** confirming a case is faster than manual entry today, and no wrong field reaches the case record unnoticed.
- **Known constraints:** internal-classified approved sample only; must use the client's approved component library; full keyboard path required.
- **Open questions for the designer:** how to make low-confidence proposals visually distinct without color-only signals; whether correction happens inline or in a side panel — designer to decide or test.
- **Out of scope:** visual/brand polish; the downstream case-creation flow; batch operations.

**Grading criteria:**

1. All six elements present and labeled or clearly identifiable (user/context, job, success condition, constraints, open questions, out of scope).
2. Open questions are genuinely left to the design partner to decide or test — not disguised prescriptions.
3. Constraints include the given data-classification and component-library facts (checks the learner carries real constraints into the brief).

**Difficulty / pass-bar note:** Pass = all six elements, with at least one real open question delegated to the designer; fail = a brief that prescribes the UI, omits constraints, or has no out-of-scope line (unbounded briefs are the common failure).

---

## Half B: Topic 5 — Hands-On Practice (Critique for Adoption Evidence)

**Learning objective:** Judge whether a discovery prototype's presentation could distort adoption evidence — a false positive from polish or a false negative from roughness — and tune the prototype as evidence rather than improving its appearance.

### Q1 (multiple choice — scenario/judgment)

A peer's State A prototype for the field-extraction workflow uses the client's real production styling, a polished logo header, and smooth animations — but the extraction confidence logic is faked with hard-coded values. In the pilot session, operators say "this looks ready, when do we get it?" What is the correct reading of this adoption signal?

- **A.** Strong positive signal — operators clearly want the tool; recommend promotion.
- **B.** Likely a false positive — the finished look may be driving enthusiasm and masking whether the *workflow* (review-then-confirm) actually beats manual entry; the faked confidence logic means the core question isn't even being tested.
- **C.** A false negative — operators are reacting to polish instead of rejecting the workflow.
- **D.** Neutral — visual style never affects adoption evidence either way.

**Answer key:** **B.**

- **B is correct:** polish creating "looks finished" enthusiasm is the textbook false positive from Exercise B; and because the risky part (confidence logic) is faked, the observed enthusiasm cannot be attributed to the workflow at all.
- **A is wrong:** treats presentation-driven enthusiasm as workflow evidence and jumps to promotion — the clean-code-promotion / prototype-laundering failure mode.
- **C is wrong:** inverts the definitions; a false negative is when *roughness* causes rejection of execution quality rather than the workflow.
- **D is wrong:** the entire point of Exercise B is that presentation *does* distort adoption evidence in both directions.

### Q2 (open response — judgment)

You are critiquing a peer's rough prototype: unstyled HTML, default browser fonts, a visible "DEBUG" panel, and confusing placeholder labels like `fld_3_prop`. Two of five operators refused to complete the test task, saying "this is not usable." Answer: (a) is this more likely a false negative or a false positive, and why; (b) name one change you would recommend and one you would explicitly *not* recommend, given that the goal is to tune the prototype as evidence.

**Model answer:** (a) Likely a false negative: the refusals cite execution quality ("not usable"), and cryptic internal labels plus a DEBUG panel give operators legitimate surface reasons to reject before the workflow itself is ever exercised — so the rejection may not be evidence about the workflow. (b) Recommend: replace `fld_3_prop`-style labels with analyst vocabulary and hide the DEBUG panel, because those defects block the test task itself. Do not recommend: visual polish (styling, branding, animations) — improving appearance beyond what the test needs risks swinging the distortion the other way, toward a false positive, and the goal is evidence quality, not appearance.

**Grading criteria:**

1. Correctly identifies false negative and grounds it in the operators' stated reason (execution quality, not workflow).
2. Recommended change removes an evidence-blocking defect (labels/DEBUG), not general polish.
3. Explicitly withholds appearance improvements with the false-positive risk as the reason — showing the learner treats the prototype as evidence, not a product.

**Difficulty / pass-bar note:** Pass = correct direction (false negative vs. false positive) with a change list that tunes evidence quality in both directions; fail = misreading the direction, or "fixing" the prototype by polishing it — which trades one distortion for the other.

---

*End of workshop assessment bank. 18 questions total: Half A — 8 (4 drills × 2); Half B — 10 (5 topics × 2). Every topic includes one recognition (multiple-choice) and one production (open-response) item. Source: Section 7 of `curriculum_modules-full.md`.*
