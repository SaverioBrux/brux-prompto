# Prompt templates and reusable blocks

Pick the smallest template that fits. Fill only the blocks the stakes justify and delete
the rest. A bracket may stay only for what the user alone knows (the subject, their
data): say so in the intro. Never leave any other template bracket unfilled.

The templates are in English. Write the final prompt in the user's language, translating
the labels and keeping them consistent within one prompt (see SKILL.md, "Language").

Contents: Light · Medium · Full (interactive) · Process block for unattended runs · Project-memory block ·
Final-report block · Research block · Coding lines · Deepening prompt · Premortem prompt ·
Second-critic prompt · Interview kickoff · Prior-art block · Skill line · Plan-only prompt · Handoff brief · Orchestrator block ·
Debug: symptom to fix

## Light

```text
[Objective in one sentence]. Output: [format/length]. Constraints: [1-2 concrete constraints].
```

## Medium (default)

```text
Objective: [real outcome / decision to make].

Context:
- [audience and purpose, and why it matters]
- [constraints, each with its reason]
- [data or material to work from; for a build, "Start from:" what already exists]

Output: [format, length, level].
[If shape or tone matters: "Example of a good result:" followed by the marked examples]

Done when:
- [testable criterion]
- [testable criterion]

Before delivering, compare the output with the criteria. Flag assumptions or weak points in
at most two lines after the output, outside any length limit set above.
```

For a prompt that will run on Claude Opus 5, leave that last line out (see
`claude-notes.md`, "Self-check lines"). When the target model is unknown, keep it.

## Full: interactive (Heavy, with the user present)

For long source material, paste it at the top under a clear label and keep the request
at the end.

```text
[MATERIAL: documents, data, examples of good results, each under its own label]

I want to work on: [topic/project].

Objective:
[the real outcome or the decision to make, and what should happen next]

Context:
- [relevant fact/constraint, with its reason]
- [audience / end user]
- [what is out of scope, and why]

Environment and material:
- Start from what exists: [projects, libraries, SDKs or products to reuse, with links]
- Work on: [raw data, files, systems, connectors available]
- Tools to use: [expert methods and instruments, e.g. databases, statistical models]
- References: [examples of good results, earlier work]

Desired output:
- format: [markdown / table / code / …]
- length and level: [...]

Process:
1. If essential context is missing, ask me first (one question at a time).
2. Proceed in small, verifiable parts.
3. Have me confirm the key decisions explicitly instead of settling them silently.

Done when:
- [testable criterion 1]
- [testable criterion 2]

Verification:
- [external signal: tests, unused data, comparison with history, the real system]
- [if useful: review by a second model or a fresh session, against the criteria above]
- Report as "done" or "verified" only what a real result has shown; tell me plainly
  what you could not verify.

Limits:
- You can do on your own: [routine, reversible actions]
- Ask me before: [irreversible actions, actions visible to others, important choices]
- Never do: [true absolutes only, each with its reason]
```

## Process block: unattended / long agent run

Replace the "Process" block of the full template with this when nobody will be watching.
Always pair it with the Final-report block and an "Ask me before" line; in a Medium
prompt, add all three at the end.

```text
Process (autonomous work):
- Carry the task through to the end: don't stop to list what remains or offer to
  continue when you can go on by yourself.
- Faced with ordinary obstacles (errors, timeouts, empty results, tools that fail),
  diagnose first, then retry or change route with the access you have.
- Stop only if a decision of mine is really needed, if you find a block put there on
  purpose (a file not to touch, access denied deliberately), or before the actions
  listed under "Ask me before". If nobody can answer during the run, skip those actions
  and decisions, finish everything else, and list them in the final report for me.
- Every so often, write one line on where you are.
- Close with a final report that stands on its own.
```

## Project-memory block

Add to prompts for an agent connected to a project folder when the work spans several
sessions (see SKILL.md, "Project memory"). Use `AGENTS.md` instead of `CLAUDE.md` for
non-Claude agents, and there replace the @STATUS.md sentence with "read STATUS.md at the
start of every session". If the project already has these files, the prompt says to read
and update them and keeps only the rules they lack. For a scheduled prompt sent again at every run, drop
the sentence about copying the rules from this message: the message comes back each time.

