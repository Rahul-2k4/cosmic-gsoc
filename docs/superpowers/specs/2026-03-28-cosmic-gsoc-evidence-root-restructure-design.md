# cosmic-gsoc Evidence Root Restructure Design

## Goal

Flatten the public evidence repo so the main GitHub landing page is the reviewer-facing proof index. Evidence media should live under a root `screenshots/` directory instead of `qualification/screenshots/`, and the root `README.md` should map each artifact to the claim it supports.

## Why This Change

The current repo works, but it makes a reviewer click into `qualification/` before the evidence becomes understandable. The user wants the default repo landing page to do that job directly.

The new shape should:

- make the root page the primary proof guide
- keep the repo structure simple and obvious
- map each image or GIF to a specific claim
- stay honest about proof strength, especially for keyboard/input claims

## Scope

In scope:

- move reviewer-facing media from `qualification/screenshots/` to `screenshots/`
- rewrite root `README.md` as the main proof index
- remove `qualification/README.md`
- update internal links and paths so the repo no longer depends on `qualification/`

Out of scope:

- changing the proposal body image choice (`hero-proof.png` remains the main proposal image)
- changing screenshot contents
- adding new screenshots or new runtime claims
- reorganizing unrelated repo content

## Target Repository Layout

Current:

```text
cosmic-gsoc/
├── README.md
└── qualification/
    ├── README.md
    └── screenshots/
        ├── hero-proof.png
        ├── terminal-proof-final.png
        ├── xdg-desktop-token.png
        ├── cosmolith-process.png
        ├── keyboard-input-proof.png
        └── ...
```

Target:

```text
cosmic-gsoc/
├── README.md
└── screenshots/
    ├── hero-proof.png
    ├── terminal-proof-final.png
    ├── xdg-desktop-token.png
    ├── cosmolith-process.png
    ├── keyboard-input-proof.png
    └── ...
```

## Root README Design

The root `README.md` becomes the main reviewer entry point. It should be short, skimmable, and proof-first.

Recommended structure:

1. Title and one-sentence repo purpose
2. Short note that `hero-proof.png` is the best single reviewer-facing image
3. Main proof table mapping artifact -> claim -> limitation or use
4. Short “How to read this repo” note that distinguishes strongest proof from supporting visuals

The page should not become a long narrative. It should behave like an evidence index.

## Proof Mapping Rules

The table should group artifacts by what they prove, not by capture order.

Required claim handling:

- `hero-proof.png`
  - Primary reviewer-facing image
  - Shows the live session, settings app, OSD, and terminal runtime proof in one frame

- `terminal-proof-final.png`
  - Narrow runtime proof
  - Confirms core COSMIC-side session processes and absence of `gnome-session-bin`
  - Must keep the existing caveat that this does not prove every GNOME-related helper process is gone

- `xdg-desktop-token.png`
  - Proves `XDG_CURRENT_DESKTOP=Regolith-Wayland:COSMIC:sway`
  - Supports the GNOME-decoupling claim

- `cosmolith-process.png`
  - Proves `cosmolith` is running in the live session

- `keyboard-input-proof.png`
  - Proves live Sway input state is present and reflects the running keyboard configuration
  - Supports the `cosmic-config -> cosmolith -> Sway` path
  - Must not be described as proof that all keyboard switching and variant cases are fully solved

- `desktop-osd.png`
  - Proves COSMIC OSD rendering

- `cosmic-settings-proof.png`
  - Proves `cosmic-settings` is running in-session

- `demo-recording.gif`
  - Full walkthrough artifact

- `desktop-clean.png`, `greetd-login.png`, `lockscreen.png`
  - Supporting evidence only

## File Moves

Implementation should move every file currently in `qualification/screenshots/` into root `screenshots/` without renaming the individual artifacts.

That keeps external references predictable and avoids unnecessary churn beyond the path prefix change.

## Link and Path Updates

The following path surfaces must be updated:

- root `README.md` links to `screenshots/...`
- any remaining internal references in repo docs that still point to `qualification/`

The final repo should not require `qualification/README.md` for navigation.

## Deletion Rules

Delete `qualification/README.md` once its proof-mapping content has been incorporated into root `README.md`.

If the `qualification/` directory becomes empty after the move, remove it as well.

## Verification

Before calling the restructure complete:

- verify root `README.md` reads cleanly in plain Markdown
- verify `screenshots/` contains every moved artifact
- verify there are no stale `qualification/screenshots/` links left in the repo
- verify GitHub root landing behavior is now correct in principle: reviewer lands on root `README.md` and can reach each artifact directly from there

## Risks

- Broken links after path changes
  - Mitigation: grep for `qualification/` references after the move

- Overclaiming the input proof
  - Mitigation: preserve the narrower wording for `keyboard-input-proof.png`

- README becoming too narrative
  - Mitigation: keep the root page table-first and concise

## Non-Goals

- No proposal prose rewrite beyond path relevance in the evidence repo
- No new subpages unless implementation reveals a strong need
- No screenshot renaming unless a technical constraint forces it

## Recommended Implementation Shape

One implementation pass should be enough:

1. create root `screenshots/`
2. move artifacts from `qualification/screenshots/` to `screenshots/`
3. rewrite root `README.md` as the proof index
4. remove `qualification/README.md`
5. verify paths and leftover references

This is intentionally simple. The repo should end up flatter, easier to scan, and still precise about what each artifact proves.
