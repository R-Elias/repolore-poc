# RepoLore Method

RepoLore is a static knowledge base for this repository.

It exists to give humans and coding agents the operational memory they do not automatically have: the context, assumptions, structure, decisions, and maintenance knowledge needed to work on the repository efficiently.

RepoLore does not act. Agents and developers act. RepoLore informs them.

## 1. Purpose

RepoLore is not ordinary documentation.

Documentation usually explains what the project does. RepoLore explains what a future maintainer or coding agent should know before changing the project.

RepoLore should reduce:

* unnecessary source-code exploration;
* repeated rediscovery of the same context;
* token waste in agentic development;
* incorrect changes caused by missing architectural context;
* loss of knowledge between sessions, agents, and developers.

The core question for every RepoLore file is:

> What should a competent maintainer or coding agent know before changing this area?

## 2. Source of Truth

The code is always the source of truth.

If RepoLore conflicts with the code, trust the code and update RepoLore.

If RepoLore is missing, incomplete, or stale, improve it only where doing so is useful for future work.

Do not invent certainty. If something is inferred but not confirmed, say so explicitly.

## 3. Structure

RepoLore lives in `.repolore/`.

The minimum structure is:

```text
.repolore/
  method.md
  root.md
  tree/
```

`method.md` defines how RepoLore must be used and maintained.

`root.md` describes the repository as a whole. It is the main entry point for understanding the project.

`tree/` mirrors the repository structure.

The RepoLore tree is structurally complete but knowledge-sparse.

This means:

* repository paths may have corresponding RepoLore nodes;
* most nodes may be empty or minimal;
* only useful levels contain real knowledge;
* knowledge should live at the level where it helps future work.

Structural completeness does not imply documentation completeness.

## 4. Root File

`.repolore/root.md` should explain:

* what this repository is;
* its main purpose;
* its major areas;
* how the repository is organized;
* where to start for common kinds of work;
* where important RepoLore knowledge currently exists;
* known uncertainty or missing knowledge.

`root.md` should act as a task-oriented map, not as a full project manual.

Prefer:

```text
If you work on X, start with Y.
If you investigate Z, read A and B.
```

Avoid:

```text
This folder contains files.
```

unless that information is useful for future work.

## 5. Tree Mirror

`.repolore/tree/` mirrors the repository’s file and directory structure.

The mirror exists so that agents can navigate knowledge using repository paths.

For example:

```text
src/services/payment/stripe.ts
```

may correspond to:

```text
.repolore/tree/src.md
.repolore/tree/src/services.md
.repolore/tree/src/services/payment.md
.repolore/tree/src/services/payment/stripe.ts.md
```

Not all of these files need meaningful content.

A node may be empty, minimal, or rich.

Use rich knowledge only where it adds value.

## 6. Reading Before Work

Before modifying or deeply analyzing an area, read RepoLore first.

For a target path, read:

1. `.repolore/method.md`
2. `.repolore/root.md`
3. the non-empty RepoLore nodes along the path to the target
4. any related RepoLore files mentioned by those nodes

Only then inspect the source files needed for the task.

Do not begin by loading broad unrelated parts of the repository. RepoLore exists to avoid that.

## 7. Writing After Work

Update RepoLore when a change affects operational memory.

A RepoLore update is required when a change affects:

* behavior;
* architecture;
* responsibilities of a file, folder, module, service, package, or subsystem;
* public or internal APIs;
* dependencies;
* configuration with behavioral impact;
* data model or schema;
* important file or folder paths;
* conventions;
* assumptions future maintainers need to know;
* interactions between areas;
* non-obvious bug fixes;
* important tradeoffs or design decisions.

A RepoLore update is usually not required for:

* formatting;
* typo fixes;
* mechanical cleanup;
* obvious local implementation changes;
* changes that do not affect future maintenance;
* temporary edits that are not intended to persist.

When unsure, add a short useful note rather than leaving future agents without context.

## 8. Where to Write Knowledge

Write knowledge at the level where it is most useful.

Use higher-level files for broad context:

```text
.repolore/root.md
.repolore/tree/src.md
.repolore/tree/apps.md
```

Use mid-level files for subsystems, packages, services, domains, or important folders:

```text
.repolore/tree/src/services.md
.repolore/tree/packages/auth.md
```

Use file-level knowledge only when a specific file contains non-obvious behavior, important constraints, or unusual implementation details.

Do not create rich file-level knowledge by default.

## 9. What to Write

Good RepoLore content includes:

* purpose of the area;
* responsibilities;
* important files and why they matter;
* local conventions;
* invariants;
* important dependencies;
* assumptions;
* non-obvious behavior;
* common pitfalls;
* change notes;
* related areas to inspect when modifying this area.

Bad RepoLore content includes:

* paraphrases of obvious code;
* exhaustive summaries of every file;
* large copied code snippets;
* generic documentation;
* stale speculation;
* notes that do not help future development.

Prefer concise operational knowledge.

## 10. Empty Nodes

An empty RepoLore node is allowed.

It means:

> This path exists structurally, but no useful operational knowledge has been recorded here yet.

Do not fill empty nodes just to make the tree look complete.

Fill a node only when the knowledge would help future agents or maintainers.

## 11. Existing Large Repositories

When initializing RepoLore in an existing large repository, do not try to document everything.

Use this approach:

1. create the RepoLore structure;
2. generate a useful but imperfect `root.md`;
3. identify major areas from existing docs, configs, folders, manifests, and naming conventions;
4. add knowledge only for high-value areas;
5. let RepoLore improve over time as real work touches the code.

The correct adoption model is:

```text
broad structure, sparse knowledge, continuous enrichment
```

Do not ask every owner to document everything from scratch.

When a future change touches an area, improve the relevant RepoLore nodes as part of the change.

## 12. Using Shell Commands Instead of RepoLore Tools

If no RepoLore tool exists yet, agents may use terminal commands to inspect and maintain RepoLore.

Useful operations include:

* list repository files;
* create a mirrored tree under `.repolore/tree/`;
* find non-empty RepoLore files;
* count approximate file sizes;
* inspect changed files when change information is available;
* compare repository paths with RepoLore paths.

Agents may write small shell or PowerShell commands for these operations.

Do not assume a dedicated RepoLore CLI exists.

When creating scripts or commands, keep them simple, local, readable, and safe.

## 13. Initialization Behavior

When RepoLore is first added to a repository:

1. read existing README, docs, manifests, workspace files, build files, and top-level folders;
2. create `.repolore/root.md`;
3. create or update the structural mirror under `.repolore/tree/`;
4. add knowledge only where it is immediately useful;
5. mark uncertainty explicitly;
6. avoid pretending the repository is fully understood.

The first version of RepoLore should be useful, not complete.

## 14. Maintenance Rule

RepoLore should evolve with the code.

A meaningful code change should either:

* update the relevant RepoLore knowledge; or
* leave RepoLore unchanged because the change has no operational-memory impact.

Do not let RepoLore become stale silently.

## 15. Principle

Maintain RepoLore as the repository’s operational memory.

It should emulate the knowledge a competent developer would carry about their scope: what matters, what is connected, what is risky, what is conventional, and what future agents should not have to rediscover.
