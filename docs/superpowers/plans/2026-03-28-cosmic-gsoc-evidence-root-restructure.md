# cosmic-gsoc Evidence Root Restructure Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Flatten the public evidence repo so reviewers land on a root proof index, with all evidence media under `screenshots/` and no active dependency on `qualification/`.

**Architecture:** Keep the repo simple: move the evidence artifacts from `qualification/screenshots/` to root `screenshots/`, promote the root `README.md` into the main proof table, and delete `qualification/README.md`. Update the active proposal link so it points to the repo root instead of the old `qualification/` path. Historical planning/spec docs keep their old path references because they describe past state.

**Tech Stack:** Git, Markdown, shell file moves, GitHub repo structure

---

## File Structure

**Files:**
- Create: `screenshots/`
- Modify: `README.md`
- Delete: `qualification/README.md`
- Move: `qualification/screenshots/*.png`
- Move: `qualification/screenshots/*.gif`
- Modify: `/Users/rahul/My_vault/GSOC 2026/ccextractor/03_Regolith_COSMIC_Session/PROPOSAL_FINAL.md`

Artifacts to move:

- `qualification/screenshots/hero-proof.png`
- `qualification/screenshots/terminal-proof-final.png`
- `qualification/screenshots/xdg-desktop-token.png`
- `qualification/screenshots/cosmolith-process.png`
- `qualification/screenshots/keyboard-input-proof.png`
- `qualification/screenshots/desktop-osd.png`
- `qualification/screenshots/cosmic-settings-proof.png`
- `qualification/screenshots/demo-recording.gif`
- `qualification/screenshots/desktop-clean.png`
- `qualification/screenshots/greetd-login.png`
- `qualification/screenshots/lockscreen.png`

Target layout:

```text
cosmic-gsoc/
├── README.md
├── screenshots/
│   ├── hero-proof.png
│   ├── terminal-proof-final.png
│   ├── xdg-desktop-token.png
│   ├── cosmolith-process.png
│   ├── keyboard-input-proof.png
│   └── ...
└── docs/superpowers/
    ├── specs/
    └── plans/
```

---

## Task 1: Create Isolated Worktree

**Files:**
- No repo file changes expected in this task

- [ ] **Step 1: Verify `.worktrees/` is ignored**

Run:

```bash
git -C /Users/rahul/Desktop/Gsoc/cosmic-gsoc check-ignore -q .worktrees
```

Expected: exit code `0`

- [ ] **Step 2: Create a dedicated worktree**

Run:

```bash
git -C /Users/rahul/Desktop/Gsoc/cosmic-gsoc worktree add /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure -b evidence-root-restructure
```

Expected: new worktree created from current `main`

- [ ] **Step 3: Verify clean baseline in the worktree**

Run:

```bash
git -C /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure status --short --branch
find /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/qualification/screenshots -maxdepth 1 -type f | sed 's#.*/##' | sort
```

Expected: clean branch status and 11 evidence artifacts listed

---

## Task 2: Move Evidence Artifacts To Root `screenshots/`

**Files:**
- Create: `screenshots/`
- Move: all files from `qualification/screenshots/` to `screenshots/`

- [ ] **Step 1: Create the target directory**

Run:

```bash
mkdir -p /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/screenshots
```

- [ ] **Step 2: Move the evidence artifacts**

Run:

```bash
mv /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/qualification/screenshots/hero-proof.png /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/screenshots/
mv /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/qualification/screenshots/terminal-proof-final.png /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/screenshots/
mv /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/qualification/screenshots/xdg-desktop-token.png /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/screenshots/
mv /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/qualification/screenshots/cosmolith-process.png /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/screenshots/
mv /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/qualification/screenshots/keyboard-input-proof.png /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/screenshots/
mv /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/qualification/screenshots/desktop-osd.png /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/screenshots/
mv /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/qualification/screenshots/cosmic-settings-proof.png /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/screenshots/
mv /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/qualification/screenshots/demo-recording.gif /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/screenshots/
mv /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/qualification/screenshots/desktop-clean.png /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/screenshots/
mv /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/qualification/screenshots/greetd-login.png /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/screenshots/
mv /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/qualification/screenshots/lockscreen.png /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/screenshots/
```

- [ ] **Step 3: Verify the new folder contents and the old folder state**

Run:

```bash
find /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/screenshots -maxdepth 1 -type f | sed 's#.*/##' | sort
find /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/qualification/screenshots -maxdepth 1 -type f | sed 's#.*/##' | sort
```

Expected: 11 files listed in `screenshots/`; no files listed in `qualification/screenshots/`

---

## Task 3: Rewrite Root README As The Proof Index

**Files:**
- Modify: `README.md`

- [ ] **Step 1: Replace the root README with the proof-first index**

Write this content to `/Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/README.md`:

