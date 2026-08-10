# Forward Deployed Design
## Modules 0 to 2, consolidated

Master reference for the Forward Deployed Designer course. Each `##` heading is one LMS item.

Delivery is individual and self-paced. Items are in dependency order within each module.

**Source of truth:** The LMS uses the HTML files in `lms-html/`. The system generates them from `generators/`. This document is the master for review and editing. If you change text here, apply the same change to the generators. If you do not, the two versions will not match.

---
---

# Module 0: The Role and Its Edges

Duration: half a day. Complete this module before using a computer. Do not skip it.

All other modules teach techniques. This module teaches the judgment that guides those techniques. A person who skips this module learns to build quickly but does not know when to stop.

---

## 0.1 Why this role exists

You already have the skills that are hardest to teach. This module describes what you will add to them.

A software role called the **forward-deployed engineer** started at Palantir. The reason for this role applies directly to this program.

Palantir sold a data platform to organizations with complex problems: banks, hospitals, and government agencies. The difficult part was never the platform. The difficult part was **translation**. Someone had to work inside the customer's environment, understand the customer's specific problem, and build the solution. That person needed to build. That person also needed to be present where the problem existed. A salesperson cannot do both. A standard product engineer cannot do both.

This role is in demand again because AI companies face the same problem. AI models are general-purpose and highly capable. Most organizations cannot identify how to apply them. The bottleneck is not capability. It is application.

> **THE PART PEOPLE GET WRONG**
>
> Forward-deployed does not mean "creates prototypes for clients." Palantir's forward-deployed engineers wrote code that customers ran in production. If involvement ends at the demonstration, this is not the forward-deployed role. It is prototyping with a different job title.
>
> **Your work ships.** This is the key distinction. It is why this module focuses on discipline rather than technique.

### Our version of this bet is specific to you

The forward-deployed role has two halves.

1. **Technical breadth.** Enough range to build something end-to-end without depending on other people.
2. **Non-technical skills.** Reading people in a meeting. Finding the real problem behind a stated problem. Knowing whose approval matters. Recognizing when a client agrees without understanding.

The second set of skills is much harder to teach. Most organizations start with engineers and try to develop client skills in them. This approach is slow and often fails.

> **THE PREMISE OF THIS PROGRAM**
>
> You already have the second set of skills. You have worked with clients for years. You recognize when a conversation stalls. You recognize when a stakeholder is protecting their area. You already work by creating something for the client to react to, instead of asking them to imagine it.

You are missing the first set of skills. AI tools have made these skills much cheaper to acquire than they were three years ago.

> You are not becoming an engineer. You are acquiring enough technical skill to work inside a client's real system, not alongside it.

---

## 0.2 The two states of your work

Because your work ships, one distinction affects everything in this role. Getting it wrong causes problems in everything that follows.

> **Every build is in one of two states. You always know which state it is in. Moving between states requires a decision from a named person. It never happens without that decision.**

| | State A: Discovery build | State B: Production work |
|---|---|---|
| **Purpose** | Answer a question | Improve something people actually use |
| **Lifespan** | Days | Indefinite |
| **Fictions** | Required. Hardcoded data and fake sign-in are correct. | Defects. Each one is a bug with a delay. |
| **Bar** | Real enough to react to | Fits the system, breaks nothing, survives you leaving |
| **Success** | You learned something, including when the answer was no | It shipped and nothing regressed |

These are not two levels of quality. They are two different jobs with opposite rules. A hardcoded array is good practice in State A and a liability in State B. One day spent on error handling is good practice in State B and waste in State A.

"Just build it properly the first time" is bad advice for this reason. Building a discovery build to production standards removes the speed that makes a discovery build useful.

### Why State A needs framing that State B does not

A wireframe uses grey boxes and placeholder text. Nobody mistakes a wireframe for a finished design. The incompleteness is clear. The shared understanding is automatic. You never need to explain it.

A working discovery build removes that shared understanding. The build runs. Buttons respond. Screens change. To any non-technical person, it looks and behaves like finished software. Every visual signal that said "this is early work" is gone. Nothing has replaced those signals.

> **WHAT THIS MEANS**
>
> The framing that was automatic before is now something you provide deliberately, every time you show State A work. This is not an addition to your job. It is how this job works.

### What State A is allowed to answer

1. **Is this the right problem?** The client described a symptom. Building the obvious response reveals quickly and cheaply whether that response actually helps.
2. **Does this flow make sense to the people who would use it?** Not to the client's executive sponsor. To the dispatcher, the nurse, the warehouse supervisor — whoever uses it daily.
3. **Is this roughly plausible to build?** Not "how long will it take." Whether the structure is sound, whether the data the client says they have is available in the form described, whether the assumed integration exists.

Write down one of these questions before you start every discovery build. If you cannot name the question, you are not in State A. You are building without a reason.

### What a State A build is not

- **Not a foundation.** Nothing in it is designed to last.
- **Not an estimate.** That it took three days tells you nothing about the real build. The parts you skipped are usually the expensive parts.
- **Not a commitment.** Showing a client a feature is not agreeing to build it.
- **Not production, no matter how good it looks.** This is especially true when it looks good.

### Promotion: the only legal way across

A discovery build can become production work. This is often the right outcome. But it happens only one way:

1. **Someone decides.** A named person makes an explicit decision that this build goes into the real system. The client saying "great, let's use it" is not a decision. Someone must record the decision.
2. **Someone lists the fictions.** Write down everything fake in the build in the faked list from Module 5. You cannot replace what nobody recorded.
3. **Someone scopes a hardening pass.** Replacing the fictions is real work with real cost. Scope it and agree on it before anyone starts.

> **THE FAILURE THIS PREVENTS**
>
> The alternative to promotion is **drift**. Nobody announces drift. It happens when a client says "can you just tidy that up so we can start using it," and you say yes because it is a small change. Four months later the fake sign-in is in front of real customers.

Every build has one state. You always know which state it is in. This is the complete rule.

---

## 0.3 The six ways this goes wrong

Each later module in this program prevents one of these failures. Read them now so each module has a purpose when you reach it.

Four of the six are the same failure under different conditions: something moved between State A and State B without a decision. The list below marks these.

### 01. The 80% illusion
`DRIFT IN THE CLIENT'S HEAD`

*A client watches you click through a working booking flow. Their expression changes. They say, "This is great, so we're basically there?" You are not there. The screens are the inexpensive part. The durable, secure, maintainable system underneath them is the expensive part, and none of it exists.*

