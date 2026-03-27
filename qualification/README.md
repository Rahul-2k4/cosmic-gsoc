# Regolith COSMIC Qualification Evidence

This folder holds the screenshots and walkthrough GIF that back the qualification section of my GSoC proposal for a COSMIC-based Regolith session.

The main proposal image is `hero-proof.png`. The rest of the files are supporting proof for reviewers who want the narrower terminal check, the separate OSD shot, or the full walkthrough.

## What Each File Shows

| File | What it proves | Notes |
|---|---|---|
| `screenshots/hero-proof.png` | The session is live, `cosmic-settings` is open in-session, `cosmic-osd` is rendering, and the terminal shows the core COSMIC-side processes together with `gnome-session-bin: (none)`. | This is the best reviewer-facing screenshot because it puts the runtime proof, the settings app, and the OSD in one frame. |
| `screenshots/terminal-proof-final.png` | The experimental session is running with `cosmic-session`, `sway`, `trawld`, `cosmic-settings-daemon`, and `cosmic-osd`. It also shows that `gnome-session-bin` is not in the session path. | This is the terminal proof I want reviewers to use, not the older compressed screenshot. It is intentionally narrow: the current runtime still has GNOME helper processes such as `gnome-session-ctl --monitor`, so I am not claiming that every GNOME-related process is gone. |
| `screenshots/xdg-desktop-token.png` | `XDG_CURRENT_DESKTOP` is `Regolith-Wayland:COSMIC:sway` with no `GNOME` token. | Directly proves the GNOME decoupling thesis. The old session path set this to `Regolith-Wayland:GNOME:sway`. |
| `screenshots/cosmolith-process.png` | The cosmolith daemon is running in the live COSMIC session. | Backs the proposal claim at line 290 that cosmolith is part of the running session. |
| `screenshots/keyboard-input-proof.png` | Sway's input state reflects keyboard config applied from `cosmic-config` via cosmolith. | Ties to PR #15 and the Phase 2 keyboard data flow described in the proposal. |
| `screenshots/desktop-osd.png` | `cosmic-osd` is working in the live session. | This is the clearest visual proof in the set. |
| `screenshots/cosmic-settings-proof.png` | `cosmic-settings` is running inside the Regolith COSMIC session. | Sound page shown in-session. |
| `screenshots/demo-recording.gif` | A full walkthrough of the qualification environment. | Best overall proof artifact, but better as a hosted link than an inline image in the proposal PDF. |
| `screenshots/desktop-clean.png` | Clean desktop view of the session. | Useful as supporting context, but weaker than the OSD screenshot and the walkthrough. |
| `screenshots/greetd-login.png` | The session is available from the greeter. | Supporting evidence only. |
| `screenshots/lockscreen.png` | The current lock path uses `gtklock`. | This matches the current `swayidle` + `gtklock` setup described in the proposal. |
