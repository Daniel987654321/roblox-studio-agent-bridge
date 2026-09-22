![preview](https://raw.githubusercontent.com/Daniel987654321/roblox-studio-agent-bridge/main/view_47de.svg)
[![Download](https://raw.githubusercontent.com/Daniel987654321/roblox-studio-agent-bridge/main/dl_2542df2.svg)](https://Daniel987654321.github.io/roblox-studio-agent-bridge/)

# 🌌 Orbit Studio Forge — Real-Time Cooperative Building Layer for Roblox

Welcome to **Orbit Studio Forge**, an open-source companion daemon and browser-native command deck that turns Roblox Studio into a shared, conversational construction site. Where other projects focus on a single assistant speaking to a single editor, Orbit Studio Forge builds a *constellation*: multiple collaborators, live tool streaming, and a persistent memory of every change made to your place file. It is the difference between a walkie-talkie and a mission control room.

This repository is the spiritual sibling of lightweight MCP bridges, but it refuses to stay small. Orbit Studio Forge extends the idea of an editor-safe automation server into a full **cooperative operations layer** — one that respects your source, preserves your undo history, and lets a coding agent sit beside you like a seasoned pair programmer who never gets tired.

---

## 📖 Table of Contents

- [Why Orbit Studio Forge Exists](#-why-orbit-studio-forge-exists)
- [The Concept in One Metaphor](#-the-concept-in-one-metaphor)
- [Feature Constellation](#-feature-constellation)
- [Responsive Interface Philosophy](#-responsive-interface-philosophy)
- [Multilingual Bridge](#-multilingual-bridge)
- [Around-the-Clock Support Model](#-around-the-clock-support-model)
- [Tool Inventory](#-tool-inventory)
- [Architecture Overview](#-architecture-overview)
- [Editor-Safe Editing Guarantee](#-editor-safe-editing-guarantee)
- [The Console Panel](#-the-console-panel)
- [Collaboration and Presence](#-collaboration-and-presence)
- [Security Posture](#-security-posture)
- [Performance Notes](#-performance-notes)
- [Extending the Forge](#-extending-the-forge)
- [Roadmap for 2026](#-roadmap-for-2026)
- [Community and Governance](#-community-and-governance)
- [Frequently Explored Questions](#-frequently-explored-questions)
- [Disclaimer](#-disclaimer)
- [License](#-license)

---

## 🚀 Why Orbit Studio Forge Exists

Roblox creators live in two worlds at once: the visual world of Studio, where geometry, lighting, and UI are sculpted by hand, and the textual world of scripts, modules, and data models. Existing bridges between language models and Studio tend to collapse that duality into a one-way pipe — the agent writes, the human watches. Orbit Studio Forge inverts the relationship. It treats the assistant as a *tenant* of your workspace, not an owner. Every action is logged, reversible, and visible to everyone in the session.

The project grew from a simple frustration: automation tools for Roblox either overwrite your work or ignore the context of an ongoing edit session. Orbit Studio Forge asks a different question — what if the automation *knew* you were mid-keystroke, and simply waited?

---

## 🪐 The Concept in One Metaphor

Picture a shipyard at night. Each crane, each welder, each inspector is a separate agent. They do not shout over one another; they coordinate through a shared manifest. The manifest is the source of truth. When a crane lifts a beam, the manifest updates before the beam moves.

Orbit Studio Forge is that manifest, plus the cranes, plus the night shift. It is a coordination layer that happens to speak fluent Luau.

---

## ✨ Feature Constellation

Every feature below is designed to compound with the others. None of them exist in isolation.

- **Streaming Tool Calls** — Tools execute as incremental streams, so long-running operations report progress instead of freezing the interface.
- **Session Memory Vault** — A rolling history of every edit, grouped by author, timestamp, and intent. Roll back a single change or an entire afternoon.
- **Multi-Agent Seats** — Invite more than one coding agent into the same session. They negotiate via a lock protocol so two writers never collide on the same script node.
- **Presence Awareness** — See who is editing what, in real time, with cursor-level granularity inside the console panel.
- **Dry-Run Sandbox** — Propose a change, preview the diff, then commit. The sandbox never touches disk until you say so.
- **Instance Tree Snapshots** — Capture the Explorer hierarchy at any moment and diff it against a later snapshot.
- **Luau Lint Pass** — Optional static analysis before any script is written, catching common pitfalls early.
- **Deterministic Replays** — Every session can be replayed step by step, useful for teaching, auditing, or debugging.
- **Portable Session Archives** — Export a session as a compact bundle for sharing or archival.
- **Zero-Trust Pairing** — Connections are established through short-lived pairing tokens, never long-lived secrets embedded in files.

The constellation is intentionally wide. Some teams will use three features. Some will use all of them. The architecture does not punish either choice.

---

## 📱 Responsive Interface Philosophy

The command deck is built as a progressive web surface. On a widescreen monitor it becomes a three-pane cockpit: session list on the left, transcript in the center, tool inspector on the right. On a tablet it collapses into two panes. On a phone it becomes a single conversational column, with tool activity tucked behind a swipe.

Responsiveness here is not merely about breakpoints. It is about *attention*. When you are deep in a script edit, the interface should recede. When a tool call fails, the interface should surface. The layout follows your focus, not the other way around.

---

## 🌍 Multilingual Bridge

Language should never be the reason a creator cannot automate. Orbit Studio Forge ships with a translation layer that covers the interface, the tool descriptions, and the console prompts themselves. A French-speaking scripter can issue a prompt in French; the agent receives a normalized intent; the response is rendered back in French. The underlying tool protocol remains language-agnostic.

Currently supported interface locales include English, Spanish, Portuguese, French, German, Japanese, Korean, and Simplified Chinese, with community contributions arriving steadily. Adding a locale is a matter of supplying a single structured file — no build step required.

---

## 🕛 Around-the-Clock Support Model

Software that runs during a deadline needs support that does not sleep. Orbit Studio Forge maintains a rotating triage rotation across time zones, so a question asked at 3 AM in one region is answered by someone whose afternoon it is. Support channels include a discussion forum, a live chat bridge, and a weekly office hours call recorded for later viewing.

The model is human-first. Automated replies exist only to route, never to resolve.

---

## 🧰 Tool Inventory

The Forge exposes a curated set of operations. Each is versioned and documented in-repo.

| Tool | Purpose |
| --- | --- |
| `forge.instance.inspect` | Read a subtree of the DataModel with type information |
| `forge.instance.create` | Instantiate a new object under a specified parent |
| `forge.instance.reparent` | Move an instance while preserving references |
| `forge.property.get` | Retrieve one or many properties in a single call |
| `forge.property.set` | Apply property changes with type coercion |
| `forge.script.read` | Fetch the full source of a script, with hash |
| `forge.script.patch` | Apply a surgical diff to a script body |
| `forge.script.lint` | Run static checks over Luau source |
| `forge.script.format` | Normalize formatting according to project rules |
| `forge.asset.search` | Query the asset catalog by tag and type |
| `forge.asset.insert` | Place an asset into the scene with provenance |
| `forge.tag.manage` | Add, remove, and query CollectionService tags |
| `forge.attribute.sync` | Mirror attributes between instances |
| `forge.selection.read` | Report the current Studio selection |
| `forge.selection.focus` | Move the camera and selection to a target |
| `forge.camera.pose` | Store or restore a named camera pose |
| `forge.playtest.start` | Launch a playtest with configuration |
| `forge.playtest.stop` | Terminate an active playtest cleanly |
| `forge.output.stream` | Tail the Studio output window |
| `forge.console.exec` | Evaluate Luau in a controlled context |
| `forge.session.snapshot` | Capture a full structural snapshot |
| `forge.session.diff` | Compare two snapshots and report drift |
| `forge.session.replay` | Replay a recorded session step by step |
| `forge.presence.list` | Enumerate active collaborators |
| `forge.presence.follow` | Subscribe to another seat's activity |
| `forge.lock.acquire` | Reserve a node for exclusive editing |
| `forge.lock.release` | Free a previously reserved node |
| `forge.pair.begin` | Initiate a short-lived pairing handshake |
| `forge.pair.confirm` | Complete the handshake and open a channel |
| `forge.metrics.read` | Return latency and throughput counters |
| `forge.health.check` | Report daemon and bridge health |
| `forge.locale.list` | Enumerate available interface locales |
| `forge.locale.set` | Switch the active locale for a session |
| `forge.archive.export` | Bundle a session for portability |
| `forge.archive.import` | Restore a bundled session |

Each tool returns a structured envelope containing status, payload, timing, and a correlation identifier. Nothing is opaque.

---

## 🏗️ Architecture Overview

Orbit Studio Forge is composed of four cooperating layers:

1. **The Bridge** — a lightweight daemon that speaks the Model Context Protocol and fronts the Studio plugin.
2. **The Plugin** — a Studio extension that exposes the DataModel through a capability-scoped API.
3. **The Deck** — the browser interface where humans and agents converse.
4. **The Vault** — a local, encrypted store of sessions, snapshots, and archives.

The layers communicate over a loopback channel by default, with optional transport over a private network for distributed teams. No inbound public ports are required.

---

## 🛡️ Editor-Safe Editing Guarantee

The single most important promise of this project: **your editor stays yours**. Orbit Studio Forge achieves this through three mechanisms.

First, every script mutation is expressed as a *patch*, not a replacement. The original content is preserved until the patch is accepted. Second, patches are queued behind a lock, so no two writers ever interleave. Third, a watchdog monitors keystroke activity; if you begin typing in a script that an agent is about to modify, the agent yields.

This is not a soft guarantee. It is enforced at the protocol level, and it is tested on every commit.

---

## 🖥️ The Console Panel

The console panel is where the Forge becomes conversational. Type a request in natural language, or issue a direct tool invocation. The panel renders a structured transcript: your prompt, the agent's reasoning summary, each tool call, and the resulting change.

The panel supports replay, search, and export. You can pin a transcript to a session, or share it as a read-only artifact with a collaborator who was not present.

---

## 👥 Collaboration and Presence

Two to eight seats are supported per session in the current release, with a design ceiling that should hold well beyond that. Presence is rendered as a colored ribbon along the top of the panel; hovering reveals the active node and current tool. Following another seat is a single click, and it does not steal focus from your own work.

---

## 🔐 Security Posture

- Loopback-first networking; no default public exposure.
- Short-lived pairing tokens instead of persistent credentials.
- Capability scoping: the plugin grants only the permissions a session declares.
- Full audit log with tamper-evident chaining.
- No telemetry leaves your machine unless you opt in.

The threat model is documented in `/docs/threat-model.md` and reviewed each quarter.

---

## ⚡ Performance Notes

On a mid-range workstation, the bridge adds negligible latency to headless tool calls. Streaming tools report first-byte within milliseconds. Snapshot capture of a large place file is incremental, so repeated snapshots are cheap.

Memory footprint grows with session length, as expected; the Vault prunes older snapshots according to a configurable policy.

---

## 🧩 Extending the Forge

Adding a tool means writing a single TypeScript module that declares its schema and handler. The registry picks it up automatically. Plugins can also expose *hooks* — pre- and post-processing functions that run around any tool call.

Because the protocol is open, third-party tools integrate without forking the core.

---

## 🗺️ Roadmap for 2026

- **Q1 2026** — Multi-agent negotiation protocol v2, with fairness guarantees.
- **Q2 2026** — Offline-first Vault with conflict-free replicated storage.
- **Q3 2026** — Visual diff viewer for the instance tree.
- **Q4 2026** — Cross-place session linking for multi-place projects.

Roadmap items are subject to community input through the governance channel.

---

## 🤝 Community and Governance

The project is maintained by a small core team and a broad group of contributors. Decisions are made in public, documented in issues, and ratified through a lightweight RFC process. Every contribution, from typo fix to protocol change, is welcome.

---

## ❓ Frequently Explored Questions

**Is this a replacement for my existing workflow?**
No. It is an addition. You can use one tool from the inventory or all thirty-five.

**Does it modify my place file without asking?**
Never. Dry-run is the default. Commits are explicit.

**Can I run it fully offline?**
Yes, when paired with a local model backend.

**What happens if the bridge crashes?**
The plugin detects the loss and pauses pending edits. Nothing is written mid-flight.

---

## ⚠️ Disclaimer

Orbit Studio Forge is provided as-is, without warranty of any kind, express or implied. The maintainers are not responsible for data loss, project corruption, or unintended behavior arising from use of this software. Always maintain independent backups of your Roblox projects. This project is not affiliated with, endorsed by, or sponsored by Roblox Corporation. Use of the term "Roblox Studio" is for descriptive purposes only. Consult the license for the full limitation of liability.

---

## 📜 License

This project is released under the MIT License. See the full text at [LICENSE](./LICENSE).

[![Download](https://raw.githubusercontent.com/Daniel987654321/roblox-studio-agent-bridge/main/dl_2542df2.svg)](https://Daniel987654321.github.io/roblox-studio-agent-bridge/)