**Why it happens.** Working software is a strong signal of completeness. Nothing tells the client that none of this is real. The client silently moves your State A build to State B, because nothing told them not to.

**What prevents it.** The framing you write in item 0.5, and the faked list in Module 5. This failure will happen anyway. Managing it is an ongoing task, not a one-time fix.

### 02. The confident wrong answer

*You build exactly what the client described, quickly and well. They are impressed. Six weeks later, a compliance requirement that nobody mentioned makes the entire flow unusable.*

**Why it happens.** Speed creates pressure to start building before discovery is complete. When you can produce something in two days, the pressure to skip difficult questions increases, not decreases.

**What prevents it.** Module 4: symptom versus problem, and the discipline of naming your question before you build.

### 03. The accidental commitment

*Someone asks, casually, "roughly how long would the real version take?" You want to help. You say "probably a couple of months." That number is now in their notes and in their board presentation. Nobody will remember you said "probably."*

**Why it happens.** You are the person the client trusts and you are visible. Both factors make you the natural target for questions you are not authorized to answer.

**What prevents it.** Item 0.4, practiced until the redirect is automatic.

### 04. The quiet promotion
`DRIFT IN THE ARTIFACT`

*The client liked the discovery build and asked their own developer to "just finish it off." Nobody scoped a hardening pass. Nobody listed what was fake. Eight months later the system is not maintainable, and it has our name on it.*

**Why it happens.** Promotion is the correct outcome for a good discovery build, so agreeing feels right. What was missing was not the agreement. It was the decision, the faked list, and the scoped work to replace the fictions.

**What prevents it.** Module 5. The faked list and the decision log exist for this purpose. They are required deliverables for this reason.

### 05. Becoming the client's shadow engineer
`DRIFT IN THE RELATIONSHIP`

*You are trusted, responsive, and you can build things. Small requests start arriving directly to you. None of them seems worth escalating. Six weeks later, you are doing unbilled production work for a client you were supposed to be running discovery with.*

**Why it happens.** This type of drift is gradual and each individual request is small. Once you can do production work, requests no longer feel out of scope, because technically you can do them.

**What prevents it.** Notice early. If you are building something that nobody scoped, this requires a scope conversation, not a favor.

### 06. The invisible regression
`STATE B ONLY`

*You change a shared component to fix spacing on one screen. It looks correct. Three other screens you have never opened now have broken layouts. You find out from a support ticket eleven days later.*

**Why it happens.** In State A, a change affects nothing else, because nothing depends on your work. In State B, anything might depend on it. The habits that made you fast in discovery cause this problem.

**What prevents it.** Module 3's production track. Know what depends on a component before you change it. Never treat a shared component as a local change.

---

## 0.4 Where your authority ends

You will be the most trusted person in the meeting and visibly able to change the client's real system. This combination means people will ask you questions you are not authorized to answer.

There are five categories. Learn them.

### The never-alone list

1. **Timelines and cost.** Any duration, any number, any cost estimate, including qualified ones. The words "probably," "roughly," and "it shouldn't be too expensive" lose their qualifiers when repeated.
2. **Feasibility guarantees.** "Yes, we can do that" is a commitment. "That's a good question, let me get you a real answer" is not. The second response costs you nothing.
3. **Scope changes.** Anything not in the current agreement. Especially small scope changes, because small ones lead to large ones.
4. **Promotion.** Declaring that a discovery build goes into the real system. This is never your decision alone, no matter how ready the build looks or how enthusiastic the client is.
5. **Blast radius.** Shared components, the design system, anything that touches data, and anything live users can reach. If a change could affect a screen you have not opened, it is not a local decision.

### Why this list is short and absolute

Judgment calls are exhausting. A rule you must evaluate each time is a rule you will eventually get wrong under pressure. The pressure is real, because the person asking is usually friendly and declining will feel uncomfortable.

These five items are not guidelines. They are absolute rules. Do not cross them alone. Do not evaluate them each time. That is much easier to hold in a client meeting late in the day.

> **READ THIS TWICE**
>
> **Escalating is not admitting you could not handle something. It is a demonstrated senior behavior. It is how you progress in this program.**
>
> Progression between levels requires evidence that you escalated something you could have handled alone. This is not a formality. Someone who never escalates is not confident. They are someone whose mistakes have not surfaced yet.

### Your escalation paths

*Replace the placeholders below with real names before publishing this item. Do not use a path with a blank.*

| Question type | Goes to | How fast |
|---|---|---|
| Timeline, cost, scope, contract | *[client lead]* | Before you respond |
| Promoting a discovery build | *[client lead]* + *[your mentor]* | Before you agree |
| Blast radius: shared components, data, live users | *[your mentor]* | Before you build it |
| Technical feasibility | *[your mentor]* | Same day |
| Stuck for 30 minutes | *[your mentor]* | Immediately |
| Client relationship getting worse. | *[client lead]* | Immediately |
| Something you cannot categorize | *[client lead]* | Immediately |

### The holding phrase

Memorize one sentence that gives you time without seeming evasive. For example:

> "That's exactly the right question, and I want to give you a real answer rather than a guess, so let me bring it back to the team and come to you with something solid."

Write your own version in your own voice. Say it out loud until it feels natural. You will use this sentence more than any other in this role.

---

## 0.5 The framing exercise

**Assessed.**

State B work shows its own results: it shipped or it did not. State A work requires language around it, because it looks finished and is not. This exercise is about showing a discovery build.

> **YOUR TASK**
>
> Write the short piece you would say to a client at the moment you first show them a discovery build. Five or six sentences, in your voice, written to be spoken out loud.

Before you write, read these two examples.

### Version A (fails)

> "So just to set expectations before I show you this, it's only a prototype, so a lot of it doesn't actually work yet. The data isn't real and there's no proper login. We'd need to rebuild most of this properly before it could go anywhere near production, so please bear that in mind as you're looking at it."

Everything in Version A is true. It still fails.

It is apologetic, which invites the client to discount work that was genuinely useful. It lists limitations without saying what the build is *for*. It makes "how long until it's properly built" the obvious next question. It positions you as apologetic while demonstrating something useful.

### Version B (works)

