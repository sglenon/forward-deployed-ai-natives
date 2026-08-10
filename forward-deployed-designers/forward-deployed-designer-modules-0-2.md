# Forward Deployed Design
## Modules 0 to 2, consolidated

Master reference for the Forward Deployed Designer course. Each `##` heading is one LMS item.

Delivery is individual and self-paced. Items are in dependency order within each module.

**Source of truth note:** the LMS receives the HTML files in `lms-html/`, generated from `generators/`. This document is the readable master for review and editing. If you change copy here, the generators need the same change or the two will drift.

---
---

# Module 0: The Role and Its Edges

Half a day. Complete before touching a keyboard. Not skippable.

Everything in the rest of the program is a technique. This module is the judgment those techniques serve. Someone who skips it acquires the ability to build fast without the framework for knowing when not to.

---

## 0.1 Why this role exists

You already hold the half of this role that is hardest to teach. This module is about what gets added to it.

There is a role in software called the **forward-deployed engineer**. It started at Palantir, and the reasoning behind it is worth understanding because it applies almost perfectly to what we are doing here.

Palantir sold a data platform to organizations with genuinely complicated problems: banks, hospitals, government agencies. They found that the hard part was never the platform. The hard part was **translation**. Someone had to sit inside the customer's world, understand how their specific mess actually worked, and build the thing that solved it. That person could not be a salesperson, because they had to build. And they could not be a normal product engineer, because they had to be in the room where the problem lived.

The role has come back into fashion because AI labs hit the same wall. The models are general-purpose and enormously capable, and most organizations still cannot articulate what to do with them. The bottleneck is not capability. It is application.

> **THE PART PEOPLE GET WRONG**
>
> Forward-deployed does not mean "makes prototypes for clients." Palantir's forward-deployed engineers wrote code that customers ran in production. If the involvement stops at the demo, it is not this role. It is prototyping with a better job title.
>
> **Your work ships.** That is the whole distinction, and it is the reason the rest of this module is about discipline rather than technique.

### Our version of this bet is specific to you

The forward-deployed role has two halves.

1. **Technical breadth.** Enough range to build something end-to-end without waiting on anyone else's queue.
2. **Everything that is not code.** Reading a room. Finding the real problem behind a stated one. Knowing whose approval actually matters. Sensing when a client is nodding politely rather than agreeing.

The second half is much harder to teach. Most companies attempting this start with engineers and try to train the client instincts in. That is slow, and it often fails.

> **THE PREMISE OF THIS PROGRAM**
>
> You already have the second half. You have been in the room with clients for years. You know what a stalled conversation feels like, you know when a stakeholder is protecting territory, and you already work by making something the client can react to instead of asking them to imagine it.

What you are missing is the first half, and AI tooling has made that half dramatically cheaper to acquire than it was three years ago.

> You are not becoming an engineer. You are acquiring enough building capability to work inside a client's real system rather than alongside it.

---

## 0.2 The two states of your work

Because your work ships, one distinction carries the whole role. Get it wrong and everything downstream goes wrong with it.

> **Everything you build is in one of two states, and you always know which one. Moving between them is a decision someone signs off on, never something that just happens.**

| | State A: Discovery build | State B: Production work |
|---|---|---|
| **Purpose** | Answer a question | Improve something people actually use |
| **Lifespan** | Days | Indefinite |
| **Fictions** | Required. Hardcoded data and fake sign-in are correct. | Defects. Every one is a bug with a delay on it. |
| **Bar** | Real enough to react to | Fits the system, breaks nothing, survives you leaving |
| **Success** | You learned something, including when the answer was no | It shipped and nothing regressed |

Notice that these are not two levels of quality. They are two different jobs with *opposite* rules. A hardcoded array is good craft in State A and a liability in State B. Spending a day on error handling is diligence in State B and waste in State A.

This is why "just build it properly the first time" is bad advice. Building a discovery artifact properly destroys the thing that made it worth building: its speed.

### Why State A needs framing that State B does not

Think about a wireframe. Grey boxes, placeholder text, no real content. And critically, **nobody has ever mistaken a wireframe for a finished design.** The incompleteness is legible. The social contract is automatic. You never had to explain it.

A working discovery build breaks that contract. It runs. Buttons respond. Screens transition. It behaves, to any non-technical person clicking through it, like software. Every visual signal that told your client "this is early" has been removed, and nothing has replaced it.

> **WHAT THIS MEANS**
>
> The framing that used to be free is now something you supply deliberately, every time you show State A work. That is not an addition to your job. It is the discipline the job runs on.

### What State A is allowed to answer

1. **Is this the right problem?** The client described a symptom. Building the obvious response reveals, quickly and cheaply, whether the obvious response actually helps.
2. **Does this flow make sense to the people who would use it?** Not to the client's executive sponsor. To the dispatcher, the nurse, the warehouse supervisor: whoever touches it daily.
3. **Is this roughly plausible to build?** Not "how long will it take." Whether the shape is sane, whether the data the client claims to have is really there in the form they described, whether the integration they are assuming exists actually exists.

Every discovery build has one of these written down before you start. If you cannot name the question, you are not in State A. You are just building.

### What a State A build is not

- **Not a foundation.** Nothing in it is designed to survive.
- **Not an estimate.** That it took three days says nothing about the real build. Often the opposite: the parts you skipped are the expensive parts.
- **Not a commitment.** Showing a client a feature is not agreeing to build it.
- **Not production, no matter how good it looks.** Especially not when it looks good.

### Promotion: the only legal way across

A discovery build can become production work. That is often the right outcome, and it may be why you built it. But it happens exactly one way:

1. **Someone decides.** A named person makes an explicit call that this is going into the real system. Not a client saying "great, let's use it." A decision, recorded.
2. **The fictions get listed.** Everything fake in the build is written down in the faked list from Module 5. You cannot replace what nobody catalogued.
3. **A hardening pass gets scoped.** Replacing the fictions is real work with real cost. It is scoped and agreed before anyone starts, not absorbed.

> **THE FAILURE THIS PREVENTS**
>
> The alternative to promotion is **drift**, and nobody announces drift. It happens when a client says "can you just tidy that up so we can start using it," and you say yes because it is a small thing, and it was a small thing, and four months later the fake sign-in is in front of real customers.

Every artifact, one state, always known. That is the whole rule.

---

## 0.3 The six ways this goes wrong

Every later module in this program exists to prevent one of these. Read them now, so the rest of the course arrives with a reason attached.

