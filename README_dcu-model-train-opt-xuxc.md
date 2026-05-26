# dcu-model-train-opt-xuxc

`dcu-model-train-opt-xuxc` is a lightweight plugin boundary for DCU model
training optimization.

It is intentionally delivered as:

- plugin metadata
- install note
- usage note
- prompt examples

It is intentionally not delivered as:

- a shared RAG deployment package
- a bundled knowledge-base distribution layer
- a large public command surface

## Public Surface

Use only these as public-facing entry points:

- [INSTALL.md](./INSTALL.md)
- [USAGE.md](./USAGE.md)
- [prompts/](./prompts)
- [`.codex-plugin/plugin.json`](./.codex-plugin/plugin.json)

## Plugin Purpose

This plugin exists to guide an agent through:

- observe-first analysis of a DCU training project
- training optimization routing
- optional continuation into kernel-route work

## Workflow

This plugin is intended to drive a lightweight training optimization flow:

```text
real project entry
  -> observe-first profiling
  -> bottleneck judgment
  -> training optimization routing
  -> optional kernel-route continuation
```

In practice, the expected phases are:

1. observe-first
2. training optimization
3. kernel-route continuation when evidence supports it

The prompt examples in `prompts/` map directly to those phases.

## Functional Scope

This plugin is meant to cover:

- DCU training performance observation
- bottleneck routing between higher-level optimization and kernel-route work
- prompt-driven usage for Codex or a similar agent
- interaction with an already-available shared RAG environment

This plugin is not meant to cover:

- shared RAG deployment
- knowledge-base asset distribution
- standalone command-heavy platform delivery

## Assumptions

This plugin assumes the host environment already provides:

- an external `dcu-rag-kb` capability
- the shared knowledge-base / model / index setup behind that capability
- agent-side plugin loading support

## Start Here

1. Read [INSTALL.md](./INSTALL.md)
2. Read [USAGE.md](./USAGE.md)
3. Pick a prompt from [prompts/](./prompts)

## Notes

- RAG is an external dependency.
- Prompt files are the main usage surface.
- The rest of the repository should be treated as implementation detail.
