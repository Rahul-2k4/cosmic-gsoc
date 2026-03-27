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