Four of the six are the same disease under different clothes: something moved between State A and State B without anyone deciding. They are tagged below.

### 01. The 80% illusion
`DRIFT IN THE CLIENT'S HEAD`

*A client watches you click through a working booking flow. Their face changes. They say, "This is great, so we're basically there?" You aren't there. The screens are the cheap part; the durable, secure, maintainable system underneath them is the expensive part, and none of it exists.*

**Why it happens.** Working software is an extremely strong signal of completeness, and there is no visual signal that conveys "and none of this is real." The client has silently promoted your State A build to State B without telling you, because nothing told them not to.

**What prevents it.** The framing you will write in item 0.5, plus the faked list in Module 5. This one will happen anyway. Managing it is ongoing, not something you solve once.

### 02. The confident wrong answer

*You build exactly what the client described, quickly and well. They're impressed. Six weeks later it turns out the actual constraint was a compliance requirement nobody mentioned, and the whole flow you designed is unusable.*

**Why it happens.** Speed makes it tempting to start building before discovery is finished. When you can produce something in two days, the pressure to skip the uncomfortable questions goes up, not down.

**What prevents it.** Module 4: symptom versus problem, and the discipline of naming your question before you build.

### 03. The accidental commitment

*Someone asks, casually, "roughly how long would the real version take?" You want to be helpful. You say "probably a couple of months?" That number is now in their head, in their notes, and in their board deck. Nobody will ever remember you said "probably."*

**Why it happens.** You are the person the client trusts and the person in the room. Both of those make you the natural target for questions you are not authorized to answer.

**What prevents it.** Item 0.4, rehearsed until the redirect is automatic.

### 04. The quiet promotion
`DRIFT IN THE ARTIFACT`

*The client liked the prototype so much they asked their own developer to "just finish it off." Nobody scoped a hardening pass. Nobody listed what was fake. Eight months later the system is unmaintainable, and it has our name on it.*

**Why it happens.** Promotion is the correct outcome for a good discovery build, so saying yes feels right. What went missing was not the yes. It was the decision, the faked list, and the scoped work to replace them.

**What prevents it.** Module 5. The faked list and the decision log exist precisely for this, and they are mandatory deliverables for exactly this reason.

### 05. Becoming the client's shadow engineer
`DRIFT IN THE RELATIONSHIP`

*You're trusted, responsive, and you can build things. Small requests start arriving directly to you. None individually seems worth raising. Six weeks on, you're doing unbilled production work for a client you were supposed to be running discovery with.*

**Why it happens.** It is flattering, it is gradual, and each individual request is genuinely small. Once you are capable of production work, the requests stop feeling out of scope, because technically you can do them.

**What prevents it.** Noticing early. If you are building something nobody scoped, that is a scope conversation, not a favor.

### 06. The invisible regression
`STATE B ONLY`

*You change a shared component to fix the spacing on one screen. It looks right. Three other screens you have never opened now have broken layouts, and you find out from a support ticket eleven days later.*

**Why it happens.** In State A, blast radius is zero, because nothing else depends on your work. In State B, everything might. The habits that made you fast in discovery are exactly the habits that cause this.

**What prevents it.** Module 3's production track. Knowing what depends on what before you touch it, and never treating a shared component as a local change.

---

## 0.4 Where your authority ends

You will be the most trusted person in the room, in the room, and visibly capable of changing the client's real system. That combination means questions will come to you that are not yours to answer.

There are five. Learn them.

### The never-alone list

1. **Timelines and cost.** Any duration, any number, any currency, including hedged ones. "Probably," "roughly" and "it shouldn't be too expensive" all lose their qualifiers in the retelling.
2. **Feasibility guarantees.** "Yes, we can do that" is a commitment. "That's a good question, let me get you a real answer" is not. The second one costs you nothing.
3. **Scope changes.** Anything not in the current agreement. Especially the small ones, because the small ones are how the large ones arrive.
4. **Promotion.** Declaring that a discovery build is going into the real system. This is never yours alone, no matter how ready it looks or how enthusiastic the client is.
5. **Blast radius.** Shared components, the design system, anything touching data, and anything live users can reach. If a change could affect a screen you have not opened, it is not a local decision.

### Why this list is short and absolute

Judgment calls are exhausting. A list you have to reason about every time is a list you will eventually get wrong under pressure, and the pressure is real, because the person asking is usually being friendly and you will feel rude deflecting.

So these five are not guidelines. They are a fence. You do not evaluate them, you just do not cross them alone. That is much easier to hold at 4pm on a Friday in a client's meeting room.

> **READ THIS TWICE**
>
> **Escalating is not admitting you couldn't handle something. It is a demonstrated senior behavior, and it is how you get promoted in this program.**
>
> Movement between levels requires evidence that you escalated something you could have gotten away with handling alone. That is not a formality. Someone who never escalates is not confident. They are someone whose mistakes have not surfaced yet.

### Your escalation paths

*Replace the placeholders below with real names before publishing this item. A path with a blank in it will not be used.*

| Question type | Goes to | How fast |
|---|---|---|
| Timeline, cost, scope, contract | *[senior client lead]* | Before you respond |
| Promoting a discovery build | *[senior client lead]* + *[engineer mentor]* | Before you agree |
| Blast radius: shared components, data, live users | *[engineer mentor]* | Before you build it |
| Technical feasibility | *[engineer mentor]* | Same day |
| Stuck for 30 minutes | *[engineer mentor]* | Immediately |
| Client relationship going sideways | *[senior client lead]* | Immediately |
| Something you cannot categorize | *[senior client lead]* | Immediately |

### The holding phrase

You need one sentence, memorized, that buys you time without sounding evasive. Something like:

> "That's exactly the right question, and I want to give you a real answer rather than a guess, so let me bring it back to the team and come to you with something solid."

Write your own version in your own voice. Say it out loud until it stops feeling awkward. You will use it more than any other sentence in this job.

---

## 0.5 The framing exercise

**Assessed.**

State B work mostly speaks for itself: it shipped or it did not. State A work is the one that needs language wrapped around it, because it looks finished and is not. So this exercise is about showing a discovery build.

> **YOUR TASK**
>
> Write the short piece you would say to a client at the moment you first show them a discovery build. Five or six sentences, in your voice, written to be said out loud.

Before you write, read these two.

### Version A (fails)

> "So just to set expectations before I show you this, it's only a prototype, so a lot of it doesn't actually work yet. The data isn't real and there's no proper login. We'd need to rebuild most of this properly before it could go anywhere near production, so please bear that in mind as you're looking at it."

