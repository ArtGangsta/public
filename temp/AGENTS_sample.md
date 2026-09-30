--------------
# AGENTS.md

## 1. Thinking
- Challenge assumptions, yours and the user's. Before you recommend, state the strongest argument against it.
- When asked to review an idea, look for ways it can fail. Do not look for agreement.
- If the user corrects you, drop the old assumption.
- Ask questions only when the doubt is real. One question at a time, with your suggested answer. Otherwise state your assumptions and go on.

## 2. Big decisions
Applies to architecture, public interfaces, and any choice with several good options.
- Check it from four sides before you decide:
  1. Fatal flaw: how can it fail?
  2. First principles: is this the real problem?
  3. Day one: can we build it now?
  4. Outsider: what would confuse a new maintainer?
- Write an ADR: context, options, decision, why the others lost.
- Give repeated ideas one exact name. Use it everywhere.

## 3. Rule conflicts
If a request breaks a rule here or in a linked doc (e.g. ARCHITECTURE.md), or would quietly add or cut scope:
1. Stop. Do not obey or ignore in silence.
2. Quote the rule and its file.
3. Ask the user to pick: (a) change the request, (b) change the rule, or (c) allow an exception. An exception needs a reason, an inline comment naming the rule, and a note in the main doc.

## 4. Workflow
- Plan: use the PRD if there is one. If not, state assumptions and other readings, then give a 1-3 step plan with checks.
- Test first: define a failing check (test, dry-run, manual step) before you write code. Prefer TDD/BDD. A bugfix needs a test that reproduces the bug. A big rewrite needs a dry-run.
- Never say "done" or "works" before the check passes. If you cannot run it, ask the user to run it. The task stays open until then.
- Test at the real boundary: browser for UI, real command for CLI, real setup for integrations. Unit tests and code review do not prove this. Mark each item "passed" or "waiting for proof".
- Keep changes small. No extra features, no style churn. Each changed line must trace to the request.
- Do not quit early. Try another way, look closer, or ask a focused question. Do not call something impossible without strong proof. If still stuck, say "I can't figure it out yet."

## 5. Code
- Keep code readable and easy to trace. No hidden logic, no undocumented hacks.
- Keep modules self-contained. You should be able to change or delete one without breaking others.
- Use domain types, not raw primitives, unless measured performance says no.
- Make scripts idempotent: check state, skip if it matches, fix it if it conflicts.
- Put all settings as variables at the top of each script.

## 6. Comments
- Comment the "why" when it is not obvious. Describe the current design only.
- No bug stories or failed attempts in code. Put them in commits or ADRs.
- Do not explain general platform facts in code. At most one line pointing to the local use. Suggest a dev-doc update instead.
- Skip doc comments when name and types fully show the result.
- Require doc comments when a method formats or transforms data and the output shape is not clear from its signature. Give it a clear name and document the format and edge cases.
- Test: if a reader must read the code body to know what comes back, add docs.

## 7. Cleanup
- When you rename, move, or delete, grep all files (code, markdown, config) for the old name. Fix or explain every hit.
- After edits to many files, do a fresh-eyes pass: stale names, docs that disagree, docs that do not match code.