# SCRIPT ARCHIVE

A personal archive of standalone scripts and small projects, not a single cohesive application. Each top-level folder is independent: different language, different purpose, no shared runtime between them. Treat this repository as a collection, not a monorepo in the "shared build system" sense.

<img width="1800" height="1000" alt="ZREX ARCHIVE" src="https://github.com/user-attachments/assets/2add23a7-daff-44ed-a3b3-6636524ac5b1" />

## What's in here

| Folder | What it is | Docs |
|--------|------------|------|
| `PCI-Framework/` | Precision Contract Intent Framework: a deterministic FAQ/conversation-tree extractor from websites, Apify-actor-compatible. Already has its own `README.md`, `AGENTS.md` (execution guide), and `CAPSTONE.md` (internal peer review record). | See the folder's own docs |
| `DELUGE/` | Zoho Cliq Deluge scripts: the "Shot Engine" Gemini-powered bot commands (built for a CliqTrix '26 submission) and the `SNIPER` Auth0 login script. | [`docs/DELUGE.md`](docs/DELUGE.md) |
| `TRADING/` | A market-making quant trading framework, built for a simulated trading competition environment (not a live-money trading system). | [`docs/TRADING.md`](docs/TRADING.md) |
| `VISPER-HOTKEY/` | AutoHotkey + Python hotkey utilities tying into VISPER (transcription) and DeepL, for local workflow automation. | [`docs/VISPER-HOTKEY.md`](docs/VISPER-HOTKEY.md) |
| `WORKFLOW/` | A standalone HTML workflow-demonstration page ("ORBIT"). | [`docs/WORKFLOW.md`](docs/WORKFLOW.md) |
| `HCJ-PortFolio/` | Personal portfolio website. Has its own `README.md`. Not documented further here since it's personal, not a technical component. | See the folder's own `README.md` |

## Repository hygiene

A few structural issues worth fixing independent of any documentation work; see [`docs/REPO_HYGIENE.md`](docs/REPO_HYGIENE.md) for detail:

- `PCI-Framework/` contains an accidental doubly-nested copy of itself (`PCI-Framework/PCI-Framework-main/`), duplicating every file one level deeper.
- `VISPER-HOTKEY/VISPER AMT MODELS/VISPER - DOCX TRANSITION.py` has a hardcoded, user-specific Windows path.

## CI

A shared `.github/workflows/ci.yml` lints each sub-project with the tooling appropriate to its language, triggered only on changes to that sub-project's own path (see the workflow file for the exact path filters). There is no unified build or test suite across the archive, since the folders don't share a runtime to build or test against.

## Contributing

This is a personal archive rather than a project soliciting outside contributions. If you're the maintainer picking this back up later: each sub-project's own doc (linked above) has enough context to resume work without re-deriving the folder's purpose from the code alone.

---

# License

ML-NEURL is distributed under the terms defined in `LICENSE`.