Everything in Version A is true. It still fails.

It is apologetic, so it invites the client to discount work that was genuinely valuable. It lists limitations without ever saying what the thing is *for*. It leaves "how long until it's properly built" as the obvious next question. In fact it practically asks it on the client's behalf. And it positions you as slightly embarrassed, which is a strange note to hit while demonstrating something impressive.

### Version B (works)

> "What we've built answers one question: does this booking flow make sense to your dispatchers? Everything you can see is real enough to react to, and nothing behind it is real. The schedules are invented, and the sign-in is a shortcut. That's deliberate. We wanted to find out whether the flow is right before anyone spends money making it durable. So click around, and tell me where a dispatcher would get stuck."

Same artifact. Same limitations. Different conversation entirely.

It opens with the question, so the client knows what they are evaluating. It states the fictions plainly and immediately claims them as intentional. It gives the client a job, *tell me where someone would get stuck*, which is far more useful than "what do you think." And it frames durability as a separate, later, costed activity, which quietly defuses "so how close are we" before it is asked.

### What yours needs

- [ ] The question this build answers, in the first sentence
- [ ] What is fake, stated plainly and without apology
- [ ] Why it is fake, framed as a decision rather than a limitation
- [ ] A specific job for the client to do while clicking
- [ ] No numbers, no durations, no guarantees
- [ ] Nothing that could be heard as agreeing to promote it

> **THE TEST**
>
> Read your version out loud, to yourself. That is not optional: this is copy meant to be spoken, and problems that are invisible on the page are obvious the moment you hear them.
>
> If it sounds like a disclaimer, rewrite it. If it sounds like an invitation, you are done. Bring the final version to your mentor.

---

## 0.6 Close

Three things to carry into Module 1.

1. **You already have the hard half.** The building capability you are about to acquire is real, and it is less rare than what you already do. Client instinct is the scarce thing.
2. **Always know which state you are in.** Discovery build or production work. If you cannot say which one without thinking, stop and find out. Everything else in this program assumes you know.
3. **Speed is only an advantage if the work is trustworthy.** Producing something impressive quickly is worth nothing if nobody can tell whether it is right. That is why Module 3 exists, and why it is the module you cannot skip. It is also the gate to being allowed near a client's real system.

> **BEFORE MODULE 1**
>
> Bring your laptop, your admin password, and three hours of patience. Setup is the least glamorous part of this program and the one that most determines whether the rest of it works.

---
---

# Module 1: Technical Literacy Floor

Weeks 1 to 2. Eleven items, in dependency order.

---

## 1.1 What this module is for

This module does not teach you to write code. It teaches you to read it, reason about it, and talk about it without bluffing.

That distinction matters more than it used to. Your tooling writes the code now, and it writes it faster than any untrained person can evaluate. The gap between *producing* output and *knowing whether the output is right* is the single largest risk in this role.

> Everything in this module exists to put a floor under that gap.

### What you are building toward

- A machine you set up yourself and can fix when it breaks
- Enough vocabulary to follow an engineer's explanation without nodding blankly
- The ability to read an error, a diff, and a file tree
- One absolute rule about client credentials that you never break

The final item is the assessment: explaining your own build out loud to an engineer in under three minutes. Everything before it is preparation for that.

### How to work through this

Items are in dependency order. Item 1.3 assumes 1.2 worked. Do not skip ahead, and do not move on from a broken step, because every later failure will trace back to it and be much harder to diagnose.

> **THE 30 MINUTE RULE STARTS NOW**
>
> Stuck for half an hour on any single step, stop and message your engineer mentor. This is not a last resort, it is the expected behaviour. Environment problems are individual and unpredictable, and someone who has seen the error before will usually recognise it in seconds.

Expect this module to feel less rewarding than the rest of the program. Setup is the least glamorous part and the one that most determines whether everything after it works.

---

## 1.2 Your terminal and editor

Two tools, installed together, because the useful thing is how they talk to each other.

### First: which track are you on

Everything in this program assumes a Linux-style environment. On a Mac you already have one. On Windows you install one.

**Windows.** Install WSL2 with Ubuntu, and from that point on do **all** project work inside the Ubuntu terminal. Not PowerShell, not Command Prompt.

```
wsl --install -d Ubuntu
```
*(PowerShell, as Administrator)*

Reboot when prompted, then open Ubuntu from the Start menu and create your Linux username and password.

**macOS.** Open Terminal from Applications, Utilities. You already have what you need. If prompted to install the Xcode Command Line Tools at any point during this module, accept. It supplies several tools the later steps assume.

> **WINDOWS: THE ONE MISTAKE TO AVOID**
>
> Mixing PowerShell and Ubuntu is the most common source of confusion in this module. Commands that work in one fail in the other, files appear to be missing when they are simply elsewhere, and the error messages do not tell you that is what happened. If a step is not working, check which terminal you are in before anything else.

### What a terminal actually is

A prompt waiting for a command, plus a sense of where it currently is in your file system. That location is the **working directory**, and most confusion for new users comes from not knowing where they are.

Start with these. They are enough for weeks.

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
> There is no recycle bin. `rm` removes a file and it is gone. Read the whole command before pressing enter, every time, and be especially careful with anything containing `-rf`.

### Survival mechanics

These will save you more time than any command in the list above.

| Key or flag | What it does |
|---|---|
| `Tab` | Autocomplete a file or folder name. Use it constantly; it also confirms the thing exists. |
| `Up arrow` | Recall previous commands. Faster and less error-prone than retyping. |
| `Ctrl + C` | Stop whatever is running. Your escape hatch. |
| `--version` | Append to almost any tool to check it is installed and which version. |
| `which name` | Show which copy of a tool is actually running. Answers "why is it using the wrong version?" |

One thing worth learning to notice: when a command finishes, you get your prompt back. If you do not have a prompt, something is still running or waiting for input from you. That single observation resolves a surprising number of "it froze" moments.

### VS Code

Install VS Code from the official site, then open it once and find four things: the file explorer, the integrated terminal, the source control panel, and the extensions panel. You will use all four daily.

Install these extensions now:

- **Remote – WSL** (Windows only). Without it, VS Code and your terminal disagree about where your files are.
- **Prettier**, for consistent code formatting.
- Whatever else the starter repo recommends when you open it later.

The link between the two tools is one command. From a terminal, inside a project folder:

```
code .
```

Windows: run this from your Ubuntu terminal, not PowerShell. VS Code will reopen in WSL mode, which is what you want.

