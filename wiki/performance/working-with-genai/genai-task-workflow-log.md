---
type: log
created: 2026-09-03
updated: 2026-09-03
status: active
tags: [working-with-genai, routing, log]
---

# GenAI Task Workflow Log

This is the journal of work run through the [[genai-task-workflow]] chain: one
entry per run, with what happened and the lesson. It covers failure at any step -
admission oversized or fragmented, work type misclassified, verification
misjudged, routing wrong, steering wrong -
so it is the single repository checked when scoping new work ("I tried something
like this before and here is why it went wrong"), and lessons compound into the
models instead of scattering. It is read at task creation when routing is being decided, and
written in the same operation as the deliverable's Time Log row whenever a run
was routed. Vocabulary: work types from [[mm-work-types]], check forms from
[[mm-verification]] - this file records instances and defines nothing.

**Entry format:** the heading is the scannable digest - `date · work type ·
outcome · deliverable` - and the bullets carry the detail, one or two lines
each. Outcome values: **Worked / Partly / Failed**. The Lesson line names which
chain step went wrong (admission / work type / verification / routing /
steering) so the log is queryable by step as well as by type. Newest first.

---

## 2026-09-03 · Taste work (admission ceremony) · Failed · [[ai-engineering-patterns]] Deliverable 2

- **Work:** Defining the D2 enabler (task-routing skill) through the standard
  ceremony. Spread across four sessions (24 Aug - 3 Sep); the definition never
  completed, and Julian paid the context re-acquaintance cost three times
  ("remind me the scope", "what have we defined so far", "tell me about the
  skill again").
- **Check:** n/a - nothing was ever routed, because admission never finished.
  That is the failure.
- **Outcome:** Failed - defining the work cost more of Julian's time than
  doing it would have (the machine does the doing).
- **Lesson:** Step at fault: admission. Deciding what and why is Taste work - only Julian can do it. The
  process made too much of it (a full interview for a machine-built 2h box)
  and split it across four sessions, paying the forgetting tax each time.
  Keep admission small, do it in one sitting, build immediately. Fix: the
  AGENTS.md Admission Fast Lane, created from this failure.

## 2026-09-03 · Build + Wiki ops · Worked · [[routing-work-system]]

- **Work:** Built the routing-work system in one interactive session: three new
  wiki files, chain edits across five mental models, an AGENTS.md rule, a
  SessionStart hook, register rows.
- **Check:** Deterministic - hook branches pipe-tested, links resolve, mirrors
  match source, formats validate.
- **Outcome:** Worked - 60 attended minutes + 819k tokens for work that would
  have taken a day-plus by hand; nothing needed rework.
- **Lesson:** Deterministic-check work delegates profitably at volume. Direct
  contrast with the 1 Sep entry: same week, same tools, opposite outcome,
  separated only by check profile.

## 2026-09-01 · Taste work · Partly · [[uk-relocation-project]] (BAU Kanban cards)

- **Work:** Claude drafted the text of a batch of BAU Kanban task cards and
  created the board; the task list itself was already mine.
- **Check:** Human judgement only - card text had to match my terse operational
  register, and only I can judge that.
- **Outcome:** Partly - the board mechanics were fine, but every card came back
  verbose despite the AGENTS.md writing rules, and I rewrote all of them
  (~120 focused minutes, more than writing them myself would have cost).
- **Lesson:** Step at fault: work type. Text in my register is taste work even
  when it looks like mechanical ops. Split next time: I write the card text,
  Claude does the Jira creation. An instruction (the length rule) is not a
  guarantee. Extends hold-the-pen beyond personal messages.

## 2026-08-21 · Critique · Worked · [[tti-comms-log]]

- **Work:** Claude critiqued and fact-checked a message I had drafted myself to
  Stephan/Ty.
- **Check:** Human judgement, cheap - I read each finding and judged it in
  seconds.
- **Outcome:** Worked - the critique caught a claim in my draft that was untrue
  against the record, before it was sent.
- **Lesson:** On voice work, critique and fact-check is where Claude's value is.
  Pair this with the entry below: same run, the two halves of hold-the-pen.

## 2026-08-21 · Taste work · Failed · [[tti-comms-log]]

- **Work:** Claude drafted personal messages to Stephan and Ty in my voice,
  iterating on tone and content.
- **Check:** Human judgement only - no external criterion for "sounds like me".
- **Outcome:** Failed - three drafts in a row rejected; I wrote my own and had
  Claude critique it instead (the entry above). Nine iterations were also burned
  polishing a message events then killed.
- **Lesson:** Step at fault: routing (should have been by hand). I hold the pen
  on my voice. And don't polish a pending message
  while events are still moving - draft close to the send moment.
