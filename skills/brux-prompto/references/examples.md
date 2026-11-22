# Worked examples

One per mode and weight. Read when unsure how much to produce, and in Improve, Debug and
Handoff modes. The requests are shown in English; answer in the language the user writes
in.

**Light.** "Write me a prompt for a tweet about the new product launch" → one line:
objective + tone + length + one thing to avoid. No ambition, no guardrails.

**Medium.** "Write me a prompt for follow-up emails after a sales demo" → medium
template, testable criteria (one call to action, under 120 words, opens on a concrete
pain point), assumption stated ("I assumed a B2B audience and a direct tone"). Then one
line: "Want me to raise the bar? For example, start from the demo transcripts and
surface the recurring objections before writing, checking them against two demos that
were not used."

**Heavy.** "Every month I prepare the sales report for management, help me do it better
with AI" → ambition map: environment stated as an assumption (e.g. a CRM export is
available, billing data unknown); Altitude from "explain what changed" to "a continuous
at-risk-customer alert, backtested on history and run beside the report for a month";
Depth testing a belief the user names (e.g. "we lose on price") against raw deal
history, judged on an unused quarter; Range with a red-team reviewer looking for
mismatches between CRM and revenue. Recommendation: rung 2 + the belief test, then ask
which version to compile. Then the full template, then Persist lines (save last
quarter's best report as the reference, keep the criteria in project instructions).

**Improve.** "Improve this prompt: 'You are a marketing expert. Write a complete
editorial plan for Instagram.'" → the same request on the medium template: persona
removed, objective, audience and resources left as fields for the user, a table as
output, four testable criteria. Then three lines on what changed and why, and the
one-line ambition offer.

**Debug.** "I asked it to fix the documentation and it stopped halfway, asking whether
to continue" → symptom: stops halfway. Patch: add the unattended Process block and say
which actions need approval. Return the patched prompt and what changed.

**New prompt, build.** "I want to make something to get more out of my smart glasses" →
before any prompt: search the official SDK, community projects on GitHub, the user
forums and the apps already on sale. Show "Already exists" (e.g. an official SDK limited
to notifications, a community library that already handles the display protocol, two
apps covering translation). Recommendation: extend the community library for the one use
nobody covers. The prompt then starts from that library by name instead of from a blank
page.

**Handoff.** After an hour planning a site migration: "write me a brief so another chat
can carry it out" → handoff template filled from the conversation: goal and done-when
checks, the first step, the decisions with reasons (and the hosting option that was
rejected, with why), exact URLs and dates, what needs approval, the checklist. One line
after it: "Paste it into a new chat and attach the site export."
