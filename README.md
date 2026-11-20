# Yelzhas Saken

AI engineer in Almaty, Kazakhstan. I build tools around LLMs and coding agents and use them in daily work.

The repositories are cleaned exports of my working copies, so their history starts on 2026-11-20.

## Repositories

| repository | what it is | status | how to check |
|---|---|---|---|
| [video-studio](https://github.com/Eljonio/video-studio) | Video generation pipeline on top of the Higgsfield CLI: scene as data → compiled prompt → N variants → frames and quality flags → pick | in use for my own reels and promo clips | `npm test` (12 tests); demo project compiles a prompt without spending credits |
| [vault-app](https://github.com/Eljonio/vault-app) | Long-term memory for coding agents: Markdown notes, facts with a source and history, recall added to every prompt, credential redaction | in daily use | `npm test` (41 tests, no network) |
| [claude-panel](https://github.com/Eljonio/claude-panel) | Overview of several parallel Claude Code sessions plus a sandboxed auditor session that reviews them | in daily use (Linux, X11) | `python3 -m unittest discover -s tests` (34 tests, 5 need GTK) |
| [claude-code-kit](https://github.com/Eljonio/claude-code-kit) | Working rules for Claude Code (63 rules, each with the incident behind it) and the memory system as an installable kit: hooks, memory layout, templates | the rules and the memory are in daily use on Linux; tests and the installer pass in CI on Linux, Windows and macOS | `npm test` in `vault-app/` (46 tests); `./install.sh` with a temporary `HOME` |
| [voice-lab](https://github.com/Eljonio/voice-lab) | Kazakh / Russian TTS: data cleaning, two-ASR transcription, LoRA fine-tuning of VoxCPM2, independent evaluation, streaming server | research prototype, not in production | CPU-only tests in `serve/`; method and numbers in `docs/METHOD.md` |
| [logic-map](https://github.com/Eljonio/logic-map) | Map of an Express backend (routes, middleware, tables, impact of a change) with an MCP server of 18 tools for Claude Code; React + Spring Boot | earlier project (spring 2026), not in use now | `./mvnw test` (1 generated test); MCP `tools/list` returns 18 tools; demo app in `examples/` |
| [secbox](https://github.com/Eljonio/secbox) | Secrets safe for working next to an agent: the agent uses a password or token without seeing it (age + GnuPG, timed unlock in RAM) | working tool with an end-to-end test; not in daily use yet | `python3 -m unittest discover -s tests` (1 end-to-end test on a throwaway safe) |
| [mebel-cnc](https://github.com/Eljonio/mebel-cnc) | Parametric cabinet furniture for CNC: model → drilling → sheet nesting → DXF | prototype, never cut on a real machine | `python -m pytest -q` (53 tests) |

Each README has a "Where to look first" table and a "Limitations" section. Each repository runs its tests on
GitHub Actions on every push; the badge at the top of its README shows the current result.

## Where each topic shows up in code

| topic | where |
|---|---|
| Coordination between parallel agent sessions through hooks | claude-panel: `claude_panel/hookprompt.py`, `claude_panel/collector.py` |
| Working rules for an agent written from real failures (rule / why / how to apply) | claude-code-kit: `rules/` |
| Sandboxing an agent: tool list, `PreToolUse` guard, read-only command whitelist | claude-panel: `claude_panel/guard.py`, `claude_panel/auditor.py` |
| Retrieval into the context window under a size budget (lexical, no embeddings, 1 KB per prompt) | vault-app: `lib/recall.js` |
| Keeping an agent from repeating stale statuses | vault-app: `lib/facts.js`, `lib/verify.js` |
| An MCP server: tool definitions with schemas over stdio | logic-map: `mcp-server/src/index.js` |
| Keeping credentials out of the context | secbox: `bin/sec` (`cmd_env`, `ask_pass`); vault-app: `lib/redact.js`; claude-panel: `scrub` in `claude_panel/journal.py` |
| A prompt as a compiled, linted artefact instead of hand-written text | video-studio: `src/domain/prompt-compiler.js`, `src/domain/prompt-prose.js` |
| Wrapping a generation CLI: cost estimate, bounded parallelism, recovery after a restart | video-studio: `src/services/runner.js`, `src/adapters/higgsfield-cli.js` |
| Fine-tuning and evaluation that does not depend on the labelling model | voice-lab: `docs/METHOD.md`, `scripts/gigaam_eval.py` |
| Outputs that are read back and verified before anything is written | mebel-cnc: `mebel/checks.py`, `mebel/dxf_out.py` |

## Not in these repositories

- Client and employer work is kept in three private repositories: a production LLM receptionist in WhatsApp and
  Instagram (Node.js, PostgreSQL, WhatsApp Cloud API), a site with a subscriber bot and a request inbox for an
  internet provider, and an outreach automation system. They are confidential; access for review is given on request.
- Training data, model weights and generated media.

UI text and most code comments are in Russian; the READMEs are in English.
