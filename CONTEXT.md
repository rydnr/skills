# PythonEDA knowledge base

Glossary for the Open Knowledge Format (OKF) knowledge base of PythonEDA and the `/pythoneda-grill` skill that maintains it.

## Language

**OKF** (Open Knowledge Format):
The v0.2 markdown-plus-YAML-frontmatter format the knowledge base is written in. The full spec is bundled at `pythoneda-grill/references/OKF.md`.
_Avoid_: knowledge format, doc format.

**Bundle**:
One repository's self-contained OKF directory, at `./<org>/<repo>/okf/`.
_Avoid_: package, folder, knowledge base (the whole corpus).

**Concept**:
A single `.md` file in a bundle, one per domain class, carrying `type` frontmatter.
_Avoid_: document, page, entry, note.

**Concept type** (`type`):
The required frontmatter field classifying a concept. One of fifteen fixed values; see the type vocabulary below.
_Avoid_: kind, category, tag.

**Knowledge base**:
The collection of all thirty-four bundles, one per domain repository.
_Avoid_: wiki, docs, corpus, documentation.

**OKF worktree**:
A git worktree of a domain repository, checked out at `./<org>/<repo>/`, whose `okf/` subdirectory is that repository's bundle.
_Avoid_: checkout, clone, sandbox.

**Task** (`TASK.md`):
The file in the current folder describing the work to be done; the input the grill refines.
_Avoid_: spec, ticket, issue, brief.

**Task-scoped CONTEXT.md**:
The glossary `/pythoneda-grill` writes beside a `TASK.md`, holding only the terms that task needs.
_Avoid_: optimized CONTEXT.md, global CONTEXT.md, full glossary.

**Initial OKF build**:
The separate, out-of-scope process that first populates the bundles from code. `/pythoneda-grill` consumes its output, never builds it.
_Avoid_: bootstrap, seeding.

## Concept type vocabulary

Fifteen fixed values. The three classifier enums — `PescioSpace` (`decision`, `artifact`, `runtime`, `tenant`), `ArchitecturalRole` (`bounded_context`, `event`, `shared_kernel`, `realm`, `code_request`, `iac`), and `HexagonalLayer` (`domain`, `infrastructure`, `application`) — are recorded as tags, never as types.

Structural — what a package is:

- **Domain**: a bounded context modelling one artifact/runtime concern (e.g. `Git`, `Boot`).
- **Shared Kernel**: a reusable library that grows on demand.
- **Realm**: a space where a human (or their agent) lives and automates.
- **Sandbox**: a proof-of-concept or experiment.
- **Tool**: developer-facing tooling (`git-hook`, `new-domain`, `flow-inspector`).
- **Code Request**: a request for code execution/review.

DDD / hexagonal building blocks — what a class is:

- **Entity**: an object with identity and mutable state.
- **Value Object**: an immutable value with no identity.
- **Event**: a domain event.
- **Event Listener**: a component that reacts to events (realms are listeners).
- **Event Emitter**: a component that emits events.
- **Port**: a hexagonal seam (including primary ports).
- **Adapter**: a technology-specific implementation of a port, in the infrastructure layer.
- **Application**: an entry-point application.
- **Nix Flake**: a Nix flake; lives in the `-def` repository's bundle, not the domain repo's.