> "What we've built answers one question: does this booking flow make sense to your dispatchers? Everything you can see is real enough to react to, and nothing behind it is real. The schedules are invented, and the sign-in is a shortcut. That's deliberate. We wanted to find out whether the flow is right before anyone spends money making it durable. So click around, and tell me where a dispatcher would get stuck."

Same build. Same limitations. A different conversation.

It opens with the question, so the client knows what they are evaluating. It states the fictions plainly and claims them as intentional. It gives the client a task — "tell me where someone would get stuck" — which is more useful than "what do you think." It frames durability as a separate, later, costed activity. This removes "so how close are we" before it is asked.

### What yours needs

- [ ] The question this build answers, in the first sentence
- [ ] What is fake, stated plainly and without apology
- [ ] Why it is fake, framed as a decision rather than a limitation
- [ ] A specific task for the client to do while clicking
- [ ] No numbers, no durations, no guarantees
- [ ] Nothing that could be heard as agreeing to promote it

> **THE TEST**
>
> Read your version out loud, to yourself. This step is required: this is copy meant to be spoken, and problems that are invisible on the page are obvious when you hear them.
>
> If it sounds like a disclaimer, rewrite it. If it sounds like an invitation, you are done. Bring the final version to your mentor.

---

## 0.6 Close

Three things to take into Module 1.

1. **You already have the difficult skills.** The technical capability you are about to acquire is real. It is also less rare than what you already do. Client judgment is the scarce skill.
2. **Always know which state you are in.** Discovery build or production work. If you cannot say which without thinking, stop and find out. Everything else in this program assumes you know.
3. **Speed is an advantage only when the work is trustworthy.** Producing something useful quickly is worthless if nobody can tell whether it is correct. This is why Module 3 exists. Module 3 is also the gate to working in a client's real system.

> **BEFORE MODULE 1**
>
> Bring your laptop, your admin password, and three hours. Setup is the least interesting part of this program. It also most determines whether the rest of the program works.

---
---

# Module 1: Technical Literacy Floor

Weeks 1 to 2. Eleven items, in dependency order.

---

## 1.1 What this module is for

This module does not teach you to write code. It teaches you to read code, reason about it, and discuss it accurately.

This distinction is now more important than before. Your tools write the code. They write it faster than an untrained person can evaluate. The gap between *producing* output and *knowing whether the output is correct* is the main risk in this role.

> Everything in this module reduces that gap.

### What you are building toward

- A machine you set up yourself and can fix when it breaks
- Enough vocabulary to follow an engineer's explanation
- The ability to read an error, a diff, and a file tree
- One absolute rule about client credentials that you never break

The final item is the assessment: explain your own build out loud to an engineer in under three minutes. Everything before that item is preparation.

### How to work through this

Items are in dependency order. Item 1.3 requires that 1.2 worked. Do not skip items. Do not continue from a broken step. Every later failure will trace back to the broken step and will be harder to diagnose.

> **THE 30 MINUTE RULE STARTS NOW**
>
> If you are stuck on any single step for 30 minutes, stop and message your mentor. This is not a last resort. It is the expected action. Environment problems are individual and hard to predict. Someone who has seen the error before will usually recognize it in seconds.

Expect this module to feel less rewarding than later modules. Setup is the least interesting part of this program. It also most determines whether everything after it works.

---

## 1.2 Your terminal and editor

Two tools, installed together, because the useful part is how they communicate with each other.

### First: which track are you on

Everything in this program requires a Linux-style environment. On a Mac you already have one. On Windows you install one.

**Windows.** Install WSL2 with Ubuntu. After that, do **all** project work inside the Ubuntu terminal. Do not use PowerShell or Command Prompt.

```
wsl --install -d Ubuntu
```
*(PowerShell, as Administrator)*

Reboot when prompted. Open Ubuntu from the Start menu. Create your Linux username and password.

**macOS.** Open Terminal from Applications, Utilities. You already have what you need. If prompted to install the Xcode Command Line Tools at any point during this module, accept. This supplies tools that later steps need.

> **WINDOWS: THE ONE MISTAKE TO AVOID**
>
> Do not mix PowerShell and Ubuntu. Commands that work in one fail in the other. Files appear to be missing when they are in the other environment. The error messages do not indicate this. If a step is not working, check which terminal you are in before anything else.

### What a terminal actually is

A terminal shows a prompt waiting for a command. It also shows where it is in your file system. This location is the **working directory**. Most confusion for new users comes from not knowing their current location.

Start with these commands. They are enough for weeks.

| Command | What it does |
|---|---|
| `pwd` | Print working directory. Where am I? |
| `ls` | List what is in here. |
| `cd folder` | Change directory, go into a folder. |
| `cd ..` | Go up one level. |
| `cd ~` | Go to your home directory. |
| `mkdir name` | Make a new folder. |
| `cp a b` | Copy a to b. |
| `mv a b` | Move or rename a to b. |
| `cat file` | Print a file's contents to the screen. |
| `clear` | Clear the screen. Nothing is deleted. |

> **RM DELETES PERMANENTLY**
>
> There is no recycle bin. `rm` removes a file permanently. Read the whole command before pressing enter, every time. Be careful with anything containing `-rf`.

### Survival mechanics

These save more time than any command in the list above.

| Key or flag | What it does |
|---|---|
| `Tab` | Autocomplete a file or folder name. Use it constantly. It also confirms the item exists. |
| `Up arrow` | Recall previous commands. Faster and less error-prone than retyping. |
| `Ctrl + C` | Stop whatever is running. Your exit. |
| `--version` | Append to almost any tool to check it is installed and which version. |
| `which name` | Show which copy of a tool is running. Answers "why is it using the wrong version?" |

Note this: when a command finishes, you get your prompt back. If you do not have a prompt, something is still running or waiting for your input. This observation resolves many apparent freeze problems.

### VS Code

Install VS Code from the official site. Open it once and find four items: the file explorer, the integrated terminal, the source control panel, and the extensions panel. You use all four daily.

Install these extensions now:

- **Remote – WSL** (Windows only). Without it, VS Code and your terminal disagree about where your files are.
- **Prettier**, for consistent code formatting.
- Any extensions the starter repository recommends when you open it later.

These two tools connect with one command. From a terminal, inside a project folder:

```
code .
```

Windows: run this command from your Ubuntu terminal, not PowerShell. VS Code opens in WSL mode.

---

## 1.3 Node and Python

Two runtimes. Install both through a version manager, not directly. The reason is worth understanding.

