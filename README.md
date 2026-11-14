# April

April is a personal, voice-first AI agent being designed around a portable core, a Mac-first native experience, Cloudflare-backed coordination and storage, and specialist agents. Its unified workspace brings together conversations, files, interactive artifacts and explicit approvals.

This repository currently contains design documentation and interactive simulations. It is not yet a working agent product.

Start with the [project wiki](wiki/README.md), [architecture](wiki/architecture.md), and [roadmap](wiki/roadmap.md).

## Acknowledgments and design references

We credit the teams whose work informs April’s design:

- **[Supermemory](https://supermemory.ai/)** — a strong reference for memory extraction, temporal facts, relationships, profiles, corrections and forgetting. April will implement its own memory system; Supermemory is not a planned runtime dependency. Our [research notes](wiki/research/memory.md) distinguish documented behavior from April’s decisions.

- **Anthropic’s The components of agent memory** is a reading reference for how agents capture, consolidate, and retrieve knowledge across sessions. [Article](https://www.anthropic.com/research/components-of-agent-memory) · [April’s reading questions](wiki/research/memory.md#related-reading-on-agent-memory)
- **Anthropic’s [Building always-on agents](https://claude.com/resources/articles/building-always-on-agents)** — an implementation reference for event-driven runs, durable inboxes, timers, memory, permissions and outgoing delivery. [April architecture notes](wiki/architecture.md#always-on-agent-design-reference) record how to use it during design; it does not select a provider or runtime dependency.
- **[Obsidian](https://obsidian.md/)** — inspiration for file-based vault organization, navigation and a tabbed knowledge workspace. April’s interface will be unified within its own application.
- **[OpenAI’s Codex](https://openai.com/codex/)** — a product reference for computer-use interaction, long-running conversations and delegated task workflows. Further study is planned; references do not imply access to proprietary implementation details.

Maintain these acknowledgments as additional references materially inform the project. Describe the specific influence and distinguish inspiration from reused code or a dependency. Any future code or asset reuse must retain applicable licenses, notices and attribution. These acknowledgments do not imply affiliation or endorsement.
