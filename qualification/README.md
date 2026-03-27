# Regolith COSMIC Qualification Evidence

This repository hosts the screenshot and walkthrough evidence referenced by the GSoC proposal for building a COSMIC-based Wayland session for Regolith.

## Evidence Map

| File | Claim Supported | Strength | Notes |
|---|---|---|---|
| `screenshots/terminal-proof-final.png` | Core session processes are live in the experimental session: `cosmic-session`, `sway`, `trawld`, `cosmic-settings-daemon`, `cosmic-osd` | Strong | Also shows `gnome-session-bin` absent. The current runtime still has GNOME helper processes such as `gnome-session-ctl --monitor`, so the narrow `gnome-session-bin` claim is the accurate one. |
| `screenshots/desktop-osd.png` | `cosmic-osd` volume overlay renders in the live session | Strong | Clear in-session OSD proof with status bar visible. |
| `screenshots/cosmic-settings-proof.png` | `cosmic-settings` runs inside the Regolith COSMIC session | Strong | Sound page visible in the live session. |
| `screenshots/demo-recording.gif` | End-to-end walkthrough of the qualification environment | Strong | Best holistic proof artifact; kept as hosted evidence rather than inline proposal media. |
| `screenshots/desktop-clean.png` | Clean desktop view of the session | Supporting | Useful context, but redundant with stronger OSD and walkthrough evidence. |
| `screenshots/greetd-login.png` | Session is available from the greeter/login flow | Supporting | Kept as supporting evidence only. |
| `screenshots/lockscreen.png` | Current lock path uses `gtklock` | Supporting | Honest proof for the current `swayidle` + `gtklock` lock path. |

## Proposal Notes

- The proposal should use `terminal-proof-final.png` as the current terminal-proof artifact instead of the older compressed `terminal-proof.png`.
- For the terminal proof, the accurate claim is:
  - core COSMIC session processes are live
  - `gnome-session-bin` is absent
- Avoid broader wording such as "`pgrep gnome-session` returns empty", because the current runtime still includes GNOME helper processes.