```text
Project memory (every session starts from zero: only what is written in these files
remains).
- CLAUDE.md, what stays true: what the project is and its goal, the rules, how to
  verify, the "done" criteria, what needs my confirmation, and these memory rules. Copy
  them there from this message in the first session: this message will not be there
  next time. Keep it short. If it already exists, update it without overwriting it. It must contain, on
  a line of its own and without quotes or backticks, the text @STATUS.md: that way the
  status is loaded automatically.
- STATUS.md, what changes: date · where we are · done · in progress · next steps (the
  first one doable without me) · decisions with their reason and rejected options with
  why · open questions · known problems. Rewrite it to the current state at every
  milestone and before ending the session, with exact names, numbers and paths. It must
  stay readable in one minute.
- At the start of a session, check that STATUS.md matches the real files. If it
  doesn't, correct it and tell me.
- If the decisions become many, move the old ones to DECISIONS.md with the date. A
  changed decision is a new entry that marks the old one as superseded.
```

## Final-report block

Add when the result of a long run will be read by someone who didn't follow the work.

```text
Final report:
Write for an intelligent reader who has not seen your work. Put the conclusions in the
first lines. Use plain words and complete sentences, with no abbreviations or names
invented during the work. Report: what you found, what you did, what you verified and
how, what remains open.
```

## Research block

Add to prompts whose core is finding out something.

```text
Research method:
Develop several competing hypotheses instead of confirming the first one. Check every
important claim against several independent sources and cite only sources you actually
consulted. For each conclusion, say how sure you are and what would change it.
```

## Coding lines

Optional single lines; add only the ones that match what the user wants.

```text
- Make the changes, don't just suggest them.   [or: Only propose, change nothing.]
- Write a general solution, not one that only makes the tests pass; if a test is wrong
  or the task is not feasible, tell me instead of working around it.
- Stay within the requested scope: no refactoring or extra features nobody asked for.
```

For ownership wording on Claude, see `claude-notes.md`.

## Deepening prompt

For when the user wants the target model to do the Depth step itself.

```text
I want a deeper version of this task, not a bigger one. Before rewriting it:
1) tell me what a top professional would do here that I am not asking for;
2) say which original material they would start from (raw data, source documents),
   rather than the summaries I usually work from;
3) name the specific methods and instruments they would use;
4) say what, outside you and me, would show that the result is correct.
Then rewrite my request so that it asks for exactly this.
```

## Premortem prompt

A cheap red-team pass on a plan, a spec or a draft.

```text
Imagine that six months from now this [plan / document / project] has turned out to be
a failure. Work backward to the most likely causes, from the most serious to the least.
For each, name the signal that would have revealed it early and the smallest change
that prevents it. Then tell me which two changes you would make right away.
```

## Second-critic prompt

To run in a fresh session or on a different model, pasting the output and the criteria.

```text
You are the independent reviewer of this work; you did not produce it.
Criteria it had to meet: [paste the "Done when" criteria]
Work to review: [paste]
For each criterion, say whether it is met, with the exact passage that shows or disproves it.
Then list the factual errors, the unsupported claims and what is missing.
Do not rewrite the work: give me only the findings, from the most serious to the least.
```

## Interview kickoff

For when the user wants the target model to run the interview.

```text
Help me turn this idea into a clear spec before executing.

Proceed like this:
1. identify the real objective (which decision it should help me make);
2. ask me targeted questions if context is missing, one at a time;
3. if the idea contains several independent pieces, propose how to split it and start
   from the first;
4. propose 2-3 approaches with pros and cons and the one you recommend;
5. write a small, verifiable spec, with "done" criteria and an external check, and ask
   me to confirm it;
6. only then, produce the output.

Idea:
[paste here]
```

## Prior-art block

Put it as the first phase of any build prompt when the existing landscape was not
checked before writing (see SKILL.md, Step 3). When it was checked, replace it with the
concrete list: "Start from: [project, link] for [part]; build from scratch only [part]".

```text
Before building anything, look at what already exists:
- official material: SDK, API, documentation, announced changes;
- open-source projects (GitHub and similar): libraries, community SDKs, demo apps; for
  each, note the licence and the date of the last update;
- the community (Reddit, Discord, forums): what works, what breaks, what is missing;
- products and apps that already do this job, including paid ones.

Report a short list with links: what each one does, what state it is in, where it stops.
Then propose three routes (reuse, extend or combine, build from scratch only the
uncovered part) with the one you recommend and why. Wait for my choice before building.
```

For unattended runs, replace the last sentence with: "Choose the route that reaches the
objective with the least new work, write in one line why, and go on." For a recurring
prompt, add: "Do this survey only at the first run and save it in the project files;
later runs read it."

## Skill line

Add to any Medium or Heavy prompt that runs on an agent able to install things.

