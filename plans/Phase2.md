# PRD: Slate OS Phase 2 — Hyprland Compositor (GUI Foundation)

**Version:** Phase 2  
**Status:** Draft  
**Author:** Adam  
**Last Updated:** 2026-07-05

---

# Overview

Slate OS Phase 2 launches the **graphical environment** for the first time.

This milestone validates the single most important technical assumption of the entire project:

> Slate OS can boot into a stable graphical desktop environment.

The previous attempt at building Slate failed exactly here — the terminal worked, but the graphical environment never started reliably. This release exists solely to prove that blocker is overcome.

---

# Objective

Install and configure **Wayland + Hyprland** so that:

- the graphical session starts automatically after boot
- the desktop renders correctly inside QEMU
- the session is stable across repeated boots

A temporary auto-login is acceptable for this milestone. The real login screen arrives in Phase 8.

---

# Problem Statement

A working kernel is not enough. A working text console is not enough.

The project can only continue if Slate **reliably launches a graphical desktop** without crashes or rendering failures. This release answers exactly that question, in isolation, with no other features to distract from it.

---

# Users

Primary user:

- Adam (developer)

---

# Goals

- Wayland + Hyprland installed.
- Hyprland auto-configured by the Slate installer (gestures, drivers).
- Graphical session starts automatically after boot.
- Desktop renders correctly.
- No compositor crashes during normal operation.

---

# Functional Requirements

## FR-001

The system shall use **Wayland** as the display protocol.

---

## FR-002

The system shall use **Hyprland** as the compositor.

---

## FR-003

The Slate installer shall auto-configure Hyprland defaults:

- input
- output
- basic rendering

No manual editing of config files should be required for a working session.

---

## FR-004

The graphical session shall start **automatically** after boot.

A temporary auto-login is acceptable for this milestone.

---

## FR-005

The desktop shall render correctly inside QEMU:

- visible background
- responsive pointer
- correct resolution

---

## FR-006

The session shall be restartable without manual recovery.

---

# Non-Functional Requirements

## Stability

The system must complete ten consecutive boots **into the graphical session** without graphical failures.

---

## Reliability

No compositor crash is acceptable during basic testing.

---

## Performance

The desktop should become usable within approximately 15 seconds inside QEMU.

Exact optimization is out of scope.

---

## Maintainability

Configuration should remain minimal.

Prefer upstream Hyprland defaults whenever possible.

---

# Out of Scope

The following remain excluded from this milestone:

- GUI terminal emulator — Phase 3
- Official wallpaper and Slate branding — Phase 4
- Top bar / dock / launcher — Phase 5 → Phase 7
- Login screen (auto-login is used here) — Phase 8
- Boot animation — Phase 9
- Window controls styling (rounded corners, fill, minimize)
- Notifications
- Settings application
- Multi-monitor

---

# Success Criteria

The milestone is complete only if all conditions are met:

- Wayland + Hyprland installed and configured.
- Graphical session starts automatically after boot.
- Desktop renders correctly inside QEMU.
- Pointer and resolution behave correctly.
- No compositor crashes occur.
- Ten consecutive successful boots into the GUI are completed.

---

# Failure Criteria

The milestone is considered failed if any of the following occur:

- Black screen.
- Frozen desktop.
- Hyprland crash.
- Manual intervention required to reach the desktop.
- Rendering artifacts or wrong resolution.

---

# Validation Procedure

For every build:

1. Boot inside QEMU.
2. Wait until the graphical desktop appears.
3. Move the pointer.
4. Confirm correct resolution.
5. Restart the session.
6. Repeat ten times.

Every run must complete successfully without manual recovery.

---

# Risks

| Risk | Mitigation |
|------|------------|
| Hyprland instability | Keep configuration minimal, use upstream defaults |
| QEMU graphics issues | Test using virtio-gpu |
| Wayland configuration errors | Avoid custom config; prefer defaults |
| Auto-login regression | Auto-login is temporary; replaced by real login in Phase 8 |

---

# Deliverables

At the end of this milestone the project must provide:

- Wayland + Hyprland installation
- Auto-configured graphical session
- Correctly rendered desktop inside QEMU
- Stable graphical boot

The graphical foundation is now proven.

---

# Exit Criteria

When this document is fully satisfied, the project may proceed to:

**Slate OS Phase 3 — Terminal**

No additional GUI features should be added before this milestone is complete.