### Why version managers exist

Different projects need different versions of the same runtime. A client repo from last year may need an older version of Node than a new project needs. If you install one version directly, you will eventually reach a project that will not run. The error message will not say "wrong version." It will describe a module failing to load.

> **THIS IS THE MOST COMMON BREAKAGE IN THIS STACK**
>
> Version mismatch, usually between Node and npm, is the most common failure in this program. A version manager makes it a 30-second fix instead of an afternoon problem.

### Node

Install `nvm` (Node Version Manager) first. Follow the install instructions on its official repository. Then use it to install Node. On Windows, do this inside your Ubuntu terminal.

```
nvm install --lts
nvm use --lts
node --version
npm --version
```

Three ideas to understand:

- **npm** Node's package manager. It downloads the libraries a project depends on.
- **package.json** The project's list of dependencies and its available commands. When you want to know how to run something, look here first.
- **node_modules** Where downloaded libraries are stored. This folder is large, can be regenerated, and is never committed to Git.

The two commands you use daily:

| Command | What it does |
|---|---|
| `npm install` | Download everything this project depends on. Run once after cloning. |
| `npm run dev` | Start the project locally. The exact name comes from package.json. |

### Python

Install through `uv` or a version manager. Follow its official install instructions. Do not install packages into the system Python.

> **WHY YOU MUST NOT USE THE SYSTEM PYTHON.**
>
> On Mac and Linux, the Python that came with your machine belongs to the operating system. Other software depends on it. Modifying it breaks software that has nothing to do with your project. This connection is not obvious when it happens.

The key concept is the **virtual environment**: a set of packages that belongs to one project only. Every Python project gets its own virtual environment. Projects cannot break each other this way.

The Python equivalents of `package.json` are `requirements.txt` or `pyproject.toml`. Same purpose, different file name.

> **KEEP THIS PROPORTIONATE**
>
> Unless the studio default stack uses Python, you need Python present and understood, not mastered. Install it, understand what a virtual environment is, and continue.

---

## 1.4 Git and GitHub access

Install Git, prove to GitHub that your machine is yours, then clone your starter repository.

### Install and identify yourself

Git usually comes with macOS and Ubuntu. Check first. Install only if it is missing. Then tell Git who you are. The name and email you set appear on every commit you make.

```
git --version

git config --global user.name "Your Name"
git config --global user.email "you@company.com"
```

### SSH keys

An SSH key is a matched pair of files. The public half you can share. The private half never leaves your machine. GitHub stores the public half and uses it to identify you. This means you do not need to authenticate each time.

```
ssh-keygen -t ed25519 -C "you@company.com"
```

Press enter to accept the default location. Setting a passphrase is optional and recommended.