---

## 1.3 Node and Python

Two runtimes. Install both through a version manager, never directly, and the reason is worth ten minutes of your attention.

### Why version managers exist

Different projects need different versions of the same runtime. A client repo from last year may need an older Node than the one a new project wants. If you install a single version directly, you eventually hit a project that will not run, and the error message will not say "wrong version." It will say something baffling about a module failing to load.

> **THIS IS THE MOST COMMON BREAKAGE IN THIS STACK**
>
> Version mismatch, usually Node against npm, is the single failure people in this program hit most often. A version manager makes it a thirty second fix instead of an afternoon.

### Node

Install `nvm` (Node Version Manager) first, following the install instructions on its official repository, then use it to install Node. On Windows, do this inside your Ubuntu terminal.

```
nvm install --lts
nvm use --lts
node --version
npm --version
```

Three ideas to hold on to:

- **npm** Node's package manager. It fetches the libraries a project depends on.
- **package.json** The project's list of dependencies and its available commands. When you want to know how to run something, look here first.
- **node_modules** Where the downloaded libraries live. Enormous, regenerable, and never committed to Git.

The two commands you will actually use daily:

| Command | What it does |
|---|---|
| `npm install` | Download everything this project depends on. Run once after cloning. |
| `npm run dev` | Start the project locally. The exact name comes from package.json. |

### Python

Install through `uv` or a version manager, following its official install instructions. Do not install packages into the system Python.

> **WHY THE SYSTEM PYTHON IS OFF LIMITS**
>
> On Mac and Linux, the Python that came with your machine belongs to the operating system. Other things depend on it. Modifying it breaks software that has nothing to do with your project, and the connection is not obvious when it happens.

The concept that matters is the **virtual environment**: an isolated set of packages belonging to one project. Every Python project gets its own, so projects cannot break each other.

The Python equivalents of `package.json` are `requirements.txt` or `pyproject.toml`. Same idea, different filename.

> **KEEP THIS PROPORTIONATE**
>
> Unless the studio default stack is Python-based, you need Python present and understood, not mastered. Install it, know what a virtual environment is, and move on.

---

## 1.4 Git and GitHub access

Install Git, prove to GitHub that your machine is yours, then clone your first repository.

### Install and identify yourself

Git usually ships with macOS and with Ubuntu. Check first, install only if missing, then tell it who you are. The name and email you set appear on every commit you make.

```
git --version

git config --global user.name "Your Name"
git config --global user.email "you@company.com"
```

### SSH keys

An SSH key is a matched pair of files. One half is public and you hand it out; the other half is private and never leaves your machine. GitHub keeps the public half and uses it to recognise you, which means you stop being asked to authenticate.

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

Copy that entire output, then paste it into GitHub under Settings, SSH and GPG keys, New SSH key.

> **THE FILE EXTENSION IS THE WHOLE POINT**
>
> The file ending in `.pub` is the public half, and it is the only one you ever copy anywhere. The file without an extension is private. If you are ever about to paste a key and you are not certain which one you have, stop and check.

Confirm it worked:

```
ssh -T git@github.com
```
*(expect a greeting with your username)*

The first connection asks you to confirm GitHub's fingerprint. Answering yes is correct here.

> **WHY BOTHER, WHEN TOKENS EXIST**
>
> You could use HTTPS with a personal access token instead. Keys are worth the fifteen minutes because they remove an authentication annoyance from every subsequent day, and because understanding the public and private halves is a concept you will meet again.

### Clone the starter repo

Your engineer mentor will give you the repository address. This is your first real exercise:

```
cd ~
mkdir projects
cd projects
git clone git@github.com:your-org/starter-repo.git
cd starter-repo
code .
```

Do not run it yet. That happens at the checkpoint in item 1.6.

---

## 1.5 Claude Code and Codex

The tools you will spend most of your working day inside.

### Claude Code

The native installer is the recommended method. It needs no Node.js, sets your PATH for you, and updates itself in the background.

```
curl -fsSL https://claude.ai/install.sh | bash
```
*(macOS, Linux, and WSL)*

> **WINDOWS USERS: RUN THIS INSIDE UBUNTU**
>
> Use your WSL terminal, not PowerShell. Claude Code should be installed and launched from the same Linux environment your projects live in, otherwise it will be looking at a different file system from the one you are working in.

Open a new terminal window afterwards so your shell picks up the PATH change, then confirm:

```
claude --version
claude doctor
```

`claude doctor` is worth remembering. It is the first thing to run when something is behaving strangely, and it will usually tell you what is wrong.

Run `claude` inside a project folder to start, and follow the prompts to authenticate with your studio account.

### Two surfaces, one tool

Install both the terminal version above and the VS Code extension from the marketplace.

| | The CLI | The VS Code extension |
|---|---|---|
| **What it is** | Claude Code in your terminal | The same tool, surfaced in your editor |
| **Use it for** | Everything. This is the primary working environment. | Reviewing changes visually, and as an on-ramp while the terminal still feels foreign |
| **Why** | Full capability, and the way the rest of the studio works | Seeing a diff highlighted is easier than reading it as text |

Start in whichever feels comfortable. Aim to be primarily in the CLI by the end of Module 2.

> **IF THE INSTALL COMMAND FAILS**
>
> Installation methods change. The current instructions live at **code.claude.com/docs/en/setup**. Check there before spending time debugging, then apply the 30 minute rule.

### Codex

**Optional.** Only install this if you are on the Codex elective track in Module 2, or if a client environment you work in has standardised on it.

Both a CLI and an IDE extension are available. Your engineer mentor will supply current install instructions, because this tool moves quickly enough that anything written here would date.

If you are not on that track, skip it. An unused tool on your machine is one more thing that can break.

---

## 1.6 Setup checkpoint

Prove the machine works before you go any further. Do not treat a partial pass as a pass.

Run each of these. Every one should print something sensible rather than an error or a blank line.

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
> If any line fails, that tool is either not installed or not on your PATH, and every later item that depends on it will fail in a way that looks unrelated. Fix it now, or escalate it now.

### The actual milestone

The seven checks above only prove things are installed. This next part proves they work together, and it is the real gate.

1. **Clone the starter repo.** You did this in item 1.4. Confirm you can still find it and open it with `code .`.
2. **Install its dependencies.** Run `npm install` and let it finish. It may take a few minutes and print a great deal of output. That is normal.
3. **Start it.** Run `npm run dev`. Look for a line in the output containing a local address, usually something like localhost followed by a port number.
4. **Open it in a browser.** Paste that address into your browser. Something should appear.

