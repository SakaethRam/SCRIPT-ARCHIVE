# Repository Hygiene

Two structural issues found while reviewing this archive, independent of the documentation itself.

## 1. `PCI-Framework/` contains an accidental doubly-nested copy of itself

The actual folder structure is:

```
PCI-Framework/
├── AGENT/
├── AGENTS.md
├── CAPSTONE.md
├── Dockerfile
├── README.md
├── requirements.txt
├── src/
└── PCI-Framework-main/          ← duplicate
    ├── AGENT/
    ├── AGENTS.md
    ├── CAPSTONE.md
    ├── Dockerfile
    ├── README.md
    ├── requirements.txt
    └── src/
```

Every file exists twice: once at `PCI-Framework/`, and again nested one level deeper at `PCI-Framework/PCI-Framework-main/`. This is a classic "downloaded a zip of the repo, extracted it into itself, and committed the result" mistake — `PCI-Framework-main` is exactly the folder name GitHub's own "Download ZIP" feature produces.

**Fix:**

```bash
cd PCI-Framework
# Confirm the nested copy is identical before deleting (it should be):
diff -rq . PCI-Framework-main --exclude=PCI-Framework-main

# If diff shows no differences, remove the duplicate:
rm -rf PCI-Framework-main
git add -A
git commit -m "Remove accidental doubly-nested PCI-Framework-main copy"
```

Run the `diff` check first rather than deleting blindly — if the two copies have actually diverged (e.g. one was edited after the duplicate was created), you'd want to know which one has the newer changes before discarding either.

## 2. Hardcoded user-specific path in `VISPER-HOTKEY`

Covered in full in `docs/VISPER-HOTKEY.md`: `VISPER - DOCX TRANSITION.py` has `C:\Users\sakae\...` baked into the source. Low-severity (it's a local automation script, not a shared service), but worth fixing for portability and to keep the habit consistent with how credentials get parameterized elsewhere in this author's other repositories.

## Why these are worth fixing even though nothing is broken today

Neither issue causes a functional problem right now: the duplicate folder just wastes repository size and could cause confusion about which copy is the "real" one if someone edits the wrong one; the hardcoded path only matters if the script runs on a different machine. Both are the kind of small papercut that gets more annoying the longer they sit, so fixing them now (while the cause is fresh and obvious) is cheaper than debugging "why did my edit not take effect" or "why doesn't this run on my laptop" months from now.
