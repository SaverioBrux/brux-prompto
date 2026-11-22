# Changelog

This file is for maintainers. SKILL.md does not name it, so the model does not load it.

## 1.0.0 - 22 November 2026

First public release. It follows seven private versions; the behaviour is that of the
last private one, with these changes for a general audience:

- Everything is in English: templates, labels, examples and trigger phrases. The skill
  writes to the user, and writes the prompt, in the language the user writes in.
- `references/toolkits.md` is now a template the user fills in, with one example section
  and a blank one. The author's personal stack is not included.
- Third-party skills are no longer named as examples of executors; the skill scout and
  the safety review cover them.
- The source of the ambition framework is credited with its link: the axes, most of the
  moves and the idea of an outside judge come from Felix Rieseberg's article. Passages
  that followed it closely were reworded.
- Craft rule on examples aligned with Anthropic's guidance (three to five when
  available); Claude notes updated on self-check lines (Claude Opus 5 exception), on
  example tags and on emphatic wording.
- Skill scout: mentions `npx skills add <owner/repo> --list`; run-without-installing
  shortcuts are not to be used before the safety review.

Checks done for this release:

- Frontmatter validated with skill-creator's `quick_validate.py`; SKILL.md under 500
  lines; description under 1024 characters.
- `npx skills` 1.9.0: `find`, `add`, `add --list` and `use` behave as described in
  `executors.md`; `vercel-labs/skills` still ships `find-skills`.
- `claude-notes.md` compared on 22 November 2026 with Anthropic's "Prompting best
  practices", "Prompting Claude Fable 5.2" and "Prompting Claude Opus 5" pages and with
  the Claude Code memory and prompt-caching docs. One correction: changing effort
  mid-session restarts the cache only on cloud platforms and gateways.
- The ambition files compared with the source article.
- Internal consistency audit across all files: no broken cross-references; the
  contradictions it found were fixed (Handoff recipients, template size with a kit, which
  skills a prompt may name, where the Skill line goes).
- Six fresh-session runs, one per mode and weight, three of them in a language other than English, judged by a
  separate reviewer. Fixes that came out of them: one rule for facts only the user has
  and for numbers the skill picks; an output format for Improve, Debug and Handoff;
  Step 3 starts from what the user already has; stricter Handoff rules (full dates,
  dropped options, unstated reasons); the spec is saved to disk in multi-session work;
  the ambition map template moved to `ambition.md`.
- The changed cases were rerun twice after the fixes (Improve, Debug, Handoff, Medium,
  two Heavy cases, a build with search, Light). The Heavy map is now skipped only when
  the user says so; asking for a prompt is not enough.
- Two more rounds after the punctuation pass (no em or en dashes anywhere), each judged
  by a separate reviewer: no regression from the punctuation. Fixes from them: a one-off
  document someone else approves is Medium, not Heavy; Improve offers ambition in one
  line and never opens the full map unasked; the Handoff first step comes from what was
  already planned; the Medium self-check line stays when the target model is unknown;
  a warning about personal data in anything the user pastes or attaches, in every mode;
  the Debug table moved to `templates.md`, with a new row for "answered the wrong
  question". Improve, Debug, Handoff and Heavy were rerun after these fixes.
- A last round on new cases unlike the shipped examples (photo renaming, restaurant
  reviews, a weekly unattended log check, a bills app with real web searches, a meeting
  agenda debug, a software-choice handoff), judged by a separate reviewer. Fixes: full
  dates in every prompt, and periods relative to the run in recurring ones; the ambition
  map kept to about 250 words; a Handoff fallback for the first step; in recurring
  prompts the prior-art survey runs once; in unattended runs, actions that need approval
  are skipped and listed in the final report.
- Three prompts the skill wrote (a review analysis, a meeting agenda, a handoff brief)
  were filled in and run in fresh sessions that knew nothing of the skill, on test data
  with known answers. All theme counts and review numbers matched, all seven planted
  points of the agenda were found with nothing invented, and the brief was followed
  without reopening decisions. Fixes from it: the self-check lines sit after the output
  and outside any length limit; computed numbers are marked as computed. Also: Debug
  patches only the cause of the symptom; a fixed order for the lines after a Medium
  prompt; Heavy prompts aimed under 700 words; recurring alone no longer makes a task
  Heavy; the map target set to about 300 words, where it lands in practice.
- The review and agenda prompts were then regenerated with the final skill and run on
  harder data (sarcasm, English reviews, a duplicate, an off-topic review, a withdrawn
  offer, a moved deadline, irrelevant mail, a phone number in a signature). First run:
  main counts right and all traps caught, but counts could not be checked and the
  executor invented concessions. Fixes: items are numbered and the numbers cited behind
  each count; positions the user did not give are marked as proposals; a one-off
  calculation the user can check is Medium. Second run: every count checkable, all
  traps caught, no invented positions; one wrong figure in a sentence, now covered.

Not checked for this release:

- Measured triggering of the English description.
- End-to-end runs beyond those above: the other prompts were read and judged, not
  executed. Each executed prompt ran once; the data were synthetic, real data will be
  messier still.
- That `npx skills find` prints install counts and links as described (read in the CLI's
  docs, not run).