> That last step is the milestone. It is the first time you have made something run on your own machine, and everything else in this program builds on it.

### Before you move on

- [ ] All seven version checks pass
- [ ] The starter repo is cloned and opens in VS Code
- [ ] Dependencies installed without errors
- [ ] The project runs locally and you have seen it in a browser
- [ ] You know how to stop it again (`Ctrl + C`)

If any box is unticked, do not continue to item 1.7. Message your engineer mentor with the exact command you ran and the exact output you got, copied as text rather than described from memory.

---

## 1.7 How the pieces fit together

A mental model you can draw from memory, and the studio's default stack mapped onto it.

Almost every application you will touch has four layers. Knowing which layer a problem lives in is most of knowing who to ask and what it will cost to change.

1. **The browser.** What the user sees and clicks. Buttons, layouts, forms, the things you already design. Changes here are usually cheap and visible immediately.
2. **The application.** The logic. What happens when the button is pressed, what rules apply, what gets calculated. Changes here cost more and are invisible until something behaves differently.
3. **The data.** What is stored and how it is shaped. Changes here are the expensive ones, because existing data has to be migrated and mistakes are hard to reverse.
4. **Deployment.** Where it all runs so other people can reach it. Usually invisible until it breaks.

> **THE USEFUL INSTINCT**
>
> Cost of change rises as you go down that list. A client asking to move a button and a client asking to change what a record means sound similarly small in a meeting. They are not remotely similar. Recognising which one you are being asked for is a genuinely senior skill.

### Draw it

Sketch these four layers with arrows showing what talks to what. Do it from memory, check it, and redraw it until it is right. You will use this diagram in the assessment.

### The default stack

Your engineer mentor will walk you through what the studio picked for each layer, and more importantly *why*. Write the reasoning down, not just the names.

The reason the why matters: a designer who knows only the names can tell a client what we use. A designer who knows the reasoning is the one who notices when a client requirement quietly breaks an assumption the stack depends on. That noticing is the moment that needs escalating, and it is worth a great deal.

> **WHEN REQUIREMENTS ARE UNCLEAR, THE DEFAULT WINS**
>
> You will often start building before every requirement is settled. In that situation, use the default stack rather than choosing something. Deviating from it is a conversation with an engineer, not a preference you exercise alone.

---

## 1.8 Git vocabulary and the daily loop

The vocabulary matters as much as the commands, because it is what lets you follow an engineer's explanation instead of nodding blankly.

### The words

- **Repository (repo)** A project and its entire history.
- **Remote** A copy of the repo that lives elsewhere, usually on GitHub.
- **origin** The default name for your main remote.
- **Clone** Copy a remote repo down to your machine, history included.
- **Branch** A parallel line of work. Yours to break without affecting anyone.
- **main** The branch everyone agrees is the real one.
- **Staging area** The set of changes you have selected to go into your next commit.
- **Commit** A saved snapshot, with a message explaining why.
- **Push** Send your commits up to the remote.
- **Pull** Bring other people's commits down to you.
- **Pull request (PR)** A proposal to merge your branch into main, reviewable by others.
- **Merge** Combine one branch into another.
- **Merge conflict** Two people changed the same lines. Git stops and asks you to decide.
- **Revert** Undo. The most valuable word in this list.
- **Stash** Set your current changes aside temporarily without committing.
- **.gitignore** A list of files Git should never track, such as node_modules and .env.
- **HEAD** Where you currently are in the history.

### The daily loop

Five steps, repeated for every piece of work.

```
git checkout -b my-change     # branch
                              # ...make your changes...
git add .                     # stage
git commit -m "why, not what" # commit
git push -u origin my-change  # push, then open a PR on GitHub
```

On commit messages: the diff already shows what changed. The message should say why, so that someone reading it in four months understands the intent rather than re-deriving it.

### Revert is the load-bearing skill

> The confidence to experiment comes entirely from knowing you can get back.

This is the reason to learn Git properly rather than tolerating it. Once you are certain you can undo anything, you will try things you would otherwise be too cautious to attempt, and trying things is most of how this job works.

Practise it deliberately before you need it. Break something on a branch, commit the breakage, then get back to where you were. Do it twice.

### Two habits

1. **Commit small and often.** When you are generating a lot of code quickly, frequent commits are the difference between losing an hour and losing a day. Commit whenever something works, even partially.
2. **Meet a merge conflict on purpose.** Ask your mentor to walk you into one deliberately, so the first conflict you hit in real work is familiar rather than alarming. They look far worse than they are.

---

## 1.9 Reading, not writing

The core skill of this module. Your tools write; you read, and you decide whether what they wrote is right.

### Reading an error message

Errors look like walls of text. They are not. Most of that text is a stack trace, which is a list of what was happening when things went wrong, and most of it is code you did not write and do not need to read.

1. **Read the first line and the last line.** The top usually names the error type. The bottom is often the immediate cause. The middle is usually noise.
2. **Find your own filename.** Scan the trace for a file that belongs to your project rather than a library. That line is almost always where to look.
3. **Search the exact message.** Paste the specific error text, not your paraphrase of it, into a search or into Claude Code. Precision matters enormously here.

### Three kinds of failure

These have completely different causes, and telling them apart is most of early debugging.

- **It did not run at all** Usually environment: a missing dependency, wrong version, wrong directory. Nothing to do with the code itself.
- **It ran and crashed** Usually a real error in the code, and the message will normally point near it.
- **It ran and did the wrong thing** The hardest kind, because nothing reports a problem. This is the one your tooling produces most often, and the reason Module 3 exists.

> **SAY WHICH KIND BEFORE YOU ASK FOR HELP**
>
> Opening with "it ran but the total is wrong" rather than "it's broken" changes how quickly anyone can help you, and it demonstrates that you have already thought about it.

### Reading a diff

A diff shows what changed: removed lines marked with a minus, added lines with a plus, unchanged lines for context. VS Code's source control panel shows this visually and is easier to start with than the terminal.

Practise until you can look at a diff and say out loud what changed, in plain language, without reading the code aloud. That translation is the skill.

> **READ BEFORE YOU ACCEPT**
>
> When your tooling proposes a change, read the diff before accepting it. Every time, including when it looks obviously fine. This habit is what separates someone using the tool from someone being used by it.

### Reading a file tree

Open the starter repo in VS Code and look at the folder structure. Guess what each folder is for, then open files and check whether you were right. Naming conventions are fairly consistent across projects, so this generalises faster than you would expect.

