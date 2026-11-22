---
name: brux-prompto
description: 'Write copy-paste-ready prompts for AI models and agents. Use when the user asks for a prompt, system prompt, spec or brief to give to an AI (a chat, a coding agent, another model, an agent); wants an existing prompt improved; asks why a prompt gave a poor result; wants a handoff brief so a new chat, another model or an agent can continue the work; or explicitly asks to aim higher with AI on a task (Altitude, Depth, Range, sized to the stakes). Typical triggers: "write me a prompt for", "help me prompt this", "improve this prompt", "why did this prompt fail", "turn this idea into a spec for an AI", "how should I ask the model to", "kickoff prompt", "write a brief to continue in another chat", "hand this off to another chat or agent", "raise the bar", "think bigger with AI", in any language. Do not use when the user wants the task itself done (write the email, summarise, fix the code), for briefs addressed to people, or when "more ambitious" is not about AI. The output is a prompt, not the finished task.'
license: MIT
metadata:
  author: SaverioBrux
  version: "1.0.0"
---

# Brux Prompto

Two moves, in order: first decide **what** to ask for (ambition), then **how** to ask
for it (spec). The stakes decide how much of the first move happens.

The deliverable is **a prompt**, not the finished task: one self-contained block the
user can copy into a fresh conversation or hand to an agent. For bigger tasks it is
preceded by a short **ambition map** that lets the user choose how high to aim.

Reference files, read only when needed:
- `references/templates.md`: all prompt templates, reusable blocks and the Debug table. Read it before
  compiling any Medium or Heavy prompt, and in Improve, Debug and Handoff modes.
- `references/ambition.md`: the moves for Altitude, Depth and Range. Read it before
  building an ambition map or applying escalations; the map template is at its end.
- `references/executors.md`: skills and tools that can carry out the prompt, and how to
  brief each. Read it when the task is Medium or Heavy.
- `references/toolkits.md`: the user's own vetted stack by domain: libraries, skills,
  quality criteria and checks. It ships as a template with one example; the user fills
  it in. Read it for Medium and Heavy requests; for a Light one take at most one rule
  from it (see its "How to use").
- `references/claude-notes.md`: behaviour notes for current Claude models (dated). Read
  it when the prompt will run on Claude and the task is Heavy, agentic or unattended.
- `references/examples.md`: one worked example per mode and weight. Read it when
  unsure how much to produce, and always in Improve, Debug and Handoff modes.

