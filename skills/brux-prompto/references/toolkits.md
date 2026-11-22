# Your vetted toolkits by domain

**Last checked: [month and year; fill this in when you edit the file].**

This file is yours to fill in. It holds your own stack: the libraries, skills and tools
you have already evaluated (and, for third-party skills, put through a safety review),
with the quality criteria and checks you care about in each domain. The skill reads it
before any fresh search, so prompts start from what you have already chosen instead of
rediscovering it every time.

As shipped it contains one example section, marked as such, and a blank section to copy.
Until you add your own sections the skill simply falls back to its normal search (Step 3
of SKILL.md and the skill scout).

Rules for the model reading this file:

- A section marked **(example)** shows the format. Its criteria and checks are sound
  defaults for that domain, but its tools are not the user's choices: offer them as
  options, never as "your kit".
- The file says what was chosen, not what is installed where the prompt will run: in the
  prompt, name the kit's skills with "if installed; tell me if any is missing".
- It ages: if the date above is empty or old, a tool is missing on the machine, or a
  repository has moved on from the reviewed version, say so and re-check instead of
  assuming.
- Ask whether a project is personal or commercial only when a licence rule depends on
  it. Never assume either.

How to use, at any weight above Light:

1. Find the domain of the request below.
2. Use the template for the task's weight (SKILL.md, Step 0). In the full template,
   libraries and working rules go in "Environment and material"; in the medium one, in
   "Context". Name the kit's skills.
3. Turn the domain's quality criteria into "Done when" lines and its checks into
   "Verification" lines. This is how vague wishes like "avoid AI slop" or "make it
   sound professional" become testable.
4. If a domain is not here, fall back to Step 3 of SKILL.md (and, for Heavy tasks, the
   skill scout). After a Heavy task in a new domain, offer to draft a section for the
   user to add once the tools have been chosen and reviewed.

For a Light request, take at most one working rule or quality criterion from the domain
and nothing else.

## Web design and animation (example)

- Skills: the frontend-design skill the user has, if any. One design skill leads a
  project; two with different rules contradict each other.
- Libraries, added to the project (not installed "in the model"): an animation library
  for timelines and scroll-driven sequences (for example GSAP with ScrollTrigger), and
  optionally a smooth-scrolling library (for example Lenis) synchronised with it.
- Division of labour: small UI feedback in CSS; page-level sequences in the animation
  library.

**Quality criteria (anti-slop), to adapt:**
- the page's one visual idea is written in a sentence before anything is built;
- at most two signature effects per page, each tied to the content; no fade-in on every
  section, no parallax on text, no scroll-jacking;
- real copy and real images; no placeholder text, no invented reviews, figures or logos;
- no default look (generic violet gradient, centred hero over three identical cards,
  emoji as icons) unless the brand calls for it;
- at most two type families and one spacing scale;
- interface feedback is fast (roughly under 300 ms) and never blocks input;
- with "reduce motion" set in the system, smooth scrolling and non-essential animation
  are off;
- it holds up on a phone: no layout shift, no dropped frames on scroll.

**Checks outside the model:** screenshots at three widths (about 390, 768, 1440 px)
reviewed against the criteria by a fresh session; a performance audit such as
Lighthouse on mobile; one run with reduced motion; the user looks at it before it is
called done.

**Licences:** check the licence of every library before a commercial project, and again
if the project is itself a tool for building sites.

## [Your domain] (blank: copy this section)

- **In the kit:** [skills and tools you use here; for each third-party skill, the
  version or commit you reviewed and the verdict]
- **Libraries / services:** [what gets added to the project, and where]
- **Working rules:** [what leads, what must not be combined, known side effects]
- **Quality criteria:** [testable statements of what "good" means in this domain]
- **Checks outside the model:** [measurements, tools, a fresh-session review, your own
  look or listen before it is called done]
- **Licences and limits:** [what is allowed for personal and for commercial use]

## Parked: evaluated, not adopted

Keep a line here for every skill or tool you evaluated and set aside, with the reason,
so it is not re-evaluated from scratch. Revisit only if the need changes.

- [name]: [why it was set aside]