You are not trying to understand the code. You are building a sense of where things live, so that when someone says "it's in the components folder" you know what they mean.

---

## 1.10 Secrets and environments

Short item, one absolute rule. This is the highest-stakes thing in the module.

### What a secret is

- **API key** A string that proves an application is allowed to use a service. Anyone holding it can act as that application, and spend its money.
- **Credential** Anything granting access: passwords, tokens, connection strings, private keys.
- **.env** A file holding these values, kept out of the repo. Code reads from it so the values never appear in the code itself.
- **.gitignore** The file that keeps .env out of Git. Check it lists .env before you commit anything to a new project.

> A client's credentials never go into a repository, a screenshot, a chat message, or a prompt.

The prompt is the one people forget, and it is the one you will be most tempted by. Pasting a config file into your tooling to ask what is wrong with it feels harmless. If that file contains a live key, you have just handed a client's credentials somewhere they should not be.

> **BEFORE PASTING ANYTHING, SCAN IT**
>
> Config files, error logs, and connection strings are the usual carriers. Look for anything that resembles a long random string. If you are unsure, replace it with the word REDACTED before pasting. Nothing is lost by doing this.

### If you leak one

It happens, including to experienced engineers. What matters is the next ten minutes.

1. **Tell someone immediately.** Your engineer mentor, then the client lead. Speed matters far more than composure.
2. **Do not quietly delete it.** Deleting a commit does not remove it from the history, and deleting the message does not un-send it. The key must be rotated, which only someone with access can do.
3. **Do not investigate alone.** Trying to assess the damage yourself costs time during the window when rotation actually helps.

> **THIS IS NEVER A DISCIPLINARY MATTER WHEN REPORTED FAST**
>
> It becomes one when it is concealed. A leaked key reported in five minutes is an inconvenience. The same key reported in five days is an incident.

---

## 1.11 Assessment: explain your own build

Book fifteen minutes with your engineer mentor. This is the gate out of Module 1.

### The task

> Explain the starter repo's architecture out loud, in under three minutes, without using the words "it" or "the thing".

The word restriction is not a gimmick. Vague pronouns are where imprecise understanding hides, and forcing yourself to name each part reveals immediately which parts you cannot name. Vagueness here predicts vagueness in front of a client, which is why this is the assessment.

### What to cover

- [ ] The four layers, and which parts of this project live in each
- [ ] What runs when you type `npm run dev`
- [ ] Where you would look first if a button stopped working
- [ ] Which parts came from the default stack and why the studio chose them
- [ ] One thing about this project you do not understand yet, named specifically

> **THE LAST ONE IS NOT A TRICK**
>
> Naming a specific gap is a stronger answer than pretending there are none. "I do not understand how the data gets from the form into storage" is a good answer. "I think I understand most of it" is not.

### How it is judged

| Level | What it sounds like |
|---|---|
| **Not yet** | Pronouns doing the work. Cannot say which layer a change would land in. Describes what the screen looks like rather than what the project is made of. |
| **Pass** | Names the parts. Can trace one action through the layers. Knows where to look first. Names a specific gap. |
| **Strong** | All of the above, plus a sense of what would be cheap to change and what would be expensive, and why. |

A "not yet" means you go back to item 1.7 and try again in a few days. It carries no penalty and is fairly common on the first attempt.

---
---

# Module 2: AI-Assisted Building

Weeks 2 to 3. Thirteen items.

Items 2.1 to 2.10 are required. Items 2.11 and 2.12 are electives, chosen by specialty and by what the engagement mix demands.

**Prerequisite:** everything in Module 1 working on your machine.

---

## 2.1 Where this module sits

This module has a governing document, and it is not this module.

> **INSERT: THE AI EXCELLENCE PLAYBOOK**
>
> The playbook is the authority for how we work with these tools. The items below are mechanics layered on top of it. Where an item and the playbook disagree, **the playbook wins**, and you should tell your mentor so the item gets corrected.

The split is deliberate. Principles are stable; tool mechanics change every few months. Keeping them in separate documents means the mechanics can be updated without anyone re-litigating the principles.

### What you will be able to do by the end

- Write a brief before you build, and recognise when you have skipped that step
- Tell scaffolding from iteration, and stop thrashing between them
- Work inside the studio's guardrails, and request changes to them rather than overriding them
- Read a plan critically before any code is written
- Connect Figma directly to your build tool
- Review generated output rather than accepting it

### What this module is not

It is not a prompting course. Prompt phrasing matters far less than the three habits this module actually drills: brief before build, plan before execute, read before accept. Those three carry almost all of the value.

---

## 2.2 Spec before build

You already do this. The whole point of this item is transferring a habit you have, not installing a new one.

You would not open Figma and start placing high-fidelity components without knowing what the screen is for. The equivalent discipline here is a short written brief before you generate anything.

### What a brief contains

- **What this screen or feature is for.** One sentence.
- **Who uses it.** The actual role, not "the user."
- **What happens on success.** Where does the person end up.
- **What happens on failure.** What if the input is wrong, the network is down, the list is empty.
- **The question this build answers.** State A only, from Module 0. If you cannot name it, stop.

Short. Half a page at most. This is a brief, not a specification document.

### Why this matters more than it sounds

Your tooling will build the wrong thing quickly and confidently. It has no way to know that you meant something different from what you said, and it will not stop to ask if your description is coherent enough to act on.

The brief is where you catch your own ambiguity, before it becomes code you then have to read, evaluate, and throw away.

### Weak brief

> "Build a booking screen for dispatchers."

The tool will produce something. You will not be able to say whether it is right, because you never said what right was.

### Working brief

> "A screen where a dispatcher assigns an available driver to an incoming job.
>
> Used by dispatchers, who handle maybe forty of these an hour and know the drivers by name.
>
> Success: the job shows as assigned and disappears from the incoming list.
>
> Failure: if no driver is available, say so clearly and let them park the job rather than losing it.
>
> Question this answers: does assigning by name work better than assigning by proximity?"

Same length, roughly. The second one is buildable, and more importantly it is *checkable*.

> **THE TEST FOR A BRIEF**
>
> Could someone else read this and tell whether what got built matches it? If not, it is not a brief yet, it is a wish.

---

## 2.3 Working the loop

Three related habits. Together they are most of the difference between a productive session and an afternoon of thrash.

### Two modes of prompting

Recognising which mode you are in prevents the most common form of wasted time.