**Language.** Templates, labels and examples here are in English. Write to the user, and
write the prompt, in the language the user writes in, translating the labels ("Done
when", "Start from", "Already exists" and the rest). Use another language for the prompt
only if the user asks or the receiving system clearly needs it.

## Pick the mode

- **New prompt** (default): the user has an idea or a task. Follow Steps 0-3, then the
  two moves.
- **Improve:** the user pastes a prompt that already exists. Weigh the task (Step 0)
  to size the result, apply Step 1's rules on target and missing facts, skip Steps 2-3,
  and keep what works in the original: diagnose it against the craft rules and
  self-review checklist below, then return the
  improved prompt plus a three-line list of what changed and why. Offer the ambition
  move in one line if the task is Medium or Heavy, never the full map: the user already
  chose what to ask for. Build the map only if they accept the offer.
- **Debug:** the user pastes a prompt and a disappointing result. Name the likely
  failure, then patch the prompt (see "Debug: symptom to fix" in the templates). Patch only
  the cause behind the symptom, even if that takes more than one block, plus a testable
  "done" if missing; name other weaknesses in one line, unapplied, so the user learns
  which change mattered.
- **Handoff:** work or planning already happened in this conversation and the user
  wants to continue it elsewhere (a new chat, a cheaper model, an agent).
  Skip the steps below and go to "Handoff brief".

## Step 0: Right-size, then pick the path

Weigh the task first. This is the gate between the two moves.

| Weight | Examples | Ambition | Spec |
|---|---|---|---|
| **Light** | a tweet, a quick email, a rename, a one-off lookup | skip | one line: objective, output, 1-2 constraints |
| **Medium** | a document, an analysis, a landing page, a normal coding task | offer it in one line | medium template |
| **Heavy** | recurring work, multi-step builds, agent workflows, anything feeding a decision, financial/legal, irreversible | full ambition map | full template |

Two overrides: if the user explicitly asks to be more ambitious, go up one level (a Light
task gets a Medium prompt with up to three escalations applied and named in one line each
after it; a Medium task gets the map); if the task is purely creative and the process is
the point, skip ambition.

A strong tell for Heavy: there will be a meeting to discuss the output. A one-off document
someone else approves (a policy, a proposal) is Medium; it turns Heavy when it recurs,
triggers something irreversible or will be discussed in a meeting. Recurring alone is not
enough: a short text reused each time stays Medium with the Persist lines; recurring work
that analyses, decides or runs an agent is Heavy.
Money alone is not enough either: a one-off comparison or calculation the user can check
is Medium; it turns Heavy when the decision binds for years or the amount is large for them.

If in doubt, default to Medium.

## Step 1: Real objective, target, scope

**Objective.** Turn "do X" into "achieve Y" or "decide Z":

- **What decision should this output help you make?**
- **What should happen once this is done? What is the goal beyond the goal?**

**Target.** Know where the prompt will run, because it changes the spec:

- a chat (no tools, a human reading each reply), an agent with tools and files, or a
  different model altogether;
- **interactive** (the user is there to answer and approve) or **unattended** (a long
  run nobody watches);
- **one session or many:** an agent connected to a project folder (Claude Code, Cowork
  and similar) on work that will span several sessions needs project memory written
  into the prompt (see "Project memory").

Infer it when obvious; otherwise assume an interactive chat and say so.

**Scope.** If the request bundles several independent pieces ("a platform with chat,
billing and analytics"), say so before refining details: split it, order the pieces,
and write the prompt for the first one. Small, compartmentalised specs are easier to
verify and drift less than one giant brief. Cut what the goal doesn't need.

### Interview only if needed

- **Vague idea:** ask **one question per turn**, using tappable options when the
  answers can be enumerated. Priority: objective, audience, output format, hard
  constraints, available data and tools, stakes.
- **Clear request:** skip the interview and state assumptions inline.
- **Facts only the user has** (their company, their data): don't guess them. In a prompt
  for an interactive agent, make asking for them its first step; in a reusable prompt,
  leave a labelled bracket. Ask the user yourself only if the answer changes the weight
  or the route.
- **Numbers you pick** to make a criterion testable (a length, a threshold) are
  assumptions: name them to the user, next to the prompt. Give the user's constraints
  no reasons they did not state.

Bias toward drafting. If you are 80% sure, draft and let the user correct. Stop asking as
soon as you can draft something useful; a stated assumption beats a fifth question.

## Step 2: Environment check

Before aiming high, check what the model will actually be able to reach: raw data or
only summaries, tools, connectors, the ability to run code, install software and verify
its own work. Ambition is capped by this. Often the most valuable line in the whole
output is "to reach this level you first need to connect X". Never invent access the
user hasn't mentioned; state the assumption.

For Light tasks this step is implicit; skip it.

## Step 3: What already exists (anything that gets built or extended)

A prompt that builds from zero something that already exists wastes the whole run. When
the task is to build, extend or improve a product, tool, device, integration, automated
workflow or dataset, find out what is already there **before** writing the prompt. Skip
this for pure writing or analysis of the user's own material, and for Light tasks. When
comparing what exists is itself the task, leave it to the prompt: at most give it a
starting list marked "to be verified". For a
vague build idea, scan first, then ask the one question that remains.

Look first at what the user already has (the project folder and neighbouring projects,
when you can see them), then in `references/toolkits.md`: what is listed there is
already chosen and reviewed. If a project of the user's already covers the request, the
prompt continues that project from its files instead of starting a new one. **If you can
search now, do it** for what the kit doesn't cover (a few
targeted searches, not a research project):

- official material: SDK, API, documentation, the vendor's roadmap and changelog;
- open source: GitHub and similar (libraries, community SDKs, reverse-engineered
  protocols, demo apps, forks), noting licence and how recently each was updated;
- the community: Reddit, Discord, forums, where people say what works, what breaks and
  what they wish existed;
- finished products and apps that already do the job, including paid ones;
- for anything technical or scientific, papers and write-ups of earlier attempts.

For a Heavy task, show the user a short **"Already exists"** list (three to six items, each
with what it is, its state, and a link when you have one), inside the
ambition map when there is one. For a Medium one, skip the
list and write a "Start from:" line in the prompt. Either way, say which path you recommend:

1. **Reuse** something as it is;
2. **Extend** or combine existing pieces;
3. **Build** new, only for the part nobody has covered.

Default to the lowest number that reaches the goal, and say why when you go higher. The
prompt you then write names the specific pieces to start from.

**If you cannot search,** don't guess what exists. Make it the first phase of the prompt
instead, using the prior-art block in the templates: the executing model surveys what
exists, reports reuse / extend / build options, and waits for the user's choice (or, in
an unattended run, picks by stated criteria and records why). In a recurring prompt it
is a one-time setup step, recorded in the project files, not repeated at every run.