```
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

```
cat ~/.ssh/id_ed25519.pub
```

Copy that entire output. Paste it into GitHub under Settings, SSH and GPG keys, New SSH key.

> **THE FILE EXTENSION IS THE WHOLE POINT**
>
> The file ending in `.pub` is the public half. It is the only file you ever copy anywhere. The file without an extension is private. If you are about to paste a key and are not certain which one you have, stop and check.

Confirm it worked:

```
ssh -T git@github.com
```
*(expect a greeting with your username)*

The first connection asks you to confirm GitHub's fingerprint. Answer yes.

> **WHY BOTHER, WHEN TOKENS EXIST**
>
> You can use HTTPS with a personal access token instead. SSH keys are worth the 15 minutes because they remove an authentication step from every day that follows. Understanding the public and private halves is also a concept you will meet again.

### Clone the starter repository

Your mentor will give you the repository address. This is your first real exercise:

```
cd ~
mkdir projects
cd projects
git clone git@github.com:your-org/starter-repo.git
cd starter-repo
code .
```

Do not run the project yet. That happens at the checkpoint in item 1.6.

---

## 1.5 Claude Code and Codex

The tools you will use most during your work day.

### Claude Code

Use the native installer. It does not need Node.js. It sets your PATH for you and updates automatically.

```
curl -fsSL https://claude.ai/install.sh | bash
```
*(macOS, Linux, and WSL)*

> **WINDOWS USERS: RUN THIS INSIDE UBUNTU**
>
> Use your WSL terminal, not PowerShell. Install and run Claude Code from the same Linux environment where your projects live. If you do not, Claude Code looks at a different file system.

Open a new terminal window after installation so your shell picks up the PATH change. Then confirm:

```
claude --version
claude doctor
```

`claude doctor` is useful to remember. Run it first when something behaves unexpectedly. It usually identifies the problem.

Run `claude` inside a project folder to start. Follow the prompts to authenticate with your studio account.

### Two surfaces, one tool

Install both the terminal version above and the VS Code extension from the marketplace.

| | The CLI | The VS Code extension |
|---|---|---|
| **What it is** | Claude Code in your terminal | The same tool, in your editor |
| **Use it for** | Everything. This is the primary working environment. | Reviewing changes visually, and as a starting point while the terminal is unfamiliar |
| **Why** | Full capability, and the way the rest of the studio works | Seeing a diff with syntax highlighting is easier than reading it as plain text |

Start in whichever feels comfortable. Work primarily in the CLI by the end of Module 2.

> **IF THE INSTALL COMMAND FAILS**
>
> Installation methods change. The current instructions are at **code.claude.com/docs/en/setup**. Check there before spending time troubleshooting. Then apply the 30 minute rule.

### Codex

**Optional.** Install this only if you are on the Codex elective track in Module 2, or if a client environment you work in uses it.

Both a CLI and an IDE extension are available. Your mentor will provide current install instructions. This tool changes quickly enough that instructions written here would become outdated.

If you are not on that track, skip it. An unused tool on your machine is another thing that can break.

---

## 1.6 Setup checkpoint

Confirm the machine works before continuing. Do not treat a partial pass as a pass.

Run each of these commands. Each one should print a version number or a message, not an error.

```
node --version
npm --version
python3 --version
git --version
code --version
claude --version
ssh -T git@github.com
```

> **A MISSING COMMAND IS NOT A SMALL PROBLEM**
>
> If any line fails, that tool is not installed or not on your PATH. Every later item that depends on that tool will fail in a way that looks unrelated. Fix it now, or escalate it now.

### The actual milestone

The seven checks above confirm tools are installed. The steps below confirm they work together. This is the real gate.

1. **Clone the starter repository.** You did this in item 1.4. Confirm you can find it and open it with `code .`.
2. **Install its dependencies.** Run `npm install` and let it finish. It may take a few minutes and print a large amount of output. This is normal.
3. **Start it.** Run `npm run dev`. Look for a line in the output containing a local address, such as localhost followed by a port number.
4. **Open it in a browser.** Paste that address into your browser. Something should appear.

> That last step is the milestone. It is the first time you have made something run on your own machine. Everything else in this program builds on this.

### Before you move on

- [ ] All seven version checks pass
- [ ] The starter repository is cloned and opens in VS Code
- [ ] Dependencies installed without errors
- [ ] The project runs locally and you have seen it in a browser
- [ ] You know how to stop it (`Ctrl + C`)

If any item is not complete, do not continue to item 1.7. Message your mentor with the exact command you ran and the exact output you received. Copy the output as text, do not describe it from memory.

---

## 1.7 How the pieces fit together

A model you can draw from memory, with the studio's default stack mapped onto it.

Almost every application you will work on has four layers. Knowing which layer a problem is in tells you who to ask and what it will cost to change.

1. **The browser.** What the user sees and clicks: buttons, layouts, forms. Changes here are usually low cost and visible immediately.
2. **The application.** The logic. What happens when a button is pressed, what rules apply, what gets calculated. Changes here cost more and are not visible until something behaves differently.
3. **The data.** What is stored and how it is structured. Changes here are the most expensive, because existing data must be migrated and mistakes are difficult to reverse.
4. **Deployment.** Where everything runs so other people can reach it. Usually not visible until it breaks.

> **THE USEFUL INSTINCT**
>
> The cost of change increases as you go down that list. A client asking to move a button and a client asking to change what a record means can sound similar in a meeting. They are not similar. Recognizing which one is being requested is a senior skill.

### Draw it

Draw these four layers with arrows showing what communicates with what. Do this from memory. Check it. Redraw until it is correct. You will use this diagram in the assessment.

### The default stack

Your mentor will explain what the studio chose for each layer, and more importantly *why*. Write down the reasoning, not just the names.

The reason the reasoning matters: a designer who knows only the names can tell a client what the studio uses. A designer who knows the reasoning can recognize when a client requirement breaks an assumption. The stack depends on that assumption. That recognition is when escalation is needed. It is a valuable skill.

> **WHEN REQUIREMENTS ARE UNCLEAR, THE DEFAULT WINS**
>
> You will often start building before all requirements are clear. In that situation, use the default stack. Choosing a different stack is a conversation with an engineer, not a personal preference.

---

## 1.8 Git vocabulary and the daily loop

The vocabulary matters as much as the commands. It lets you follow an engineer's explanation instead of appearing to understand.

### The words

- **Repository (repo)** A project and its entire history.
- **Remote** A copy of the repo that lives elsewhere, usually on GitHub.
- **origin** The default name for your main remote.
- **Clone** Copy a remote repo to your machine, history included.
- **Branch** A parallel line of work. Yours to break without affecting anyone else.
- **main** The branch everyone agrees is the current version.
- **Staging area** The set of changes you have selected for your next commit.
- **Commit** A saved snapshot with a message explaining why.
- **Push** Send your commits to the remote.
- **Pull** Bring other people's commits to your machine.
- **Pull request (PR)** A proposal to merge your branch into main, reviewable by others.
- **Merge** Combine one branch into another.
- **Merge conflict** Two people changed the same lines. Git stops and asks you to decide.
- **Revert** Undo. The most important word in this list.
- **Stash** Set your current changes aside temporarily without committing.
- **.gitignore** A list of files Git should never track, such as node_modules and .env.
- **HEAD** Your current position in the history.

### The daily loop

Five steps, repeated for every piece of work.

```
git checkout -b my-change     # branch
                              # ...make your changes...
