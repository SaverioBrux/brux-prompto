# brux-prompto

**Most prompts fail before the first word is written: they ask for the wrong size of thing.**

brux-prompto is an agent skill that writes prompts for AI models and agents. You describe
a task in your own words; it hands back one self-contained prompt you can paste into a
fresh chat or give to an agent. Before it writes, it decides how much the task deserves.

```bash
npx skills add SaverioBrux/brux-prompto
```

## Why I built this

I kept making the same five mistakes, and no prompt guide fixed them, because none of
them is about wording.

1. **Wrong size.** A three-paragraph prompt for a tweet. A one-liner for a monthly report
   that ends up in a meeting.
2. **Asking too small.** I asked the model to fill in the report, when I could have asked
   it to tell me what changed and what to decide.
3. **Letting the model grade itself.** "Looks good to me" from the same model that wrote
   it is not a check.
4. **Building what already exists.** A whole run spent on something a library already did.
5. **Starting from zero every session.** A new chat that redid, or contradicted, last
   week's work.

So the skill does not start by writing. It starts by weighing.

## How it works

Two moves, in this order.

**1. What to ask for.** The task gets a weight, and the weight decides everything after it.

| Weight | Example | What you get |
| --- | --- | --- |
| Light | a tweet, a quick email | one line. Nothing else |
| Medium | a document, an analysis, a normal coding task | a short prompt, plus one offer to raise the bar |
| Heavy | recurring work, agent runs, anything that feeds a decision | a map of more ambitious versions to choose from, then the full prompt |

**2. How to ask for it.** Objective, context, a definition of done you can test, and a
check that does not rest on the model's own opinion: a real result, a fresh session, or
you against a stated criterion.

No ambitious version is offered without that outside check. If there is no way to verify
it, the skill lowers the ambition and tells you why.

## What you can say to it

| You say | You get |
| --- | --- |
| "Write me a prompt for…" | A prompt sized to the task |
| "Improve this prompt" | The improved prompt and three lines on what changed and why |
| "Why did this prompt give a bad result?" | The failure named, and a patched prompt |
| "Write a brief so another chat can continue" | A handoff brief built only from what was decided |
| "Raise the bar on this" | An ambition map along three axes (Altitude, Depth, Range), or a stronger prompt for a small task |

It answers in the language you write in.

It hands back a prompt; it does not do the task. Ask it to write the email and it stays
out of the way: that is a job for the model, not for this skill.

## A small example

> **You:** Write me a prompt for a tweet announcing that our small bakery now delivers on
> Sundays.

A single line comes back (wrapped here to fit), adapted from a test run:

```text
Write a tweet announcing that [bakery name], a small bakery, now delivers on Sundays.
Output: one tweet, under 280 characters, warm and plain, like a neighbour sharing good
news. Constraints: say how to order ([phone, link or app]); use only the facts given
here, with no invented prices, hours or delivery areas.
```

The brackets are the two facts only you know. No framework, no ceremony.

> **You:** Every month I prepare the sales report for management. Help me do it better
> with AI.

Here it stops and shows you a map first. One rung up: explain what changed and why.
Two rungs up: prepare the decisions. Three: an at-risk-customer alert, tested on past
data and run beside the report for a month. You pick the version; it writes that prompt.

## Does it actually help? A side-by-side test

Same model, same messy data, two fresh sessions: one got the plain request ("here are 40
reviews, tell me what to improve"; "prepare the agenda, here are the emails"), the other
got the prompt brux-prompto wrote for that request. The data had planted traps (sarcasm,
a duplicate, an off-topic review, a withdrawn offer, a moved deadline) and a known
answer. A separate reviewer scored both by hand.

| Measure | Plain request | brux-prompto prompt |
| --- | --- | --- |
| Reviews: complaint counts matching the truth | 4/4 | 3/4 |
| Reviews: counts you can check (review numbers cited) | 0/4 | 4/4 |
| Reviews: traps handled | 6/7 | 7/7 |
| Reviews: quotes copied word for word | 20/23 | 16/16 |
| Agenda: critical points found, traps handled | 7/7, 5/5 | 7/7, 5/5 |
| Agenda: points that cite the email they come from | 0/4 | 4/4 |

The honest reading: a good model finds the same facts either way, and the plain answer
even had the single best insight (ratings falling in the last two months). What the
prompt changes is that every number and every point can be checked against its source,
so a wrong one gets caught. That is the outside check this skill is built around. One
run each, synthetic data: a small test, not a benchmark.

## What it does along the way

- **Looks before it builds.** For anything that gets built, it checks what already
  exists and recommends reuse, extend or build, in that order.
- **Names the right executor.** It points the prompt at the skills and tools you already
  have, without absorbing them.
- **Scouts new skills carefully.** For projects it shortlists at most three, and each one
  you pick goes through a safety review before you are told how to install it. It never
  installs anything itself.
- **Gives agents a memory.** For work that spans sessions, the prompt makes the agent
  keep an instructions file and a status file on disk, and check them against reality at
  the start of every session.
- **Debugs prompts by symptom.** Fourteen common failures, each with its likely cause
  and its patch.

## How it got here

This is version 1.0.0, and the eighth version I have written. The first seven were
private and built around my own tools. For the public one I took my personal stack out
and left a template in its place, moved everything to English, and wrote down what was
checked and what was not, in the [changelog](CHANGELOG.md). Before release it was run in
fresh sessions on one case per mode and judged by a separate reviewer, and three of the
prompts it wrote were run on test data with known answers. What that found is in the
changelog too.

## Install

On a coding agent, with the [skills CLI](https://skills.sh):

```bash
npx skills add SaverioBrux/brux-prompto
```

In the Claude apps: download `brux-prompto-skill.zip` from the
[latest release](https://github.com/SaverioBrux/brux-prompto/releases/latest) and upload
it in the skill settings.

It works with any agent that supports the Agent Skills format. One reference file,
`claude-notes.md`, is specific to Claude models and is read only when the prompt will
run on Claude.

## Make it yours

`skills/brux-prompto/references/toolkits.md` is a template. Fill it with the libraries,
skills, quality criteria and checks you have already chosen for the domains you work in,
and the skill starts from your stack instead of searching every time. It ships with one
example section and a blank one to copy. The skill works without it.

## Layout

```
skills/brux-prompto/
  SKILL.md                  the path: mode, weight, ambition, spec, output format
  references/
    templates.md            prompt templates, reusable blocks, the Debug table
    ambition.md             the moves for Altitude, Depth and Range; the map template
    executors.md            naming skills and tools; finding and reviewing new skills
    toolkits.md             your own stack by domain (template)
    claude-notes.md         behaviour notes for current Claude models (dated)
    examples.md             one worked example per mode and weight
MAINTAINING.md              how to change the skill without breaking it
CHANGELOG.md
```

## Credits

The ambition half of this skill stands on Felix Rieseberg's
[How to be more ambitious: A tutorial for humans with models](https://felixrieseberg.com/how-to-be-more-ambitious-a-tutorial-for-humans-with-models/)
(October 2026): the axes Altitude, Depth and Range, most of the moves on each, and the
idea of an outside judge come from there. Read it; it is better than any summary. What
this skill adds is the part around it: sizing the ambition to the stakes, requiring a
judge for every escalation, and turning the result into a prompt you can paste.
The notes on Claude models follow Anthropic's public prompting documentation.

## Licence

MIT. Created and maintained by Saverio ([@SaverioBrux](https://github.com/SaverioBrux)).
