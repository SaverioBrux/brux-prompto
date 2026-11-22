# Notes for prompts that will run on Claude

**Checked: November 2026**, against Anthropic's "Prompting best practices" and "Prompting
Claude Fable 5.2" pages (platform.claude.com/docs, Prompt engineering section). Model
behaviour changes with every release: if this date is more than a few months old, or the
user names a newer model, check the current docs before relying on these notes. Nothing
here applies to non-Claude models.

Use these for agentic or unattended prompts of any weight, and for Heavy ones. Do not
paste them into other Light or Medium prompts.

## Settings line (outside the prompt)

When the user controls the effort level (API, Claude Code, some apps), suggest one in a
single line after the prompt:

- everyday knowledge work, chat, interactive coding: **medium**
- hard analysis, research, agentic work, long unattended runs: **high**
- above high only where a gain has been measured; it costs many more tokens

On Fable 5.2, instructions like "answer directly without deliberating" don't reduce
thinking at medium and above; lowering effort does. Effort barely changes reply length;
ask for length in the prompt.

## Choosing the model, and switching

- **Strongest model for the plan, a cheaper one for the execution.** The top-tier model
  uses plan limits or credits much faster; reserve it for design, hard analysis and the
  one big job, and hand routine execution to the tier below with a handoff brief. Which
  models and limits apply depends on the user's plan and changes often: ask or check, do
  not assume.
- **Prefer a new chat with a brief over switching model mid-chat.** After a switch the
  request is recomputed without the cache, because each model has its own. Moving down a
  tier (for example from Fable 5.2 to Opus 5.5, Sonnet 5.5 or Haiku 5.5) also drops the earlier
  model's thinking; moving up to Fable 5.2 keeps it. (Checked November 2026: Claude Code
  docs, "How Claude Code uses prompt caching"; platform docs, "Preserved thinking", table
  "Which model switches keep the reasoning". Changing effort mid-session restarts the
  cache on cloud platforms and gateways, not on current models with an API key or a
  Claude subscription; picking model and effort at the start avoids the question.)
- In Claude Code the split can run in one session: main model as orchestrator, a cheaper
  model for subagents. Use the orchestrator block from the templates.

## Project memory on Claude Code and Cowork

From the Claude Code memory docs (code.claude.com/docs/en/memory), checked November 2026:

- Each session starts with a fresh context window. `CLAUDE.md` is read at the start of
  every session, from the working directory and the directories above it. It is context,
  not enforcement: critical limits still belong in permissions or hooks.
- `CLAUDE.md` can import other files with `@path` (for example a line `@STATUS.md`);
  imported files are loaded at session start with it. The import must be written bare:
  inside quotes or backticks it is not imported. Every import costs context in every
  session, so the status file must stay short.
- Longer instruction files use more context and are followed less well (the docs aim
  for under 200 lines). Keep `CLAUDE.md`
  to what every session needs; move the rest to files read on demand.
- Claude Code also has **auto memory**: notes Claude writes for itself, loaded each
  session, stored on the local machine outside the project folder. It does not replace
  a status file in the folder, which the user can read, version and carry to another
  machine, tool or chat.
- Without a `CLAUDE.md`, recent versions fall back to `AGENTS.md`; a `CLAUDE.md` can
  also import `@AGENTS.md` to share one file with other agents.

## Behaviours worth prompting for

- **Stopping early on long tasks** (more often at low/medium effort): include the
  unattended Process block from the templates. Keep a human confirmation for risky or
  irreversible actions, because the model asks less often once told to keep going.
- **Approvals:** the model follows approval rules closely. A broad rule ("ask before
  sending messages to anyone") can freeze routine work. List the specific actions that
  need approval and the routine ones that don't. When approving mid-run, say exactly
  what is approved rather than "continue".
- **"Never" is read as absolute.** Use "ask before deleting files" when the user wants
  control rather than a ban.
- **Caution piles up.** Old cautions in memory, notes and instruction files make agents
  over-careful. Suggest deleting the ones whose reason is gone.
- **Silence during long runs:** ask for a line before starting, brief updates, and a
  closing recap that stands on its own.
- **Final reports:** include the final-report block; readers haven't seen the tool calls.
- **Style rules are followed literally.** A hard limit ("max 20 words per sentence") can
  make prose choppy. Prefer describing the reader and the purpose.
- **Code ownership (Fable 5.2):** if the user wants the model to improve structure as
  it works, say the codebase is the model's own to maintain; expect more changes and
  more tokens. If the user wants minimal changes, leave ownership out and state the
  scope.
- **Subagents:** delegation can dominate cost. Don't write standing "always delegate"
  instructions; say when delegation is worth it (independent, parallel work).
- **Self-check lines** ("before you finish, verify against the criteria") catch errors
  on most models, so keep the one line the Medium template has. Claude Opus 5 is the
  documented exception: it verifies by default and such lines make it over-verify, so
  leave the line out of prompts written for that model.
- **Examples:** the docs suggest three to five, varied, each wrapped in `<example>`
  tags so they are not mistaken for instructions.

## Things to keep out of the prompt

- **Requests to write out the reasoning** (step-by-step thinking in the answer, thinking
  tags): on current models these can be declined. Ask for conclusions, evidence and
  assumptions; rely on the model's built-in thinking.
- **Shouting** (CRITICAL, MUST, capitals): models from the 4.5 generation on follow the
  system prompt closely and over-trigger on it. Use plain wording with the reason.
- **Anti-laziness boilerplate** written for older models ("be thorough, use tools
  whenever in doubt"): it now causes over-exploration and over-triggering of tools.
- **Token budgets shown to the model**: they can raise spend without improving results.