| | Scaffolding | Iteration |
|---|---|---|
| **Goal** | Get a structure standing up | Change one thing without disturbing everything else |
| **Scope** | Broad. Whole screens, whole flows. | Narrow. Name the file, name the behaviour. |
| **Expect** | To throw a lot of it away | To keep it |
| **Failure mode** | Fiddling with details before the shape exists | Vague requests that cause collateral changes |

The mistake that costs the most: iterating while still in scaffolding. Adjusting spacing on a layout you are about to replace is wasted effort, and it feels like progress, which is why it is easy to do for an hour.

### Restart versus patch

When output is roughly right, patch it. When it is structurally wrong, delete it and re-prompt with a better brief.

Designers systematically over-patch. Deleting generated work feels wasteful, because deleting your own work is wasteful. This is a false transfer: the cost was minutes, and a bad foundation you keep patching costs far more than a clean second attempt.

> **THE SIGNAL TO RESTART**
>
> You have asked for three corrections and each one has introduced a new problem. That is not a patching situation. Delete it, work out what your brief failed to say, and start again.

### Context is a resource

Long sessions degrade. The tool is holding an increasingly large and increasingly cluttered conversation, and the quality of what it produces falls off.

- Start a fresh session for a genuinely new task rather than dragging an exhausted one forward.
- Clear context when you change direction significantly.
- If answers start feeling vague or repetitive, that is usually the signal, not a reason to explain yourself more forcefully.

### Commit before you start something big

From Module 1: revert is what makes experimentation safe. Before a large scaffolding pass, commit. Then a bad outcome costs you one command instead of an afternoon of manual undoing.

---

## 2.4 The rules that do not bend

Five. All of them appear elsewhere in the program; this is the single place they sit together.

1. **The 30 minute rule.** Stuck for half an hour, escalate. This prevents the failure where you burn a day and arrive at something that works for reasons nobody understands, including you.
2. **Never paste client data or credentials into a prompt.** From item 1.10. Restated here because this is where the temptation actually lives.
3. **Never override a guardrail locally.** Request a change instead. Item 2.6 covers why.
4. **Read the diff before accepting.** Every time. Item 2.10.
5. **Always know which state you are in.** Discovery build or production work, from Module 0. The tool does not know and will not ask.

> **WHY A FENCE AND NOT GUIDELINES**
>
> These are the same shape as the never-alone list in item 0.4, for the same reason. A rule you evaluate every time is a rule you eventually get wrong when you are tired and close to finished. A rule you simply do not cross costs nothing to hold.

---

## 2.5 Claude Code: your working session

The shape of a normal working session, so you have a default to depart from.

### Starting

```
cd ~/projects/your-project
claude
```

The working directory matters. The tool works with the project you started it in, so starting from the wrong folder is a common early confusion, and the symptoms look like the tool being unhelpful rather than misplaced.

### The loop

1. **Describe what you want,** using the brief from item 2.2.
2. **Ask for a plan** and read it before anything is written. Item 2.7.
3. **Approve, or reject and re-brief.** Rejecting costs seconds.
4. **Read the diff.** Item 2.10.
5. **Commit** when something works, even partially.

That is it. Everything else in this module is a refinement of these five steps.

### Worth knowing early

| Command | What it does |
|---|---|
| `/clear` | Reset the conversation context. Use when changing direction. |
| `/help` | List available commands. |
| `claude doctor` | Diagnose installation and configuration problems. |
| `Ctrl + C` | Stop what is currently running. |

### CLI or extension

Both, as installed in item 1.5. The CLI is where the work happens. The extension is genuinely better for one thing: reading a diff with syntax highlighting rather than as plain text.

Use the extension freely while the terminal still feels foreign, and aim to be primarily in the CLI by the end of this module. Not for purity, but because that is where the rest of the studio works, and shared tooling makes it possible for someone to help you.

---

## 2.6 Guardrails: CLAUDE.md and project rules

A `CLAUDE.md` file sits in a project and is read at the start of every session. It is standing instruction: conventions, the default stack, things to do, things never to do.

Engineering maintains it. It exists so that every person and every session working in that repo behaves consistently, without each individual having to remember or negotiate the conventions.

### What is usually in it

- The default stack and version constraints
- Naming and file structure conventions
- Which patterns to use for common things, and which to avoid
- Commands for running, testing, and building the project
- Anything previously learned the hard way

### The rule

> **Request additions. Do not override locally.**

If a guardrail is blocking legitimate work, say so and get it changed. What you must not do is quietly edit or ignore it on your machine.

> **THE FAILURE THIS PREVENTS**
>
> A local override is invisible to everyone else. Your work now follows a convention nobody knows about, and it looks like a mistake to the next person who reads it. Worse, whatever the guardrail was protecting against is now unprotected, and the person who put it there has no idea.

Reading the file is worth ten minutes on any project you are new to. It is the fastest available summary of how a codebase expects to be treated.

---

## 2.7 Plan before execute

The highest-leverage habit in this module, and the one that maps most directly onto how you already work.

You do not go from a brief to a finished screen. You wireframe, you look at it, you adjust, and only then do you commit effort to the detailed version. Asking for a plan is the same move.

### How it works

Ask for a plan before any code is written. Read it. Then approve it, or reject it and re-brief.

### What to look for in a plan

1. **Is it solving the problem I described,** or a nearby problem that was easier to solve?
2. **Is it touching more than it should?** A plan that mentions files unrelated to your request is a warning. In a client repo it is a blast radius question from item 0.4.
3. **Has it invented requirements?** Additions you did not ask for are common, plausible, and will need maintaining.
4. **Are there assumptions I should correct?** This is where the tool tells you what it thinks your ambiguous brief meant.
5. **Does the order make sense to me?** If you cannot follow the sequence, you will not be able to evaluate the result.

### Rejecting is free

A plan costs seconds to produce and seconds to reject. Code costs you the time to read it, evaluate it, and undo it. The asymmetry is enormous, and it is the entire reason this habit pays.

> **THE INSTINCT TO BUILD**
>
> The temptation is to skip the plan when the task feels obvious. Obvious tasks are exactly where the tool most often quietly solves something adjacent, because there was nothing in your brief to constrain it. Skip the plan when the change is genuinely one line, and not otherwise.

---

## 2.8 Permissions and blast radius

The tool asks before doing certain things. You can widen or narrow that, and the right setting depends entirely on which state you are in.

### The principle

> Permissiveness should scale inversely with blast radius.