This step also sharpens the ambition move: what already exists is the baseline, so the
ambitious version starts where the existing solutions stop instead of redoing them, and
a working project found here is the best existence proof to show the model.

---

## Move 1: Ambition (Medium: one-line offer · Heavy: full map)

For Medium tasks, add one line after the spec: the single most valuable escalation and
an offer to apply it ("Want me to raise the bar? For example: …").

For Heavy tasks, build the map below before writing the spec.

### Four principles

1. **Methods, not vocabulary.** "Act like an expert" changes the model's words, not its
   process. Every escalation must name a concrete method, tool, data source or check.
2. **No escalation without an outside judge.** A harder goal judged only by the model
   produces confident fake success or metric gaming. Pair each escalation with a check
   that does not rest on the model's own opinion: a real result, a fresh session, or the
   user checking against a stated criterion (levers 1 and 2 under Verify, or the user). If none is
   feasible, lower that escalation and say why. The Medium one-line offer names its check.
3. **The environment caps ambition** (see Step 2).
4. **Self-efficacy hacks work on models too.** Frame hard targets as achievable and
   expected ("this is solvable, keep going"); show an existence proof when one exists;
   label explorations as experiments allowed to fail, so radical options get tried
   instead of only safe local tweaks. Always together with principle 2.

### The three axes

Read `references/ambition.md` before building a map; it has the moves for each axis.

- **Altitude: from task to outcome.** A ladder of about three rungs: understand
  instead of fill in, prepare the decisions, redesign the system the task belongs to.
  Driven by "what should happen next?" and "which past constraint does this process
  exist for?".
- **Depth: work as the best in the field do.** Expert instruments, the rawest
  material, an unreasonable target framed as reasonable, a belief tested against data,
  new knowledge validated on unseen data.
- **Range: bring in other fields.** Rewrite the deliverable as verbs, then assemble a
  crew in three groups (make it right, make it land, break it) and take each member's
  method, never the persona.

### Recommend

Pick **one** version: the most ambitious one that is reachable and verifiable now, often
a mix (e.g. Altitude rung 2 + one Depth move + the red team). Never push all three axes to
the maximum by default.

---

## Move 2: Spec (Spec · Verify · Environment)

Compile the chosen version into a prompt, using the templates in
`references/templates.md` (a Light task needs only the one line from Step 0). That file
also has optional blocks to offer when they fit: coding lines, a deepening prompt, a
premortem, a second-critic prompt, an interview kickoff.