git add .                     # stage
git commit -m "why, not what" # commit
git push -u origin my-change  # push, then open a PR on GitHub
```

On commit messages: the diff already shows what changed. The message should say why. Someone reading it four months later needs to understand the intent, not re-derive it.

### Revert is the skill everything else depends on

> The confidence to try new things comes from knowing you can undo them.

This is why learning Git properly matters. When you know you can undo anything, you try things you would otherwise avoid. Trying things is most of how this role works.

Practice this before you need it. Break something on a branch, commit the breakage, then return to where you were. Do this twice.

### Two habits

1. **Commit small and often.** When you are generating a large amount of code quickly, frequent commits are the difference between losing an hour and losing a day. Commit whenever something works, even partially.
2. **Create a merge conflict deliberately.** Ask your mentor to walk you into one on purpose, so the first conflict in real work is familiar rather than alarming. Conflicts look worse than they are.

---

## 1.9 Reading, not writing

The core skill of this module. Your tools write. You read. You decide whether what they wrote is correct.

### Reading an error message

Errors look like large blocks of text. Most of that text is a stack trace: a list of what was happening when the failure occurred. Most of the trace is code you did not write and do not need to read.

1. **Read the first line and the last line.** The top usually names the error type. The bottom is usually the immediate cause. The middle is usually not useful.
2. **Find your own filename.** Scan the trace for a file that belongs to your project rather than a library. That line is almost always where to look.
3. **Search the exact message.** Paste the specific error text, not your description of it, into a search or into Claude Code. Exact text matters here.

### Three kinds of failure

These have different causes. Telling them apart is most of early debugging.

- **It did not run at all.** Usually an environment problem: a missing dependency, wrong version, or wrong directory. Not related to the code itself.
- **It ran and crashed.** Usually a real error in the code. The message will usually point near it.
- **It ran and did the wrong thing.** The most difficult kind, because nothing reports a problem. This is the kind your tools produce most often. It is why Module 3 exists.

> **SAY WHICH KIND BEFORE YOU ASK FOR HELP**
>
> Opening with "it ran but the total is wrong" rather than "it's broken" changes how quickly anyone can help you. It also shows that you have already thought about the problem.

### Reading a diff

A diff shows what changed: removed lines marked with a minus, added lines with a plus, unchanged lines for context. VS Code's source control panel shows this with highlighting. Start with VS Code if the terminal is unfamiliar.

Practice until you can look at a diff and describe what changed in plain language, without reading the code aloud. That translation is the skill.

> **READ BEFORE YOU ACCEPT**
>
> When your tool proposes a change, read the diff before accepting it. Do this every time, including when the change looks obviously correct. This habit is what separates someone using the tool from someone accepting whatever the tool produces.

### Reading a file tree

Open the starter repository in VS Code and look at the folder structure. Guess what each folder is for. Then open files and check whether you were correct. Naming conventions are consistent across projects. This skill develops faster than you might expect.

You are not trying to understand the code. You are building a sense of where things are, so when someone says "it's in the components folder" you know what they mean.

---

## 1.10 Secrets and environments

Short item. One absolute rule. This is the highest-risk item in the module.

### What a secret is

- **API key** A string that proves an application is authorized to use a service. Anyone who holds it can act as that application and spend its money.
- **Credential** Anything that grants access: passwords, tokens, connection strings, private keys.
- **.env** A file holding these values, kept out of the repository. Code reads from this file so the values never appear in the code itself.
- **.gitignore** The file that keeps .env out of Git. Check that it lists .env before you commit anything to a new project.

> A client's credentials never go into a repository, a screenshot, a chat message, or a prompt.

The prompt is where people forget this rule. It is also where you will feel the most temptation. Pasting a config file into your tool to ask what is wrong with it feels harmless. If that file contains a live key, you have given a client's credentials to a place they should not be.

> **BEFORE PASTING ANYTHING, SCAN IT**
>
> Config files, error logs, and connection strings are the usual sources. Look for anything that looks like a long random string. If you are not certain, replace it with the word REDACTED before pasting. You lose nothing by doing this.

### If you leak one

This happens, including to experienced engineers. What matters is the next ten minutes.

1. **Tell someone immediately.** Your mentor, then the client lead. Speed matters more than composure.
2. **Do not quietly delete it.** Deleting a commit does not remove it from the history. Deleting the message does not un-send it. The key must be rotated. Only someone with access can do that.
3. **Do not investigate alone.** Trying to assess the damage yourself uses time during the window when rotation actually helps.

> **THIS IS NEVER A DISCIPLINARY MATTER WHEN REPORTED FAST**
>
> It becomes one when it is concealed. A leaked key reported in five minutes is an inconvenience. The same key reported in five days is an incident.

---

## 1.11 Assessment: explain your own build

Book 15 minutes with your mentor. This is the gate out of Module 1.

### The task

> Explain the starter repository's architecture out loud, in under three minutes, without using the words "it" or "the thing".

The word restriction is not arbitrary. Vague pronouns hide imprecise understanding. Forcing yourself to name each part shows immediately which parts you cannot name. Imprecision here predicts imprecision in front of a client. This is why it is the assessment.

### What to cover

- [ ] The four layers, and which parts of this project are in each
- [ ] What runs when you type `npm run dev`
- [ ] Where you would look first if a button stopped working
- [ ] Which parts came from the default stack and why the studio chose them
- [ ] One thing about this project you do not understand yet, named specifically

> **THE LAST ONE IS NOT A TRICK**
>
> Naming a specific gap is a stronger answer than claiming you understand everything. "I do not understand how the data gets from the form into storage" is a good answer. "I think I understand most of it" is not.

### How it is judged

| Level | What it sounds like |
|---|---|
| **Not yet** | Pronouns doing the work. Cannot say which layer a change would land in. Describes what the screen looks like rather than what the project is made of. |
| **Pass** | Names the parts. Can trace one action through the layers. Knows where to look first. Names a specific gap. |
| **Strong** | All of the above, plus a sense of what would be low cost to change and what would be high cost, and why. |

A "not yet" result means you return to item 1.7 and try again in a few days. This carries no penalty and is common on the first attempt.

---
---

# Module 2: AI-Assisted Building

Weeks 2 to 3. Thirteen items.

Items 2.1 to 2.10 are required. Items 2.11 and 2.12 are electives, chosen by specialty and by engagement requirements.

**Prerequisite:** everything in Module 1 working on your machine.

---

## 2.1 Where this module sits

This module has a governing document, and it is not this module.

> **INSERT: THE AI EXCELLENCE PLAYBOOK**
>
> The playbook is the authority for how we use these tools. The items below describe mechanics that build on the playbook. When an item and the playbook disagree, **the playbook wins**. Tell your mentor so the item can be corrected.

The split is deliberate. Principles are stable. Tool mechanics change every few months. Keeping them in separate documents means mechanics can be updated without re-examining the principles.

### What you will be able to do by the end

- Write a brief before you build, and recognize when you have skipped that step
- Tell scaffolding from iteration, and stop going back and forth between them
- Work inside the studio's guardrails, and request changes to them rather than overriding them
- Read a plan before any code is written
- Connect Figma directly to your build tool
- Review generated output rather than accepting it

### What this module is not

This is not a prompting course. Prompt phrasing matters much less than the three habits this module teaches: brief before build, plan before execute, read before accept. These three habits provide most of the value.

---

## 2.2 Spec before build

You already do this. This item transfers a habit you have, not installs a new one.

You would not open Figma and start placing high-fidelity components without knowing what the screen is for. The equivalent here is writing a short brief before you generate anything.

### What a brief contains

- **What this screen or feature is for.** One sentence.
- **Who uses it.** The actual role, not "the user."
- **What happens on success.** Where does the person end up.
- **What happens on failure.** What if the input is wrong, the network is down, the list is empty.
- **The question this build answers.** State A only, from Module 0. If you cannot name it, stop.

Keep it short. Half a page at most. This is a brief, not a specification document.

### Why this matters more than it sounds

Your tool builds the wrong thing quickly and confidently. It cannot know that you meant something different from what you wrote. It will not stop to ask if your description is clear enough.

The brief is where you find your own ambiguity, before it becomes code you must read, evaluate, and discard.

### Weak brief

> "Build a booking screen for dispatchers."

The tool will produce something. You will not be able to say whether it is correct, because you never defined what correct means.

### Working brief

> "A screen where a dispatcher assigns an available driver to an incoming job.
>
> Used by dispatchers, who handle approximately 40 of these per hour and know the drivers by name.
>
> Success: the job shows as assigned and disappears from the incoming list.
>
> Failure: if no driver is available, say so clearly and let them save the job rather than losing it.
>
> Question this answers: does assigning by name work better than assigning by proximity?"

Same length, approximately. The second one is buildable. It is also *checkable*.

> **THE TEST FOR A BRIEF**
>
> Could someone else read this and tell whether what got built matches it? If not, it is not a brief yet. It is a wish.

---

## 2.3 Working the loop

Three related habits. Together they prevent most wasted time.

### Two modes of prompting

Knowing which mode you are in prevents the most common source of wasted time.

| | Scaffolding | Iteration |
|---|---|---|
| **Goal** | Get a structure working | Change one thing without disturbing everything else |
| **Scope** | Broad. Whole screens, whole flows. | Narrow. Name the file, name the behavior. |
| **Expect** | To discard a large amount of it | To keep it |
| **Failure mode** | Adjusting details before the structure exists | Vague requests that cause unintended changes |

The most costly mistake: iterating while still in scaffolding. Adjusting spacing on a layout you are about to replace is wasted work. It also feels like progress, which is why it is easy to do for an hour.

### Restart versus patch

When output is approximately correct, patch it. When it is structurally incorrect, delete it and write a better brief.

Designers tend to patch too much. Deleting generated work feels wasteful, because deleting your own work is wasteful. This reasoning does not apply to generated work: the cost was minutes. A bad foundation that you keep patching costs more than a clean second attempt.

> **THE SIGNAL TO RESTART**
>
> You have asked for three corrections and each one has introduced a new problem. This is not a situation for patching. Delete it, identify what your brief did not say, and start again.

### Context is a resource

Long sessions produce lower-quality output. Your tool holds an increasingly large and cluttered conversation, and output quality decreases.

- Start a new session for a genuinely new task rather than continuing an exhausted one.
- Clear context when you change direction significantly.
- If answers become vague or repetitive, start a new session. This is the signal, not a reason to add more explanation.

### Commit before you start something big

From Module 1: being able to undo is what makes trying new things safe. Before a large scaffolding pass, commit. Then a bad outcome costs you one command instead of undoing many changes manually.

---

## 2.4 The rules that do not bend

Five rules. All of them appear elsewhere in this program. This is the one place they sit together.

1. **The 30 minute rule.** Stuck for 30 minutes, escalate. This prevents spending a day on something that arrives at a working result for reasons nobody understands.
2. **Never paste client data or credentials into a prompt.** From item 1.10. Repeated here because this is where the temptation is strongest.
3. **Never override a guardrail locally.** Request a change instead. Item 2.6 covers why.
4. **Read the diff before accepting.** Every time. Item 2.10.
5. **Always know which state you are in.** Discovery build or production work, from Module 0. The tool does not know and will not ask.

> **WHY A FENCE AND NOT GUIDELINES**
>
> These are the same shape as the never-alone list in item 0.4, for the same reason. A rule you evaluate every time is a rule you will eventually get wrong when you are tired and close to finishing. A rule you simply do not cross costs nothing to hold.

---

## 2.5 Claude Code: your working session

The shape of a normal working session, so you have a starting point.

### Starting

```
cd ~/projects/your-project
claude
```

The working directory matters. Your tool works with the project you started it in. Starting from the wrong folder is a common early confusion. The symptoms look like your tool being unhelpful rather than a location problem.

### The loop

1. **Describe what you want,** using the brief from item 2.2.
2. **Ask for a plan** and read it before anything is written. Item 2.7.
3. **Approve, or reject and write a new brief.** Rejecting costs seconds.
4. **Read the diff.** Item 2.10.
5. **Commit** when something works, even partially.

Everything else in this module is a refinement of these five steps.

### Worth knowing early

| Command | What it does |
|---|---|
| `/clear` | Reset the conversation context. Use when changing direction. |
| `/help` | List available commands. |
| `claude doctor` | Diagnose installation and configuration problems. |
| `Ctrl + C` | Stop what is currently running. |

### CLI or extension

Both, as installed in item 1.5. The CLI is where the work happens. The extension is better for one thing: reading a diff with syntax highlighting rather than as plain text.

Use the extension while the terminal is unfamiliar. Work primarily in the CLI by the end of this module. The reason is not preference. It is that the rest of the studio uses the CLI, and shared tools make it possible for others to help you.

---

## 2.6 Guardrails: CLAUDE.md and project rules

A `CLAUDE.md` file sits in a project and is read at the start of every session. It provides standing instructions: conventions, the default stack, required practices, prohibited practices.

Engineering maintains this file. It exists so every person and every session working in that repository behaves consistently, without each person needing to remember or negotiate the conventions.

### What is usually in it

- The default stack and version constraints
- Naming and file structure conventions
- Which patterns to use for common things, and which to avoid
- Commands for running, testing, and building the project
- Anything learned from previous problems

### The rule

> **Request additions. Do not override locally.**

If a guardrail blocks legitimate work, say so and get it changed. Do not quietly edit or ignore it on your machine.

> **THE FAILURE THIS PREVENTS**
>
> A local override is not visible to anyone else. Your work now follows a convention nobody knows about. It looks like a mistake to the next person who reads it. The protection the guardrail provided is gone, and the person who set it up does not know.

Reading this file is worth 10 minutes on any project you are new to. It is the fastest available summary of how a codebase expects to be treated.

---

## 2.7 Plan before execute

The most valuable habit in this module. It maps directly onto how you already work.

You do not go from a brief to a finished screen. You sketch, you look at it, you adjust, and only then do you invest in the detailed version. Asking for a plan is the same step.

### How it works

Ask for a plan before any code is written. Read it. Then approve it, or reject it and write a new brief.

### What to look for in a plan

1. **Is it solving the problem I described,** or a related problem that was easier to solve?
2. **Is it touching more than it should?** A plan that mentions files unrelated to your request is a warning. In a client repository this is a blast radius question from item 0.4.
3. **Has it added requirements I did not ask for?** Additions you did not request are common, plausible, and will need maintaining.
4. **Are there assumptions I should correct?** This is where your tool shows you what it understood from your brief.
5. **Does the order make sense to me?** If you cannot follow the sequence, you will not be able to evaluate the result.

### Rejecting is free

A plan costs seconds to produce and seconds to reject. Code costs you the time to read it, evaluate it, and undo it. This gap is why this habit provides value.

> **THE INSTINCT TO BUILD**
>
> The temptation is to skip the plan when the task seems obvious. Obvious tasks are exactly where your tool most often solves a related problem instead, because nothing in your brief constrained it. Skip the plan only when the change is genuinely one line.

---

## 2.8 Permissions and blast radius

Your tool asks before doing certain things. You can make these permissions wider or narrower. The correct setting depends entirely on which state you are in.

### The principle

> Permissiveness should be inversely proportional to blast radius.

| | Scratch discovery build | Client repository |
|---|---|---|
| **Blast radius** | Zero. Nothing depends on it. | Potentially everything. |
| **Reasonable stance** | Permissive. Speed is the point. | Conservative. Approve deliberately. |
| **Cost of a mistake** | Minutes | A release, a regression, a client conversation |

The same tool, the same person, two correct answers. This is the two-state model from Module 0 in a practical setting.

### Never blanket-approve

Regardless of state, read these before they run:

- Anything that deletes
- Anything that pushes to a remote
- Anything touching data or a database
- Anything installing or changing dependencies in a client repository
- Anything reaching outside the project directory

> **THE HABIT WORTH BUILDING**
>
> Approving everything automatically in a client repository is the fastest way to cause the invisible regression from item 0.3. The five seconds saved per approval is not worth the eleven days before a support ticket identifies the problem.

---

## 2.9 MCP servers, starting with Figma

MCP is a method for giving your tool access to other systems: your design files, your project tracker, your documentation.

This item matters more for you than for an engineer learning the same tool, because one of these connections is what makes this role possible for a designer.

### Figma first

Connecting Figma means your tool can read your design source directly. You do not need to describe your own design in text and hope the description is accurate.

This is what makes a forward-deployed designer faster than an engineer working from a design handoff. You are not translating between two formats. You are building from the source.

Practical results:

- Reference frames and components directly rather than describing them
- Design tokens carry through instead of being approximated
- Changes in the design file are visible to the build without a re-description step

### Other studio servers

Your mentor will explain which other servers are connected and what each one does. Ask what a server can access before you use it.

> **A CONNECTED SERVER IS A PERMISSION**
>
> Connecting a system means your tool can read from it, and in some cases write to it. In a client context, this is a question about where data goes. It belongs on the never-alone list. Ask before connecting anything that belongs to a client.

---

## 2.10 Reviewing what it wrote

The last required item. The bridge into Module 3.

Read the diff before accepting it. Do this every time, including when it looks obviously correct, and especially when you are nearly finished.

### What you are looking for

1. **Does it do what I asked?** Compare against your brief, not against your memory of your brief.
2. **Does it do more than I asked?** Extra changes are common, not exceptional. Each one is something you now own.
3. **Did it touch files I did not expect?** This is the clearest warning sign and the easiest to see.
4. **Do I understand every change?** If not, ask for an explanation. Then check the explanation against the code.

### The specific risk

From item 1.9: the most difficult failure is code that runs and does the wrong thing, because nothing reports a problem. Generated code is particularly good at producing this failure. It is fluent, plausibly structured, and confident.

> Your tool produces output that looks correct faster than you can determine whether it is correct. This gap is the main risk in this role. Reading the diff is the only habit that closes it.

### When you cannot follow a change

Ask for an explanation or ask for a simpler approach. A change you cannot read is a change you cannot verify. A change you cannot verify should not go in front of a client.

This is not a problem to apologize for. It is the correct response. Module 3 will assess you on this behavior.

---

## 2.11 Codex literacy

**Elective.** Take this if you work in client environments that use it, or if you want a second tool for difficult problems.

Same principles as items 2.2 through 2.10. Different interface.

### What to cover with your mentor

- CLI and IDE extension install and authentication
- The project instruction file convention, and how it maps to `CLAUDE.md` from item 2.6
- Where the working loop differs: the approval model, how tasks are delegated, how results come back
- When to use it instead of Claude Code
- When running both on the same problem is genuinely useful, and when it is just avoiding a decision

> **CURRENT SPECIFICS COME FROM YOUR MENTOR**
>
> This tool changes quickly enough that anything written into a curriculum would be outdated within a quarter. The principles above are stable. The mechanics are not.

---

## 2.12 Open-source and local models

**Elective.** Take this if you work with clients who have data residency constraints, or on internal work where cost or offline capability matters.

### What to cover

- Running models locally: the common runtimes, and what hardware supports in practice
- Open-weight versus hosted, and what the capability difference looks like on real work
- Where it is genuinely useful: sensitive data that cannot leave a client's environment, high-volume repetitive tasks, offline work
- Deployment basics, if the studio offers this to clients: where it runs, who maintains it, what it costs

### The honest positioning

> A local model is for narrow, sensitive, or repetitive tasks. It is not a substitute for your primary tool in the main build loop of a client engagement.

This is the key point. A person can finish this elective and still believe a local model replaces the primary tool. That belief is wrong. They will produce slower, lower-quality work and think they are being resourceful.

The correct understanding: this is a tool for a specific constraint, usually a data constraint. When the constraint is real, it is the only option. When it is not, it is a disadvantage.

---

## 2.13 Assessment: rebuild a Figma flow

One working day. This is the gate out of Module 2.

### The task

> Take an existing Figma flow — one you or a colleague has already designed — and rebuild it as a working discovery build in one day.

Your mentor will agree the flow with you beforehand. Choose something with at least three screens and one form.

### What you hand in

1. **The running build.** It starts with a documented command and is clickable.
2. **The brief you wrote first.** From item 2.2, written before you started, not written afterward.
3. **The faked list.** Everything fictional in the build: hardcoded data, mocked sign-in, buttons that go nowhere. This is a preview of Module 5. The point is to build the habit of recording fictions as you create them, not trying to remember them later.

### How it is judged

| Level | What it looks like |
|---|---|
| **Not yet** | Does not run, or runs but cannot be explained. No brief, or a brief written afterward. Faked list missing or incomplete. |
| **Pass** | Runs. You can explain what the code does and why it is structured that way. Brief written first and visibly matching what got built. Faked list complete. |
| **Strong** | All of the above, plus evidence of the loop: a restart where patching was not working, a plan you rejected, a place where the brief was incorrect and you noticed. |

### What is not being judged

Polish. Visual fidelity. Whether it looks finished.

A build that runs, is understood, and has its fictions recorded is better than a more polished one you cannot account for. This ordering is deliberate. Module 3 applies it more strictly.

> **THE ONE THING THAT FAILS THIS AUTOMATICALLY**
>
> A build you cannot explain. Not "I do not understand every line" — that is normal. But "I do not know why this is here." If that is true of any significant part of what you hand in, you accepted output without reading it. That is the one habit this module exists to prevent.

---

*End of Modules 0 to 2.*
