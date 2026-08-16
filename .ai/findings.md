<!-- type: findings | status: active | since: 2026-08-16 | applies-to: work-activity-log -->

# Findings: work-activity-log

## repo_distiller — docs_index self-listing inconsistency

`deterministic.docs_index` (parser-produced, not hand-edited) lists only `.ai/CONTEXT.md`, even though `.ai/distillate.json` and `.ai/distillation-ollama.md` are also present under `.ai/` at read time. Compare `LogicallyTyped`'s distillate (same pipeline run), whose `docs_index` lists all three `.ai/` files. The apparent cause: the parser lists whatever is already on disk under `.ai/` at scan time — a repo whose distillate/ollama-md outputs did not yet exist when `docs_index` was computed under-lists relative to a repo where they pre-existed from an earlier pass. Parser-ordering artifact, not a content error; field left as parsed per the Stage 2 rule against hand-editing deterministic values.

## repo_distiller — distillation-ollama.md / distillate.json integration_points mismatch

`.ai/distillation-ollama.md § Integration Points` renders:

```
- UNKNOWN
```

while `.ai/distillate.json interpretive.integration_points` is `[]` (correctly empty — this repo has no external integration points). The Markdown renderer appears to emit a literal `UNKNOWN` bullet for an empty list rather than an explicit "none" statement or omitting the section. Minor renderer inconsistency; `distillation-ollama.md` is a rendered pipeline artifact, not hand-edited here.
