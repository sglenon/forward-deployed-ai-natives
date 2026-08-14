# Forward-Deployed Design

### A training program for converting client-facing designers into designers who ship working proofs of concept

---

## Assumptions in this draft

Change these and the structure still holds, but the pacing will shift.

- **Cohort:** 4–6 designers, run together rather than individually.
- **Duration:** 8 weeks, roughly 6–8 hours per week, alongside existing client work.
- **Support:** each cohort has one engineer mentor (technical questions, guardrail maintenance) and one senior client lead (commercial and relationship questions). Mentors are not full-time on this.
- **Prerequisites:** already client-facing, fluent in Figma, willing to live in a terminal. No prior coding requirement.
- **Machines:** mixed Windows and Mac. Windows participants work in WSL2 throughout. Setup Day forks by OS.
- **Tool tracks:** Claude Code is required for everyone. Codex and open-source/local LLM tracks are elective.
- **Existing assets:** a default tech stack decided by engineering, a starter repo, a `CLAUDE.md` ruleset, and the AI Excellence Playbook. If these don't exist yet, building them is Week 0 and it is engineering's job, not the cohort's.

---

## The thesis of the program

A designer with a working prototype in the room changes the shape of a client conversation. The client stops describing what they imagine and starts reacting to something real. A designer who can then go on to make real changes to the client's system stops being a supplier and becomes embedded. That progression is the program.

**Forward-deployed means the work ships.** If involvement stops at the prototype, this is prototyping with a better job title. So the governing idea every graduate must hold is not about prototypes. It's about knowing which kind of work they're doing:

> **Everything you build is in one of two states, and you always know which one. Moving between them is a decision someone signs off on, never something that just happens.**

### State A: Discovery build

Purpose: answer a question. Lifespan: days. Fictions are required: hardcoded data and fake sign-in are correct craft here. The bar is *real enough to react to*. Success is having learned something, including when the answer was no.

The three questions a State A build is allowed to answer:

1. Is this the right problem?
2. Does this flow make sense to the people who'd actually use it?
3. Is this roughly plausible to build?

### State B: Production work

Purpose: improve something people actually use. Lifespan: indefinite. Fictions are defects. The bar is *fits the system, breaks nothing, survives you leaving*. Success is that it shipped and nothing regressed.

This covers embedded design changes to a client's live product and any discovery build that has been formally promoted.

### Promotion: the only legal transition

A discovery build becoming production work is often the right outcome. It happens exactly one way: a named person decides, the faked list gets written, and a hardening pass is scoped and agreed as real work with real cost.

The alternative is **drift**, and nobody announces drift. Most failure modes in this program are drift wearing a different outfit.

---

## Module 0: The role and its edges

**Half day. Do this before anyone touches a keyboard.**

Content:

- Where this role comes from and why the ability to ship is what gives it credibility.
- The three questions above, and the non-goals.
- **Authority boundaries.** The list of things a forward-deployed designer never decides alone: timelines, pricing, feasibility guarantees, scope changes, and anything that becomes a long-lived architectural choice. These get named on day one and repeated in every subsequent module.
- The escalation path, with actual names attached.

Output: each participant writes, in their own words, one paragraph explaining to a hypothetical client what a PoC is and isn't. Read them aloud. The ones that sound like disclaimers have failed. It has to sound like an invitation.

---

## Module 1: Technical literacy floor

**Weeks 1–2**

The goal is not to make designers into engineers. It is to make them able to *reason about* and *talk about* what they're building, so they are neither helpless nor overconfident.

### 1.1 Setup Day

**One supervised full day, whole cohort together, engineer mentor in the room.**

Do not send installation instructions asynchronously. Environment setup is where non-engineers quietly give up, and the failures are individual and unpredictable: a PATH problem, a permissions prompt, a corporate antivirus. Doing it together turns a week of demoralizing solo debugging into one day where every failure gets solved in front of everyone.

**Fork the room by OS first.** Windows participants go the WSL route (Ubuntu under WSL2) and do everything inside the Linux terminal from that point on. Mac participants work natively. Mixing instructions between the two is the most common source of confusion; separate the tracks explicitly and let each group have its own checklist.

