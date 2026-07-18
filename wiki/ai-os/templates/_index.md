---
type: index
created: 2026-05-26
---

# Templates

Reusable artifact patterns for producing consistent, well-structured `.md` files. Each template is a fill-in-the-blank scaffold — copy it, complete the placeholders, and the output is a ready-to-use wiki artifact.

Templates live here rather than in Service Design or System Design because they are neither process documentation nor infrastructure documentation — they are reusable output patterns.

---

## Prompt Templates

Structured prompts for use with Claude or other LLMs. Each prompt template defines the context, instruction, and output format needed to produce a repeatable result.

| Template | Purpose |
|----------|---------|
| [[prompt-0\|Prompt 0: The Human Prompt]] | Pre-flight checklist — forces you to think through outcome, stakes, done/wrong criteria, context, decomposition, and hard parts before touching an LLM |

---

## How to use a template

1. Open the template file
2. Copy the entire contents into a new `.md` file at the appropriate wiki path
3. Replace all `[placeholder]` values with real content
4. Delete the template header block before saving the final artifact
