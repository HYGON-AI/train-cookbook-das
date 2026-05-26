# Usage

Use this plugin through prompt-driven entry, not through a large command
surface.

## Prompt Entry

Start from one of these prompt examples:

- [prompts/observe_first.prompt.md](./prompts/observe_first.prompt.md)
- [prompts/train_optimize.prompt.md](./prompts/train_optimize.prompt.md)
- [prompts/kernel_route.prompt.md](./prompts/kernel_route.prompt.md)

## Plugin Intent

This plugin is for:

- DCU training performance observation
- training optimization routing
- optional kernel-route continuation

This plugin is not for:

- deploying the shared RAG environment
- distributing model/index assets
- exposing a large standalone command catalog to end users

## Shared Dependency

The plugin expects an existing shared RAG capability:

```bash
dcu-rag-kb-query "hygon dcu index_add atomic optimization"
```

## Notes

- Treat the prompt files as the main public usage surface.
- Treat the rest of the repository as implementation detail.
