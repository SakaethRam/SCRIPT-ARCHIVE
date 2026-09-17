# VISPER-HOTKEY

Local workflow-automation utilities: AutoHotkey (AHK) scripts for hotkey-triggered actions, plus a couple of small Python helpers, built around the VISPER transcription/translation workflow documented in the ML-VISPER project.

## Files

### `VISPER x CURSOR.ahk`

Hotkey: `Ctrl+Shift+M`. When the active window is File Explorer, copies files from the current folder into specific target folders based on extension: `.mp4`/`.mov` → a Video Components folder, `.wav`/`.mp3`/`.xlsx` → an Audio Components folder. A simple, extension-based file router for organizing VISPER's input/output media without doing it by hand.

### `VISPER AMT MODELS/VISPER x DeepL.ahk`

Hotkey: `Ctrl+Shift+T`. Branded "ARKIN X AUTOMATION DOMAIN" in its header. Grabs selected text from the active window (specifically checks for Notepad), sends it through DeepL for translation, and returns the translated text, all without leaving the keyboard. This is the "quick manual translation check" counterpart to VISPER's own batch Whisper-based translation pipeline: useful for spot-checking a line rather than running the full notebook pipeline.

### `VISPER AMT MODELS/VISPER - SRT TRANSITION.py`

Not inspected in full here; based on the naming convention alongside the DOCX transition script below, presumably converts VISPER's timestamped output into `.srt` subtitle format. Confirm the exact input/output format against the source directly before relying on this description.

### `VISPER AMT MODELS/VISPER - DOCX TRANSITION.py`

Converts `.srt` files into `.docx` documents: reads every `.srt` file from a source folder, writes each line as a paragraph into a new Word document, and saves it to an output folder.

**Hardcoded paths, worth fixing:**

```python
SRT_FOLDER = r"C:\Users\sakae\VISPER - Translation Model\SRT Files"
DOCX_FOLDER = r"C:\Users\sakae\VISPER - Translation Model\SRT - DOCX"
```

These are absolute, user-specific Windows paths baked into the script. Two practical problems this causes:

1. **Not portable** — the script only runs correctly on the machine (and user account) these exact paths exist on.
2. **Minor information exposure** — the Windows username (`sakae`) is visible in the committed source. Low sensitivity on its own, but worth cleaning up as a matter of habit, the same way hardcoded API keys are worth cleaning up in other projects in this archive.

**Suggested fix:**

```python
import os

SRT_FOLDER = os.environ.get("VISPER_SRT_FOLDER", os.path.join(os.getcwd(), "SRT Files"))
DOCX_FOLDER = os.environ.get("VISPER_DOCX_FOLDER", os.path.join(os.getcwd(), "SRT - DOCX"))
```

or, more simply, accept both as command-line arguments via `argparse` so the script runs correctly on any machine without editing source.

## Why these are AHK scripts, not Python

AutoHotkey is specifically built for global hotkeys and Windows UI automation (reading the active window, simulating keystrokes/clipboard actions) in a way that's considerably more direct on Windows than equivalent Python (`pyautogui` or similar) would be. Since this whole VISPER-HOTKEY folder is Windows-specific local tooling rather than a cross-platform deliverable, AHK is a reasonable fit here, unlike in a project meant to be shared or deployed elsewhere.
