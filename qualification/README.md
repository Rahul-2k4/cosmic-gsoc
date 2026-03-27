# Regolith COSMIC Qualification Evidence

This folder holds the screenshots and walkthrough GIF linked from my GSoC proposal for building a COSMIC-based Wayland session for Regolith.

I kept this repo simple on purpose: each file here backs a specific claim in the proposal, and the notes below say what it proves and what it does not.

## What Each File Shows

| File | What it proves | Notes |
|---|---|---|
| `screenshots/terminal-proof-final.png` | The experimental session is running with `cosmic-session`, `sway`, `trawld`, `cosmic-settings-daemon`, and `cosmic-osd`. It also shows that `gnome-session-bin` is not in the session path. | This is the terminal proof I want reviewers to use, not the older compressed screenshot. It is intentionally narrow: the current runtime still has GNOME helper processes such as `gnome-session-ctl --monitor`, so I am not claiming that every GNOME-related process is gone. |
| `screenshots/desktop-osd.png` | `cosmic-osd` is working in the live session. | This is the clearest visual proof in the set. |
| `screenshots/cosmic-settings-proof.png` | `cosmic-settings` is running inside the Regolith COSMIC session. | Sound page shown in-session. |
| `screenshots/demo-recording.gif` | A full walkthrough of the qualification environment. | Best overall proof artifact, but better as a hosted link than an inline image in the proposal PDF. |
| `screenshots/desktop-clean.png` | Clean desktop view of the session. | Useful as supporting context, but weaker than the OSD screenshot and the walkthrough. |
| `screenshots/greetd-login.png` | The session is available from the greeter. | Supporting evidence only. |
| `screenshots/lockscreen.png` | The current lock path uses `gtklock`. | This matches the current `swayidle` + `gtklock` setup described in the proposal. |
