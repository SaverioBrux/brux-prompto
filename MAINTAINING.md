# Maintaining brux-prompto

Where to put your hands. SKILL.md does not name this file, so the model does not load it.

| File | What it holds | When you edit it |
| --- | --- | --- |
| SKILL.md | The path: modes, weight, ambition, spec, craft rules, briefs, output format | To change how the skill decides or how much it produces. Limit: 500 lines |
| references/templates.md | The prompt templates, reusable blocks and the Debug table (symptom to fix) | To change the text that ends up in prompts |
| references/ambition.md | The moves on the three axes (Altitude, Depth, Range) and the ambition map template | Rarely |
| references/executors.md | How to name skills and tools; finding new skills and the safety review | When the way to search or review changes. Dated |
| references/toolkits.md | The user's kits by domain (template + one example) | Only to change the format; the content belongs to each user |
| references/claude-notes.md | How current Claude models behave | At every new model. Dated |
| references/examples.md | One example per mode and weight | When the output format changes |
| CHANGELOG.md | The version log | At every version |

## Three rules for changing it without breaking it

1. Every concept is defined in one file; the others refer to it by name. Where things live:
   - weight and how much to produce: SKILL.md, "Step 0" and "Output format";
   - the outside judge: SKILL.md, "Four principles" and "Move 2";
   - what already exists: SKILL.md, "Step 3";
   - language: SKILL.md, "Language" (templates only point to it);
   - project memory: SKILL.md, "Project memory"; the text that goes in the prompt is in templates.md;
   - how kits are used: toolkits.md, "How to use".
2. Before adding a line to SKILL.md, look for one to remove. After every change check:
   lines in SKILL.md (500 at most), characters in the description (1024 at most), the
   version number in the frontmatter, a line in the changelog.
3. After a change, rerun at least one case per weight: a tweet (light), follow-up emails
   after a demo (medium), a multi-session research project on a coding agent (heavy).
   Run one of them in a language other than English.

## Labels are an interface

The English labels in the templates ("Done when", "Verification", "Ask me before",
"Start from", "Already exists", "Decided", "to be verified") are referred to by name in
SKILL.md and across the reference files. Rename one everywhere or nowhere.

## Dated files

`claude-notes.md` and `executors.md` carry a "Checked" date. When you re-check them,
update the date and say in the changelog what was compared with what, and what was not.