| | Scratch discovery build | Client repository |
|---|---|---|
| **Blast radius** | Zero. Nothing depends on it. | Potentially everything. |
| **Reasonable stance** | Permissive. Speed is the point. | Conservative. Approve deliberately. |
| **Cost of a mistake** | Minutes | A release, a regression, a client conversation |

The same tool, the same person, and two correct answers. That is the two-state model from Module 0 showing up in a practical setting.

### Never blanket-approve

Regardless of state, some things get read before they run:

- Anything that deletes
- Anything that pushes to a remote
- Anything touching data or a database
- Anything installing or changing dependencies in a client repo
- Anything reaching outside the project directory

> **THE HABIT WORTH BUILDING**
>
> "Approve everything" in a client repo is the single fastest way to cause the invisible regression from item 0.3. The five seconds you save per approval is not worth the eleven days before a support ticket tells you what happened.

---

## 2.9 MCP servers, starting with Figma

MCP is a way to give your tooling access to other systems: your design files, your project tracker, your documentation.

This item matters more for you than for an engineer learning the same tool, because one of these connections is the specific thing that makes this role coherent for a designer.

### Figma first

Connecting Figma means the build tool can read your design source directly, instead of you describing your own design in prose and hoping the description survives translation.

That is the capability that makes a forward-deployed designer faster than an engineer working from a handoff. You are not translating between two representations. You are building from the source.

Practical implications:

- Reference frames and components directly rather than describing them
- Design tokens carry through instead of being approximated
- Changes in the design file are visible to the build without a re-explanation step

### Other studio servers

Your mentor will cover which others are connected and what each is for. Ask what a server can reach before you use it, not after.

> **A CONNECTED SERVER IS A PERMISSION**
>
> Connecting a system means your tooling can read from it, and in some cases write to it. In a client context, that is a question about what data is going where, and it belongs to the never-alone list. Ask before connecting anything of a client's.

---

## 2.10 Reviewing what it wrote

The last required item, and the bridge into Module 3.

Read the diff before accepting it. Every time, including when it looks obviously fine, and especially when you are nearly finished and want to be done.

### What you are looking for

1. **Does it do what I asked?** Compare against your brief, not against your memory of your brief.
2. **Does it do more than I asked?** Extra changes are the common case, not the exception. Each one is something you now own.
3. **Did it touch files I did not expect?** The clearest available warning sign, and the easiest to spot.
4. **Do I understand every change?** If not, ask for an explanation, then check the explanation against the code rather than accepting it.

### The specific risk

From item 1.9: the hardest failure is code that runs and does the wrong thing, because nothing reports a problem. Generated code is unusually good at producing exactly this. It is fluent, it is plausibly shaped, and it is confident.

> Your tooling produces output that looks correct faster than you can determine whether it is correct. That gap is the whole risk in this role, and reviewing the diff is the only habit that closes it.

### When you cannot follow a change

Say so, and ask for it to be explained or simplified. A change you cannot read is a change you cannot verify, and a change you cannot verify should not be in front of a client.

This is not a limitation to apologise for. It is the correct response, and it is the behaviour Module 3 will assess you on.

---

## 2.11 Codex literacy

**Elective.** Take this if you work in client environments that have standardised on it, or if you want a second opinion available on stubborn problems.

Same principles as items 2.2 through 2.10. Different surface.

### What to cover with your mentor

- CLI and IDE extension install and authentication
- The project instruction file convention, and how it maps to `CLAUDE.md` from item 2.6
- Where the working loop differs in practice: the approval model, how tasks are delegated, how results come back
- When to reach for it over Claude Code
- When running both on the same problem is genuinely useful, and when it is just indecision with extra steps

> **CURRENT SPECIFICS COME FROM YOUR MENTOR**
>
> This tool moves quickly enough that anything written into a curriculum would date within a quarter. The principles above are stable; the mechanics are not.

---

## 2.12 Open-source and local models

**Elective.** Take this if you work with clients who have data residency constraints, or on internal work where cost or offline capability matters.

### What to cover

- Running models locally: the common runtimes, and what hardware actually supports in practice rather than in principle
- Open-weight versus hosted, and what the capability gap looks like on real work rather than on a benchmark
- Where it genuinely helps: sensitive data that cannot leave a client's environment, high-volume repetitive tasks, offline work
- Deployment basics, if the studio offers this to clients: where it runs, who maintains it, what it costs

### The honest positioning

> A local model is for narrow, sensitive, or repetitive tasks. It is not a substitute for your primary tooling in the main build loop of a client engagement.

That is the lesson to leave with. Someone who finishes this elective believing they can swap a local model in for the primary build loop has learned the wrong thing, and will produce slower, worse work while believing they are being resourceful.

The right frame: this is a tool for a specific constraint, usually a data one. When the constraint is real, it is the only option. When it is not, it is a handicap.

---

## 2.13 Assessment: rebuild a Figma flow

One working day. This is the gate out of Module 2.

### The task

> Take an existing Figma flow, one you or a colleague has already designed, and rebuild it as a working discovery build in one day.

Your mentor will agree the flow with you beforehand. Pick something with at least three screens and one form.

### What you hand in

1. **The running build.** It should start with a documented command and be clickable.
2. **The brief you wrote first.** From item 2.2, written before you started, not reconstructed afterward.
3. **The faked list.** Everything fictional in the build: hardcoded data, mocked sign-in, buttons that go nowhere. This is a preview of Module 5, and the point is to build the habit of cataloguing fictions as you create them rather than trying to remember them later.

### How it is judged

| Level | What it looks like |
|---|---|
| **Not yet** | Does not run, or runs but cannot be explained. No brief, or a brief written afterwards. Faked list missing or incomplete. |
| **Pass** | Runs. You can explain what the code does and why it is structured that way. Brief written first and recognisably matching what got built. Faked list complete. |
| **Strong** | All of the above, plus evidence of the loop: a restart where patching was going nowhere, a plan you rejected, a place where the brief was wrong and you noticed. |

### What is not being judged

Polish. Visual fidelity. Whether it looks finished.

A build that runs, is understood, and has its fictions catalogued beats a more beautiful one you cannot account for. That ordering is deliberate, and it is the same ordering Module 3 will apply more strictly.

> **THE ONE THING THAT FAILS THIS AUTOMATICALLY**
>
> A build you cannot explain. Not "I do not understand every line," which is fine and normal, but "I do not know why this is here." If that is true of any significant part of what you hand in, you accepted output without reading it, and that is the one habit this module exists to prevent.

---

*End of Modules 0 to 2.*