Install order (each step depends on the previous one):

**a. Terminal**

- Where it lives, what a prompt is, what the working directory means.
- Windows: WSL2 + Ubuntu, and the habit of using the Ubuntu terminal rather than PowerShell for project work.
- The starting command set, kept deliberately small: `pwd`, `ls`, `cd` (including `cd ..` and `cd ~`), `mkdir`, `cp`, `mv`, `cat`, `clear`.
- `rm` taught with a warning attached, because there is no recycle bin.
- Survival mechanics that save more time than any command: Tab to autocomplete, Up-arrow for history, `Ctrl+C` to stop a running process, and how to tell whether a process is still running or waiting for input.
- `--version` as a universal diagnostic, and `which` (`where` on native Windows) to answer "which copy of this is actually running."

**b. VS Code**

- Install, then the tour: file explorer, integrated terminal, source control panel, extensions.
- `code .` from the terminal to open the current folder. WSL users install the Remote–WSL extension and open projects from inside WSL so the editor and the terminal agree about where files live.
- Extensions to install now: Remote–WSL (Windows only), Prettier, and whatever the default-stack repo recommends.

**c. Node.js**

- Install via a version manager (`nvm`, or `fnm`/`nvm-windows`) rather than a direct download. Teach *why*: different projects need different Node versions, and the resulting mismatch is the single most common environment failure in this stack. Ten minutes spent here prevents a recurring support cost.
- What `npm` is, what `package.json` is, what `node_modules` is and why it is never committed.
- `npm install` and `npm run dev` as the two commands they'll use daily.

**d. Python**

- Install via a version manager or `uv` rather than touching the system Python. On Mac and Linux the system Python belongs to the operating system, and modifying it breaks things unrelated to the project.
- The virtual environment concept and why every project gets its own.
- `requirements.txt` / `pyproject.toml` as the Python equivalent of `package.json`.
- Keep this proportionate. Unless the default stack is Python-based, designers need Python present and understood, not mastered.

**e. Git and GitHub access**

- Install Git, set `user.name` and `user.email`.
- Generate an SSH key: `ssh-keygen -t ed25519 -C "your@email"`, understand that the `.pub` file is the half you share and the other half never leaves the machine, add it to the ssh-agent, paste the public key into GitHub, then confirm with `ssh -T git@github.com`.
- This is worth doing properly rather than falling back to HTTPS tokens. It's a fifteen-minute concept that removes an authentication annoyance from every subsequent day.
- Clone the studio's starter repo as the first real exercise.

**f. AI coding tools**

