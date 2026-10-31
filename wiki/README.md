# April wiki

A living design for a personal agent system: one interaction agent across devices and apps, delegating to specialists with scoped capabilities.

## Start here

- [Vision and principles](vision.md)
- [Agent briefs](agents/README.md)
- [Architecture and Cloudflare platform map](architecture.md)
- [Shared task and result contracts](contracts.md)
- [Decision log](decisions.md)
- [Roadmap](roadmap.md)
- [Ideas and working notes](ideas.md)
- [Interactive design workspace](workspace/agent-system-workspace.html)
- [Client and GUI exploration seed](workspace/client-exploration.seed.json) — platform-agnostic core with Mac integration first, 15 choices, decisions, open questions, and ten proposed experiments (31 October 2026).
- [Interactive client and GUI exploration](workspace/client-exploration.html) — open in a browser; includes editable choices, experiments, decisions, notes, and JSON import/export. Browser edits save locally and do not automatically update the seed or TSX file.

All project artifacts have their canonical files in this `wiki/` directory. Open the browser-ready HTML for the interactive experience. The earlier app-managed TSX copy is superseded as the entry point; its source is preserved here for reference.

## Interactive maps

Both workspaces now use one matching map-first interface. Select a lens, choose a branch, and expand individual records in the details panel. The client map covers experience, stack choices, validation and decisions; the system map covers architecture, specialists, delivery and decisions. Notes and applicable statuses remain editable. Use Detailed editor for the complete original editing/import tools, and Return to map to resume visual exploration. Export JSON regularly.

The full design was committed before this redesign; the map views retain the same underlying data and browser storage keys.

### Artifact files

- [Agent system workspace](workspace/agent-system-workspace.html), [starting data](workspace/agent-system.seed.json), [map preview](workspace/agent-system-preview.png), and [usage guide](workspace/START-HERE.txt).
- [Client exploration workspace](workspace/client-exploration.html), [starting data](workspace/client-exploration.seed.json), [original TSX source](workspace/client-exploration-source.tsx), and [interface preview](workspace/client-exploration-preview.png).

The TSX source requires the original host SDK and is not a standalone browser application. Use the HTML version to interact. No GUI framework is selected. A required separate Obsidian host is ruled out in favor of one unified April application; other deferred frameworks remain recommendations rather than confirmed rejections.

Both interactive HTML workspaces and their seed data include the voice clarifications from 31 October 2026: voice-first artifacts, Mac → web → Android rollout, adjustable autonomy, user-reviewed self-extension, offline request queuing, and inspectable memory with financial/medical exclusions. The Mac clarifications also cover activation/dismissal, focus preservation, active-monitor indicators, private-vault grants, non-blocking artifacts, DOCX preview, provider-portable voice and the unified app decision. The original TSX source is an archived earlier snapshot, not the maintained UI. Existing browser edits are preserved when voice-session decision entries are added on reload; confirmed new decisions take precedence over conflicting earlier proposals.

Interactive edits save in browser storage, not directly into wiki files. Export JSON from the workspace and save the export under `wiki/workspace/` to include those edits in the project. The starting data and Markdown pages do not synchronize automatically. Browser storage is tied to the browser and address used to open the workspace.

## How to work on the idea

Develop one agent or decision at a time. Record responsibilities, required data, permissions, outputs, unresolved questions, and the smallest useful milestone. Distinguish confirmed preferences from proposed implementations.

Use these Markdown pages for repository-based ideation and reviewable changes. Keep product choices provisional until validated. Add implementation evidence and revise the roadmap as work progresses.

The interactive HTML is a portable starting snapshot, not a synchronized view of these pages. Its edits save in browser storage, not into the repository. Export JSON to preserve those edits; reconcile them into the relevant Markdown pages before treating them as project decisions. The bundled seed JSON contains the initial design, not subsequent browser edits.

To continue in chat, reference the relevant page or attach the latest exported JSON. Do not put credentials, recordings, or sensitive source data in this wiki.

Seeded from the design conversation on 30 October 2026. This documents a proposed system, not deployed infrastructure.
