# Install

This repository is delivered as a lightweight plugin boundary.

It assumes the host agent environment already provides:

- Codex skill loading support
- a working `dcu-rag-kb` capability
- the corresponding shared knowledge-base / model / index setup

## 1. Clone

```bash
git clone <repo-url> dcu-model-train-opt-xuxc
cd dcu-model-train-opt-xuxc
```

## 2. Let the host agent load the plugin

The expected plugin metadata is:

- [`.codex-plugin/plugin.json`](./.codex-plugin/plugin.json)

The host should use this plugin as a skill/plugin package, not as a standalone
engineering platform to install from scratch.

## 3. Validate the shared RAG dependency

```bash
dcu-rag-kb-query "hygon dcu index_add atomic optimization"
```

If this command fails, the shared RAG environment is not ready. Fix that in the
shared RAG layer, not in this plugin.

## Notes

- This plugin does not deploy RAG assets.
- This plugin does not carry models or indexes.
- This plugin is intentionally lightweight at the delivery surface.
