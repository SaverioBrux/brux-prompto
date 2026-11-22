# The three axes of ambition

Read this before building an ambition map (Heavy tasks, or whenever the user asks to be
more ambitious). The four principles and the "Recommend" rule are in SKILL.md.

Source: the axes, most of the moves below and the idea of an outside judge come from
Felix Rieseberg, "How to be more ambitious: A tutorial for humans with models"
(13 October 2026,
felixrieseberg.com/how-to-be-more-ambitious-a-tutorial-for-humans-with-models/). This
skill adds the gate by stakes, the rule that every escalation gets a judge, the three
crew groups and the premortem.

## Altitude: climb from task to outcome

Build a short ladder, usually three rungs above the plain task. Add a third question to
the two in SKILL.md Step 1: **which past constraint does this process exist for?** Many routines date
from when humans had to sift data by hand; if that constraint is gone, the process can be
redesigned.

Typical rungs:
1. **Understand** instead of fill in: all available data, explain what changed, why, and
   what to do.
2. **Prepare the decisions:** the few most urgent ones, with options and arguments for
   and against.
3. **Redesign the system:** state the purpose of the process, design a better way to
   achieve it, prove on history that it would have caught problems earlier, run it in
   parallel with the current one for a cycle.

The top rung is where durable workflows live ("fix this crash" becomes "keep the app
crash-free"), and it only works once the model can fetch inputs and verify on its own.

## Depth: work the way the best in the field work

Pick the moves that fit:

- **Expert instruments:** databases, statistical models, profilers, simulations, primary
  sources. Insist on them when the model drifts to markdown tables and prose. The user
  doesn't need to know them; ask the model to name them, then sanity-check.
- **Rawest material:** logs, raw exports, original documents, rather than a version
  someone has already summarised.
- **Unreasonable target, framed as reasonable:** if 2× is the ask, explore 50×. Huge
  targets force architectural options small ones never reach. If the model calls it
  impossible, reassert that it is solvable. Always with a hard measurement.
- **Challenge a belief:** take one "fact" the user or organisation relies on and test it
  adversarially against raw data, looking for evidence against it.
- **Produce new knowledge:** model or simulate observed history, look for a signal nobody
  knows yet, show it predicts on data it was not built on.

## Range: bring in other fields

This is where the most surprising results tend to come from, and where people are least
creative, so do the imagining for the user.

1. **Nouns to verbs:** rewrite the deliverable as what it must achieve. "A monthly
   report" becomes "let three managers see what changed, trust the cause and pick an
   action before the meeting ends". The verbs reveal the useful fields.
2. **Crew in three groups:**
   - **Make it right:** analyst, statistician, domain specialist.
   - **Make it land:** journalist, editor, information designer, motion/audio designer.
   - **Break it (red team):** short seller, forensic accountant, security tester,
     hostile reviewer, hunting the weakest assumption and the evidence against it. A
     cheap red-team move that fits almost any task is the **premortem**: assume the
     result was delivered and failed badly, then work backward to why.
3. **Method, not persona:** not "write like a short seller" but "find the claim
   everything rests on and search for what would falsify it, as a short seller would".
   The method changes the work; a costume only changes the voice.

Parallel subagents can run crew members as separate passes, but they can be a large
share of a session's cost. Suggest them only when the passes are truly independent and
the stakes justify it; otherwise sequence the methods in one run.

## Ambition map template

Show it before the spec for Heavy tasks (see SKILL.md, "Output format"). About 300
words: one line per rung or move, no explanations beyond the judge.

```text
**The task:** [as it is today, in one line]
**Environment:** [what the model can reach · what is missing to go higher]
**Already exists:** [solutions found · what they cover · where they stop]

**Altitude**
1. [rung]; judge: [outside check]
2. [rung]; judge: [...]
3. [rung]; judge: [...]; needs: [setup]

**Depth**
- [concrete move]; judge: [...]

**Range**
- Verbs: [the deliverable rewritten as actions]
- Make it right: [role → method]
- Make it land: [role → method]
- Break it: [role → method]

**Recommendation:** [chosen version · cost/risk in one line · first step]
```