- **Spec: the intent made unambiguous.** Objective, context, output format,
  constraints, and a **definition of done**: testable criteria fixed up front ("three
  sections, each ending with a recommendation", not "make it good"). For Heavy tasks,
  ask the model to surface key decisions for explicit confirmation instead of settling
  them silently.
- **Verify: how correctness gets checked.** Three levers, strongest first:
  1. **External signal:** tests, holdout data, backtesting on history, a benchmark, the
     real system's response, past examples of good output loaded as the standard.
  2. **A second critic:** a different model or a fresh session reviewing the output
     against the criteria, without the first one's context.
  3. **Self-review** against the criteria: fine for Light and Medium, not enough alone
     for Heavy.
  Also require grounded claims: the model reports something as done or checked only
  when a real result showed it, and says plainly what it could not verify. A number it
  computes is marked as computed, with its inputs, never credited to a source.
  When it counts or sorts items (reviews, tickets, emails), it numbers them and cites the
  numbers behind each count, in sentences as in tables. A position the user did not give
  is marked as a proposal.
- **Environment: the workshop.** Two halves: what the model can **reach** in this run
  (data, tools, references, guardrails) and what should **persist** so the workshop isn't
  rebuilt every time (see "Persist").

### Craft rules (apply while compiling)

1. **Explain the why.** A constraint with its reason generalises ("the text will be read
   aloud, so no bullet lists"); a bare rule gets applied literally or inconsistently.
2. **Say what to do, not only what to avoid.** "Write in flowing paragraphs" beats "no
   bullets". Positive instructions are testable.
3. **Show, don't describe.** When format or tone matters, include examples of good
   output (three to five when the user has them; one real one beats none), clearly
   marked as examples and varied enough not to be copied literally. Past good outputs
   are the best source; never invent "past" examples.
4. **Material first, request last.** With long documents or data, put the material at
   the top, separated from instructions by clear labels or tags, and the request at the
   end.
5. **Name the action.** "Suggest changes" gets suggestions; "make these changes" gets
   changes. Say which one is wanted.
6. **Guide, don't script the thinking.** State the goal, the criteria and the hard
   constraints; avoid a long step-by-step procedure for reasoning the model does better
   on its own. Prescribe steps only where order really matters.
7. **Ask for conclusions, evidence and assumptions, not a transcript of the reasoning.**
   Requests to write out the internal reasoning add noise and some models decline them.
8. **Be precise about approvals and absolutes.** List the specific actions that need
   confirmation and the routine ones that don't. Keep "never" for true absolutes, with
   scope and reason; where the user just wants control, write "ask before X".
9. **Self-contained.** The prompt must make sense to someone with zero context: no
   references to "the file from before" or to this conversation, and relative days
   ("Friday", "tomorrow") written as full dates; in a recurring prompt, as a period
   relative to the run ("the seven days before today"). Colleague test: could
   a smart colleague who knows nothing about the task follow it?
10. **Nothing heavier than needed.** Every block must earn its place; delete empty or
    decorative ones.

### Interactive or unattended

The same task needs a different Process block depending on the target (Step 1):

- **Interactive:** short checkpoints, key decisions confirmed by the user, questions
  allowed one at a time.
- **Unattended / long agent run:** checkpoints that wait for a human block the work.
  Instead: carry the task to completion, work through ordinary obstacles (errors,
  timeouts, empty results) by diagnosing and retrying, stop only for real blockers or
  the listed risky actions, give brief progress notes, and close with a report written
  for a reader who saw none of the work.

Both blocks are in the templates file.

### Name the executor (skills and tools)

This skill writes the prompt; other skills and tools are often the right ones to carry
it out. For a Medium or Heavy prompt, start from the kit in `references/toolkits.md`
when the domain is there, then check for other executors using the skills visible in
this environment and `references/executors.md`:

- a long goal with several independent workstreams, on an agent with subagents → an
  orchestration skill, or the orchestrator block from the templates;
- explaining how a mechanism works to people who need to *see* it → an interactive
  visual-explainer skill;
- a deliverable in a specific format (deck, document, spreadsheet, branded material) →
  the matching format or brand skill.

Rules:

- In the prompt, name only skills the user has installed and approved (kit skills with
  "if installed"). Anything else goes in a list after it, marked as needing review and
  install. On an agent that can install things, add the Skill line from the templates.
- The prompt must stand without the skill: it still states the objective, the definition
  of done and the verification. The skill is the "how", never a replacement for those.
- Apply that executor's briefing tips. If nothing fits, say nothing; don't invent one.

**Skill scout (Heavy tasks, or when the user asks).** When the project has a gap a skill
would fill, also look
for skills the user doesn't have yet. Follow "Finding new skills" in
`references/executors.md`. The limits that matter:

- search in this order: already installed, official sources, community;
- shortlist at most three, each with what it does, its source and why this project
  needs it, marked as to be verified; popularity is not safety;
- **never install on your own. Candidates are shown as "to be verified"; how to install
  one is given only after its safety review:** run the skill-inspection skill on each
  one the user picks, and drop anything it rejects. If no scanner is available, read the
  source yourself and say the check was lighter;
- the prompt names only installed, approved skills; candidates go in a list after it.

### Project memory (agent on a folder, work spanning sessions)

Every new session starts with an empty context. When the prompt will run on an agent
connected to a project folder and the work will not finish in one session, make the
agent keep its own memory on disk, as part of the task and not as an afterthought. This
holds for any project, not only code: a research dossier, a campaign, a book, a
migration. Skip it for one-shot tasks, where it is only overhead.

Add the project-memory block from the templates. It asks for two files with different
jobs, and the split is the point:

- **The instructions file** (`CLAUDE.md` on Claude Code and Cowork, `AGENTS.md` on other
  agents): what stays true. What the project is and its goal, the rules and conventions,
  how to run and check things, the definition of done, the guardrails. Short, because it
  is loaded in every session and long files are followed less well. If one already
  exists, the agent reads it and updates it; it never overwrites it.
- **The status file** (`STATUS.md`): what moves. Where the work stands, what is done,
  what is in progress, the next steps, decisions with their reasons and the options
  rejected, open questions, known problems. Updated at every milestone and before the
  session ends, **rewritten to the current state rather than appended to**, with a date.
  It follows the handoff rules: exact names and numbers, final versions only.

Three details make it work: the instructions file carries these memory rules and the
spec itself (objective, done criteria, verification, limits), because the kickoff prompt
is gone after the first session; it points to the status file
so it is read at the start of every session (on Claude Code, an import line on its own,
without quotes or backticks; see `references/claude-notes.md`); and at the start of a
session the agent checks the status against the real files before trusting it, since a
stale status is worse than none.

If the list of decisions grows long, move the old ones to a separate log
(`DECISIONS.md`) and keep in the status file only the ones still shaping the work. The
two files follow opposite rules: the status is rewritten to the present, the log is
history, so each entry is dated, and a changed decision gets a new dated entry that
marks the old one as superseded instead of editing it.

### Persist (recurring tasks only)

If the user will do this again, add two or three lines after the prompt on what to save
so the next run starts from a built workshop:

- standing rules and the verification plan in project instructions or a CLAUDE.md (the
  project-memory block already makes a folder agent write these);
- reference material in one known place (past good outputs, source data, glossary);
- the procedure as a reusable skill once it has worked twice;
- critical limits enforced at tool level (permissions, hooks), not only in a prompt.

Also suggest pruning old rules whose reason is gone: they make agents over-careful.

### Self-review before delivering

Read the draft as a hostile reviewer for ten seconds, then fix silently:

- **Size:** anything heavier than the task deserves?
- **Ambiguity:** can any requirement be read two ways? Pick one and make it explicit.
- **Verification:** external where the stakes need it?
- **End state:** are the done criteria testable ("under 120 words") or vague ("keep it short")?
- **Remnants:** any bracket the user need not fill, "TBD" or invented access left in?
  Any number you picked that is not named as an assumption?
- **Internal conflicts:** does any block fight another (a scope limit against "go beyond")?
- **Objective:** concrete, or decorative?

---

## Plan first, execute elsewhere (Heavy, optional)

Big jobs often go better and cost less in two sessions: the strongest model designs the
plan, then a fresh session (a cheaper model, or an agent) executes it. When execution
will be long, offer this split in one line: first a **plan-only prompt** from the
templates, then, once the plan is agreed, a **handoff brief** for the executing session.

A fresh session with a brief beats switching to a cheaper model mid-conversation: each
model has its own cache, so everything is reprocessed, and a lower-tier model cannot read
the stronger model's thinking.

Where the harness supports subagents, the same split can run in one session with the
orchestrator block from the templates. Mention the cost: workers can be most of the bill.

## Handoff brief

The receiver sees none of this conversation. The brief is everything it will know, so
the rules are stricter than for a normal prompt:

- **Copy, don't paraphrase,** the exact names, numbers, dates, links and file names.
  Write relative days ("Thursday", "today") as full dates.
- **Only the final version** of anything that changed along the way; no history of the
  discussion.
- **Add nothing that wasn't said or decided.** No new ideas, no new questions in the brief. If
  something essential is missing (above all how to tell the work succeeded), ask the
  user before writing the brief. If only part is missing (the success check stops short
  of the final state, a detail is undecided), write the brief, put the gap under "Open"
  and ask the one question after it.
- **Decisions carry their reason,** and every option dropped along the way is listed
  with why, so the receiver doesn't reopen them or rediscover the same dead ends. A
  reason nobody stated is written as "reason not stated", not reconstructed.
- **What is already done** is stated, so it isn't redone.
- **The first step is one the receiver can take without the user,** taken from what was
  already planned. If nothing planned qualifies: for an agent with file access, checking
  the facts in the brief; for a chat, preparing what the first planned step needs (a
  checklist, a draft) so the user only has to approve it.
- **As short as it can be while complete,** in one block to copy.

Use the handoff template in `references/templates.md`. Before delivering, check the
brief against the conversation line by line for anything invented, outdated or missing,
then tell the user in one line where to paste it and what to attach.

---

## Output format

Write in the user's language (see "Language" above). No essay around the output.
In every mode, Handoff included: if the prompt or brief has the user paste or attach data
about people (exports, transcripts, backups, tickets), add one line telling them to
remove or mask what the task does not need, or to use a tool approved for that data.

**Light and Medium:** a one-line intro, the prompt in a fenced code block, then, in this
order and only those that apply: the numbers you picked, the personal-data line, the
one-line ambition offer (Medium), the Persist lines (any weight, when the task recurs),
one line of options (run it here, tweak a block, make it heavier).

**Improve:** a one-line intro, the improved prompt, three lines on what changed and why,
the ambition offer when it applies. **Debug:** the likely failure in one line, the
patched prompt, what changed. For Improve, Debug and Heavy, close with one line on where
the prompt runs best (here, a fresh chat, an agent on the project folder) and an offer to
run it here when that fits. **Handoff:** the brief in one block, then one line on where to paste it
and what to attach.

**Heavy:** the ambition map, then the recommendation, then ask which version to compile
(tappable options when possible). Skip the map only when the user says so
("just the prompt", "now"); asking for a prompt is not enough. Then give three lines
(what you raised, its judge, the cost), the
"Already exists" list if Step 3 produced one, then the prompt: aim under 700 words by
dropping blocks that don't apply; for an agent, long rules can live in a file it reads. After the prompt, add as
needed: the candidate skills from the scout
("Suggested skills, to be verified before installing"), the Persist lines if the task
recurs, and one line of suggested settings (see `references/claude-notes.md`).

The ambition map template is at the end of `references/ambition.md`. Drop the sections
that add nothing for this task, and keep the map readable on a phone: about 300 words,
one line per rung or move.

## Completion criteria

Done when:
- the real objective (not just the task) is explicit, and the scope is one coherent piece;
- the level of ambition matches the stakes, and any escalation has an outside judge;
- for anything that gets built, what already exists has been checked (or the prompt
  makes that its first phase) and the reuse / extend / build choice is explicit;
- missing context is resolved or assumptions are stated;
- the definition of done is testable and the output format unambiguous;
- the Process block, where the prompt has one, matches the target (interactive or
  unattended);
- for multi-session work on a project folder, the prompt makes the agent keep the
  instructions file and the status file;
- environment, verification and limits are visible when the stakes justify them;
- the whole thing is self-contained, copy-paste-ready and no heavier than the task deserves.
