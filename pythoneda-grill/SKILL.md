---
name: pythoneda-grill
description: Grill a PythonEDA task against its OKF knowledge base, update the OKF, and produce a task-scoped CONTEXT.md.
disable-model-invocation: true
---

# pythoneda-grill

Relentlessly interview a PythonEDA `TASK.md` against the OKF knowledge base, write what the interview resolves back into the OKF, and distill a task-scoped `CONTEXT.md` beside the task.

Two disciplines do the heavy lifting; read them when their step begins:

- `grilling` — the interview loop (design tree, frontier rounds, one question at a time).
- `domain-modeling` — the glossary/ADR discipline (capture terms and decisions as they crystallize).

Vocabulary lives in `../CONTEXT.md`; the full format spec in `references/OKF.md`; the repository list in `repositories.md`.

## Procedure

Run the steps in order; each ends on its completion criterion before the next begins.

### 1. Materialize the OKF worktrees

For every `org/repo` in `repositories.md`, ensure a worktree at `./<org>/<repo>/` on the task's working branch.

- Canonical clones live in the `.canonical/` directory beside the task folder. If `../.canonical/<org>/<repo>` is missing, `git clone https://github.com/<org>/<repo>.git` into it.
- From the canonical clone, `git worktree add` the worktree at `./<org>/<repo>/` on the task branch, creating the branch first if it doesn't exist.

Done when every line of `repositories.md` has a worktree at `./<org>/<repo>/` and its `okf/` directory is present. If the OKF is absent from the worktrees, stop and tell the user to build the initial OKF first.

### 2. Ensure the task file

`TASK.md` must exist in the current folder. If it doesn't, stop and ask for one.

Done when `TASK.md` names a concrete task.

### 3. Read the task and the OKF

Read `TASK.md`, then read the bundles the task touches: open each relevant `./<org>/<repo>/okf/index.md`, then the concepts it points to. Consult `references/OKF.md` for any frontmatter you're unsure of.

Done when you can state the task's goal and which OKF concepts already cover parts of it.

### 4. Grill

Run the `grilling` interview: build the design tree, ask the whole frontier each round, give a recommendation per question, and wait. Ask only what the OKF cannot answer; find facts yourself, put decisions to the user.

Done when the frontier is empty and the user confirms shared understanding.

### 5. Update the OKF

Write everything the interview resolved back into the bundles. Follow the type vocabulary in `../CONTEXT.md` and the frontmatter in `references/OKF.md`. A generated concept is `generated.by: pythoneda-grill/<model>`, carries `sources` pointing at the originating `.py` and `README.md` on `main`, and starts `status: draft` with no `verified`. Cross-bundle links are GitHub URLs to `main`; intra-bundle links are bundle-relative `/...` paths. Regenerate each touched `index.md` and append dated entries to each touched `log.md`.

Done when every resolved term and decision is an OKF concept with conformant frontmatter, and no touched index is stale.

### 6. Polish the TASK.md

Rewrite `TASK.md` in place to match the shared understanding from step 4 — scope, naming, and any assumptions the OKF corrected.

Done when `TASK.md` and the interview's conclusion agree.

### 7. Write the task-scoped CONTEXT.md

Write `CONTEXT.md` in the same folder as `TASK.md`, using `domain-modeling`'s glossary format: each term the task needs, defined in one or two sentences, with its `_Avoid_` set. Source it from the updated OKF bundles, never from raw code; keep implementation detail out.

Done when `CONTEXT.md` sits beside `TASK.md` and covers every term the task relies on.