```text
Use the skills already installed when they help. If you think a new skill or tool would
help, tell me which and why, but ask me before installing anything: I want to have it
checked first.
```

## Plan-only prompt

First half of the plan/execute split. Run it on the strongest model available.

```text
Objective: a step-by-step plan for [objective]. Do not build anything yet.

Context:
- What I already have: [material, systems, work done]
- What I want at the end: [result, and how I will know it worked]
- Limits: [budget, deadline, what must not be touched, each with its reason]

Propose 2-3 routes with pros and cons and the one you recommend. Have me confirm the key
decisions. If you lack context, ask me questions before planning.
```

## Handoff brief

Fill it from the conversation, following the rules in SKILL.md ("Handoff brief"). Delete
the parts that are empty. The closing lines are for the receiver. Keep them for an agent
that works alone; for a chat where the user reads each reply, drop the second and third
bullets of section 8.

```text
HANDOFF BRIEF: [name of the work]
The reader has not seen the previous conversation: everything needed is here.

1. Objective
[one sentence]
Done when: [the checks I will use to say it worked]

2. Decided
- [final decision]; why: [reason in a few words]
Rejected: [option]; why: [reason]

3. Facts
[exact names, numbers, dates, links and file names the work depends on]

4. Already done
[what has been completed, so it isn't redone]

5. Ask me before
[action]; why: [reason]

6. Open
[only what is truly still undecided]

7. Step list
[ ] [first step, doable without me]
[ ] [step]

8. How to work
- If you have access to files or connected apps, before acting open the ones that may
  matter, even if this brief doesn't name them.
- Follow the list and tick each step. Don't close by announcing the next step: do it.
  Don't offer to continue: continue.
- Stop only for what is under "Ask me before" or for a decision only I can make.
- Don't reopen what is under "Decided". If you find something that contradicts it, tell me.
- Close with a short recap: what you did, what you verified, what comes next.
```

## Orchestrator block

Only for agent harnesses with subagents, and only when the user wants one session to plan
and delegate. Mention the cost when offering it.

```text
Act as the director of the work. The plan, the architecture and the checks are yours.

Work on two tracks: getting the task done, and improving the environment so the next
task goes better (written rules, automatic checks, missing data and access). When you
notice a possible improvement, propose it.

Split the work into independent tasks and give each to a subagent, with a complete
brief: objective, "done" criteria, material, limits.
Pass context through pointers (files, notes, project pages) instead of rewriting it in
messages: what is already written somewhere should not be duplicated.
Delegate only what is truly separable: do yourself what needs the whole context.

When a subagent delivers, check the result against the criteria before assigning the
next task; if it doesn't meet them, send it back saying what is missing.
Every so often, reread how a task went, especially the ones that went badly, and turn
what you learn into a written rule or a check.

Handle on your own everything that doesn't need me. Stop only for a decision of mine.

Objective: [objective]
```

## Debug: symptom to fix

When the user brings a prompt and a result that disappointed, match the symptom:

| Symptom | Likely cause | Patch |
|---|---|---|
| Generic, could-be-anyone output | no context, no examples, digested inputs | add audience and purpose, real examples, rawer material |
| Answered the wrong question (a summary when actions were needed) | the request names an activity, not the result wanted | state the result and its shape (who, what, by when) as the objective |
| Right content, wrong shape | format described vaguely | definition of done + an example of the shape |
| Sounds expert, isn't | persona without method | name instruments, data and the external check |
| Confident but wrong or invented | nothing to verify against | external signal, grounded-claims line, sources to cite |
| Stops halfway, offers to continue | unattended task with interactive framing | the unattended Process block above |
| Asks permission for everything | vague or piled-up cautions, absolute "never" rules | name steps that need no approval, narrow the absolutes |
| Did suggestions instead of the work | action not named | "make the changes", not "can you suggest" |
| Over-built, added things nobody asked | scope left open | state scope and what is out of scope, with the reason |
| Ignored part of the brief | prompt too long or contradictory | cut, resolve the conflict, request at the end |
| Built from zero something that already exists | no look at prior art | "Already exists" scan, or the prior-art block as first phase |
| New chat redid or contradicted earlier work | context lost between sessions | handoff brief with decisions, reasons and what is done |
| Each new agent session starts lost, re-explores the folder | no memory on disk | project-memory block: instructions file + status file |
| Too timid, only safe tweaks | small target, fear of failing | bigger target framed as solvable, permission to fail, existence proof |

If none fits, ask for the one thing the user expected and didn't get, and add that as an
explicit criterion.