```markdown
# cosmic-gsoc

Qualification evidence and supporting artifacts for my GSoC 2026 proposal: **Build a COSMIC-based Wayland Session for Regolith** (CCExtractor).

`screenshots/hero-proof.png` is the best single reviewer-facing image in this repo. It combines the live session, `cosmic-settings`, `cosmic-osd`, and terminal runtime proof in one frame.

## Proof Index

| File | Claim it supports | How to use it |
|---|---|---|
| `screenshots/hero-proof.png` | The experimental Regolith COSMIC session is live, `cosmic-settings` is open in-session, `cosmic-osd` is rendering, and the terminal shows the core COSMIC-side processes together with `gnome-session-bin: (none)`. | Best single image for reviewers. |
| `screenshots/terminal-proof-final.png` | The experimental session is running with `cosmic-session`, `sway`, `trawld`, `cosmic-settings-daemon`, and `cosmic-osd`. It also shows that `gnome-session-bin` is not in the session path. | Narrow runtime proof. This does not claim every GNOME-related helper process is gone. |
| `screenshots/xdg-desktop-token.png` | `XDG_CURRENT_DESKTOP` is `Regolith-Wayland:COSMIC:sway` with no `GNOME` token. | Direct proof for the GNOME-decoupling claim. |
| `screenshots/cosmolith-process.png` | The `cosmolith` daemon is running in the live COSMIC session. | Direct runtime proof that the bridge process is up. |
| `screenshots/keyboard-input-proof.png` | Sway's input state reflects the running keyboard configuration. | Supports the `cosmic-config -> cosmolith -> Sway` path, but does not by itself prove every layout-switching or variant case is solved. |
| `screenshots/desktop-osd.png` | `cosmic-osd` is working in the live session. | Best standalone OSD proof. |
| `screenshots/cosmic-settings-proof.png` | `cosmic-settings` is running inside the Regolith COSMIC session. | Standalone settings-app proof. |
| `screenshots/demo-recording.gif` | A full walkthrough of the qualification environment. | Best complete walkthrough artifact. |
| `screenshots/desktop-clean.png` | Clean desktop view of the session. | Supporting visual context only. |
| `screenshots/greetd-login.png` | The session is available from the greeter. | Supporting evidence only. |
| `screenshots/lockscreen.png` | The tested lock path uses `gtklock`. | Supporting evidence for the current lock path. |

## How To Read This Repo

- Start with `screenshots/hero-proof.png` if you want the strongest single screenshot.
- Use `screenshots/terminal-proof-final.png`, `screenshots/xdg-desktop-token.png`, `screenshots/cosmolith-process.png`, and `screenshots/keyboard-input-proof.png` for narrower runtime claims.
- Treat the remaining images and GIF as supporting evidence, not stronger replacements for the primary proof.
```

- [ ] **Step 2: Verify the README formatting**

Run:

```bash
sed -n '1,220p' /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/README.md
git -C /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure diff --check
```

Expected: table renders cleanly in plain Markdown; `git diff --check` exits `0`

---

## Task 4: Remove The Old Qualification Index And Update Active Dependent Links

**Files:**
- Delete: `qualification/README.md`
- Modify: `/Users/rahul/My_vault/GSOC 2026/ccextractor/03_Regolith_COSMIC_Session/PROPOSAL_FINAL.md`

- [ ] **Step 1: Delete the obsolete qualification README**

Delete:

```text
/Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/qualification/README.md
```

- [ ] **Step 2: Remove the now-empty `qualification/` directory if possible**

Run:

```bash
rmdir /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/qualification/screenshots 2>/dev/null || true
rmdir /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/qualification 2>/dev/null || true
```

- [ ] **Step 3: Update the active proposal link to the repo root**

In `/Users/rahul/My_vault/GSOC 2026/ccextractor/03_Regolith_COSMIC_Session/PROPOSAL_FINAL.md`, replace:

```markdown
[Rahul-2k4/cosmic-gsoc](https://github.com/Rahul-2k4/cosmic-gsoc/tree/main/qualification)
```

with:

```markdown
[Rahul-2k4/cosmic-gsoc](https://github.com/Rahul-2k4/cosmic-gsoc)
```

- [ ] **Step 4: Verify no active navigation depends on `qualification/`**

Run:

```bash
rg -n "tree/main/qualification|qualification/screenshots|\\[qualification/\\]" /Users/rahul/Desktop/Gsoc/cosmic-gsoc /Users/rahul/My_vault/GSOC\ 2026/ccextractor/03_Regolith_COSMIC_Session/PROPOSAL_FINAL.md --glob '!docs/superpowers/**'
```

Expected: no matches

Note: `docs/superpowers/**` is intentionally excluded because those files are historical planning/spec artifacts.

---

## Task 5: Verify Final State, Commit, And Publish

**Files:**
- All moved screenshots
- `README.md`
- Deleted `qualification/README.md`
- `/Users/rahul/My_vault/GSOC 2026/ccextractor/03_Regolith_COSMIC_Session/PROPOSAL_FINAL.md`

- [ ] **Step 1: Verify final worktree state**

Run:

```bash
find /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure/screenshots -maxdepth 1 -type f | wc -l
git -C /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure status --short --branch
```

Expected: `11` evidence files in `screenshots/`; git status shows the move set plus README changes

- [ ] **Step 2: Commit the repo restructure**

Run:

```bash
git -C /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure add README.md screenshots qualification/README.md
git -C /Users/rahul/Desktop/Gsoc/cosmic-gsoc/.worktrees/evidence-root-restructure commit -m "Flatten evidence repo structure and promote root proof index"
```

Expected: commit created on branch `evidence-root-restructure`

- [ ] **Step 3: Fast-forward `main` and push**

Run:

```bash
git -C /Users/rahul/Desktop/Gsoc/cosmic-gsoc merge --ff-only evidence-root-restructure
git -C /Users/rahul/Desktop/Gsoc/cosmic-gsoc push origin main
```

Expected: `main` updated and pushed

- [ ] **Step 4: Verify the pushed GitHub structure**

Run:

```bash
gh api repos/Rahul-2k4/cosmic-gsoc/contents/README.md --jq '.name'
gh api repos/Rahul-2k4/cosmic-gsoc/contents/screenshots --jq '.[].name'
```

Expected: `README.md` returned; screenshot listing contains the 11 moved artifacts

---

## Implementation Notes

- Do not rewrite or “fix” historical docs under `docs/superpowers/` just to remove old `qualification/` references. Those files describe earlier repo state and should remain historically accurate.
- Keep the proof wording tight. `keyboard-input-proof.png` supports the input path, but it is not proof that all keyboard-layout and variant work is complete.
- Do not rename evidence files during the move. Only the directory prefix should change.