- Install Claude Code (see Module 2a) and, for the optional track, Codex.
- Both offer a CLI and a VS Code extension. Install both surfaces: the CLI is the primary working environment and the extension is the visual anchor that makes it approachable early on.
- Installation methods change; point at the official docs rather than a command pasted into this curriculum. For Claude Code: [https://docs.claude.com/en/docs/claude-code/overview](https://docs.claude.com/en/docs/claude-code/overview). Note that the native installer is now the recommended path and doesn't require Node.js, while the npm route is the legacy method. WSL users install and run from inside the Linux environment.
- Authenticate and confirm the install works before anyone leaves the room.

**Setup Day exit checkpoint.** Nobody finishes until every one of these prints something sensible:

```
node --version
npm --version
python3 --version
git --version
code --version
claude --version
ssh -T git@github.com
```

Plus: clone the starter repo, install its dependencies, run it locally, and see it in a browser. That last one is the actual milestone: the first time the participant makes something appear on their own machine.

### 1.2 The mental model

Browser, application, data, deployment. What lives where, what talks to what, and what it costs to change each one. Whiteboard it until they can redraw it from memory. Then map the studio's default stack onto that diagram so the abstraction has a concrete instance attached to it.

### 1.3 The default stack

What engineering picked, and more importantly, the reasoning. A designer who knows *why* the default exists is the one who notices when a client requirement breaks it, which is the moment that needs escalating.

### 1.4 Git vocabulary and workflow

The vocabulary matters as much as the commands, because it's what lets them follow an engineer's explanation without nodding blankly.

- **Terms:** repository, remote, `origin`, clone, branch, `main`, staging area, commit, push, pull, pull request, merge, merge conflict, revert, stash, `.gitignore`, `HEAD`.
- **The daily loop:** branch → change → stage → commit with a message that says why → push → open a PR.
- **Revert is the load-bearing skill.** The confidence to experiment comes entirely from knowing you can undo. Practise it deliberately: break something, then get back.
- **Merge conflicts** get demonstrated once, on purpose, so the first one they meet in real work isn't frightening.
- **Commit small and often.** For someone generating a lot of code quickly, frequent commits are the difference between a bad hour and a bad day.

### 1.5 Reading, not writing

- Reading an error message and extracting the actual signal from the stack trace noise.
- Reading a diff and saying out loud what changed.
- Looking at a file tree and guessing what each file does, then checking.
- Recognizing the difference between "it crashed," "it ran but did the wrong thing," and "it didn't run at all." These have completely different causes and telling them apart is most of early debugging.

### 1.6 Environments and secrets

`.env` files, why they're gitignored, and what an API key is. The rule is absolute and stated as a rule: a client's credentials never go into a repo, a screenshot, a chat message, or a prompt.

**Module assessment:** explain your own PoC's architecture to an engineer, out loud, in under three minutes, without saying "it" or "the thing." Vagueness here predicts vagueness in front of a client.

---

## Module 2: AI-assisted building

**Weeks 2–3**

2a is required. 2b and 2c are elective, chosen by specialty and by what the engagement mix demands. The shared principles below apply to all three and are taught once.

> **Insert the AI Excellence Playbook here.** The playbook is the governing document for this module. The tool-specific sections below are mechanics layered on top of it, and where they disagree, the playbook wins.

### 2.0 Shared principles

- **Spec before build.** A short written brief covering what this screen is for, who uses it, and what happens on success and on failure, written before generating anything. Designers already do this instinctively for visual work; the module transfers the habit.
- **Two modes of prompting.** Scaffolding (get a structure standing up) versus iteration (change one thing without disturbing everything else). Recognizing which mode you're in prevents most thrash.
- **Restart versus patch.** When output is 80% right, patch it. When it's structurally wrong, delete it and re-prompt with a better brief. Designers over-patch because deleting generated work feels wasteful. It isn't. The cost was minutes.
- **Context is a resource.** Long sessions degrade. Start fresh for a new task rather than dragging an exhausted conversation forward.
- **The 30-minute rule.** Half an hour stuck alone, then escalate to the engineer mentor. No exceptions. This prevents the failure where a designer burns a day and arrives at something that works for reasons nobody understands.
- **Never paste client data or credentials into a prompt.** Restated here because this is where it will actually be tempted.

### 2a Claude Code literacy

**Required.**

- **CLI and extension.** The terminal is the primary working environment; the VS Code extension is the visual on-ramp and stays useful for reviewing changes. Install both, work primarily in the CLI.
- **The guardrail files.** How `CLAUDE.md` and project rules work, what engineering has encoded in them, and the process for *requesting* an addition rather than quietly overriding one locally. Overriding a guardrail without telling anyone is the behaviour this module exists to prevent.
- **Plan before execute.** Getting a plan out of the agent and reading it critically before letting it write anything. This is the highest-leverage habit in the entire module and it maps directly onto how designers already work.
- **Permissions.** What the tool is allowed to do without asking, and why blanket approval is a bad idea in a client repo.
- **Reusable patterns.** Where the studio's repeated flows live (auth screens, form handling, table views) so nobody regenerates the same thing from scratch each engagement.
- **MCP servers, with Figma first.** Connecting the design source directly to the build tool is the specific capability that makes this role work for designers rather than being a worse version of engineering. Cover the studio's other connected servers as relevant.
- **Reviewing output.** Reading what changed before accepting it, every time, including when it looks obviously fine.

### 2b Codex literacy

**Optional.**

Same principles, different surface. Worth covering for participants who'll work across client environments that have standardized on it, or who benefit from a second opinion on a stubborn problem.

- CLI and IDE extension install and authentication.
- The project-instruction file convention and how it maps to what they learned in 2a.
- Where the working loop differs in practice: approval model, how tasks are delegated, how results come back.
- When to reach for it over Claude Code, and when running both on the same problem is worth the time versus just being indecisive.

*Engineering to supply current specifics; this tool moves quickly and anything written here will date.*

### 2c Open-source and local LLM literacy

**Optional.**

Relevant for participants working with clients who have data-residency constraints, or for internal work where cost or offline capability matters.

- Running models locally: the common runtimes, and what hardware actually supports.
- Open-weight versus hosted, and what the capability gap looks like in practice rather than on a benchmark.
- The honest positioning: local models are for sensitive, narrow, or repetitive tasks, not for the main build loop of a client PoC. A participant who leaves this track thinking they can substitute a local model for the primary tooling has learned the wrong lesson.
- Deployment-adjacent basics if the studio offers this to clients: where it runs, who maintains it, what it costs.

**Module assessment:** rebuild an existing Figma flow as a working PoC in one working day. Judged on whether it runs and whether the participant can explain what the code does, not on polish.

---

## Module 3: Verification

**Weeks 3–4. This is the most important module in the program.**

The core risk of AI-assisted building is that output arrives looking correct faster than the builder can determine whether it is. Inside a codebase that's a review problem. In front of a client it's a reputation problem.

- **What "working" means.** The happy path is not the path. Explicit coverage of: empty states, error states, loading states, bad input, mobile viewport, refresh, back button, and what happens when the data isn't the sample data.
- **Adversarial self-review.** A written checklist the participant runs against their own work before anyone else sees it. Cohort maintains and improves the checklist over the program; it becomes a studio asset.
- **Naming what's fake.** Every PoC contains fictions: hardcoded data, mocked auth, a button that goes nowhere. These are legitimate and often correct. The discipline is that every one of them is *written down as it's created*, not reconstructed afterward.
- **The demo conditions test.** Would this survive on the client's laptop, on their wifi, with their data, with their colleague clicking around unsupervised? Most PoCs fail at least one. Knowing which is the point.

**Assessment:** participants are paired and given two hours to break each other's Module 2 builds. Both the breaks and the *undiscovered* breaks get documented. This does more for verification instinct than any lecture.

### 3b The production track

State B has a different bar, and this half of the module is the gate to being allowed near a client's real system.

- **Blast radius.** Before touching anything, knowing what depends on it. Shared components, design tokens, and anything reaching data or live users are never local changes.
- **Regression awareness.** Checking the screens you didn't change. The habits that make you fast in discovery are exactly the habits that cause invisible regressions.
- **Working inside someone else's system.** The client's design system and conventions constrain you, including where you'd have chosen differently. Deviating is a conversation, not a preference.
- **Reversibility.** Small commits, working branches, and knowing how to get back. In State A a bad hour costs an hour; in State B it can cost a release.

**Assessment:** make a change to a shared component in a realistic codebase, then produce the list of everything that could have been affected and evidence you checked it.

---

## Module 4: The client conversation

**Weeks 4–5**

This module leans on what designers are already good at and sharpens it toward the new capability.

- **Symptom versus problem.** Clients describe symptoms. "Reporting takes three days" might not be a software problem at all. Practice extracting the real constraint before proposing anything.
- **Building live.** When it lands as magic and when it becomes a disaster. Rules: never live-build something you haven't built once before, always have a working fallback open in another window, and stop the moment debugging starts.
- **The expectation script.** How to say "this is a prototype" so it actually registers. Framing it as a question the prototype answers works better than framing it as a limitation of the prototype.
- **"Great, can we launch this next week?"** The single most dangerous sentence in this role. Scripted, rehearsed, role-played until the response is automatic. The response is never yes and never a flat no; it's a redirect to the people who can scope it.
- **Reading the room.** Who has authority, who feels threatened by the project, whose approval the champion actually needs. Good work dies here routinely.

**Assessment:** role-played client session with a senior playing a difficult client. Scored on discovery quality and on whether the participant held the authority boundaries under pressure.

---

## Module 5: Handoff

**Weeks 5–6**

Handoff differs by state, and conflating the two is how drift happens.

### 5a Handing off a discovery build

Three required deliverables at the end of every discovery engagement:

1. **The faked list.** Everything fictional in the build, and what a real version would require.
2. **The decision log.** What was chosen, what was assumed, what was deliberately deferred. Keep it to a page.
3. **The open questions.** What the build failed to resolve, stated plainly. A discovery build that answered nothing is a finding, not a failure.

Then: a working session with engineering to translate the build into a scope and estimate, with the designer present. Attending this session is what teaches the designer what their choices cost.

### 5b Handing off production work

Different job. The work is staying, so the handoff is about whoever maintains it next.

- Following the client's existing review and release process rather than inventing one.
- Documenting *why*, not what. The diff already says what changed.
- Design system contributions handed over so the client's own team can extend them.
- An explicit end-of-engagement handover: what you touched, what's unfinished, what you'd do next.

### 5c Running a promotion

When a discovery build is promoted, this is the checklist:

1. The decision is recorded, with a name against it.
2. The faked list becomes the work list.
3. The hardening pass is scoped and costed *before* anyone starts.
4. The artifact is re-labelled State B, and everyone touching it knows.

A promotion that skips any of these four is drift with extra steps.

---

## Module 6: Capstone

**Weeks 6–8**

A real engagement, scaffolded. Senior owns the relationship and the framing; the designer owns discovery for a narrow scope and owns the build. The engineer mentor is on call but does not touch the code.

Deliverables: the PoC, the three handoff documents, and a recorded client walkthrough.

Debrief covers what the client actually did with it, which is the only real measure.

---

## Levels after the program

Graduation from the course is not graduation to solo work. The levels gate **which state of work a person is trusted with**, not just how much client contact they get. Nobody touches a client's production system on the strength of having finished a course.


| Level         | Client contact                   | Trusted with                                        | Can decide                                                   |
| ------------- | -------------------------------- | --------------------------------------------------- | ------------------------------------------------------------ |
| **Shadow**    | Present, observing               | State A, paired                                     | Nothing alone                                                |
| **Supported** | Runs the session, senior in room | State A alone; State B only paired with an engineer | Design and flow decisions                                    |
| **Embedded**  | Runs the engagement              | State A and State B within an agreed scope          | Everything inside that scope; escalates the never-alone list |


Nobody moves up on time served. Movement requires a specific demonstrated thing. Most usefully, evidence they escalated something they could have gotten away with handling alone.

**The Supported → Embedded gate is verification, not build skill.** The question is never "can they build it," because by that point they obviously can. It's whether they can prove their own work is right, catch their own regressions, and recognize blast radius before touching something. Module 3 is that gate.

---

## What the organization has to supply

The program fails without these, and none of them are the cohort's responsibility.

- A maintained starter repo and guardrail ruleset, owned by an engineer with time allocated to it.
- Two OS-specific Setup Day checklists (Windows/WSL and Mac), version-dated and revised after each cohort. Tooling install methods change often enough that a stale checklist will burn a full day.
- Mentor hours that are genuinely protected, not squeezed between billable work.
- A safe first engagement for the capstone: an internal project or a forgiving client.
- A decision about who absorbs the cost when a PoC turns into unplanned scope. Answer this before the first cohort ships anything.

---

## Risks worth watching

**The 80% illusion.** A working PoC reads as nearly finished to non-technical stakeholders. Every mitigation in Module 4 targets this, and it will still happen. Expect to manage it commercially, not just verbally.

**Scope absorption.** A designer with client trust and the ability to build is the ideal person for a client to quietly route work to. This is the most likely way the program costs money instead of making it.

**Designer becomes shadow engineer.** If PoC work crowds out design work, you've converted a designer into a mediocre engineer and lost what made them valuable. Cap the proportion of time in build mode and watch it.

**The remediation loop.** Fast-built prototypes that get extended into production are exactly the artifact that generates painful month-six problems. Module 5 exists for this reason. If handoff discipline slips, this program becomes a source of the thing it should prevent.