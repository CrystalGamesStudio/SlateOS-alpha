# PRD: Slate OS Phase 3 — Terminal

**Version:** Phase 3  
**Status:** Draft  
**Author:** Adam  
**Last Updated:** 2026-07-05

---

# Overview

Slate OS Phase 3 introduces the first **graphical application**: a terminal emulator.

Now that the graphical session is stable (Phase 2), this milestone proves that an application can be launched inside the desktop, accept input, run commands and be closed normally.

---

# Objective

Provide a working terminal emulator that runs natively inside the Hyprland session.

The terminal is the primary tool used to validate the rest of the desktop in later milestones.

---

# Problem Statement

A desktop that cannot launch any application is not yet usable.

The terminal is the simplest meaningful application — if it launches and works inside the graphical session, the rest of the application pipeline is proven.

---

# Users

Primary user:

- Adam (developer)

---

# Goals

- Install a default terminal emulator.
- Terminal launches inside the Hyprland session.
- Terminal accepts keyboard input and executes commands.
- Terminal can be closed normally using the window close control (●).

---

# Functional Requirements

## FR-001

The system shall include a default terminal emulator compatible with Hyprland (e.g. Foot or Kitty).

---

## FR-002

The terminal shall launch successfully inside the graphical session.

---

## FR-003

The terminal shall accept keyboard input.

---

## FR-004

The terminal shall execute shell commands and display their output.

---

## FR-005

The terminal window shall be closable using the close control (●).

---

## FR-006

The terminal shall be reopenable after being closed.

---

# Non-Functional Requirements

## Performance

The terminal should launch within approximately one second.

---

## Stability

The terminal must not crash during normal command execution.

---

## Reliability

Closing and reopening the terminal must work repeatedly without session instability.

---

# Out of Scope

The following remain excluded from this milestone:

- Custom Slate-branded terminal (this is the default upstream terminal).
- Multiple tabs / split panes.
- Terminal configuration UI.
- Window controls beyond close (●) — minimize / maximize arrive later.
- Launcher / dock integration — Phase 6 / Phase 7.

---

# Success Criteria

The milestone is complete only if all conditions are met:

- Terminal is installed.
- Terminal launches inside the graphical session.
- Keyboard input works.
- Shell commands execute and produce output.
- Terminal closes via ●.
- Terminal can be reopened after closing.
- No regression from Phase 2.

---

# Failure Criteria

The milestone is considered failed if any of the following occur:

- Terminal cannot launch.
- Keyboard input is not received.
- Commands do not execute.
- Closing the terminal crashes the session.
- The graphical session regresses.

---

# Validation Procedure

For every build:

1. Boot into the graphical session.
2. Launch the terminal.
3. Type a basic command (e.g. `echo`, `ls`).
4. Verify the output is correct.
5. Close the terminal using ●.
6. Reopen the terminal.
7. Repeat several times.

Every run must complete successfully.

---

# Risks

| Risk | Mitigation |
|------|------------|
| Terminal incompatibility with Hyprland | Use a known-compatible terminal (Foot / Kitty) |
| Input not reaching the terminal | Verify keyboard config in Hyprland |
| Close control misconfigured | Bind ● to standard window close |

---

# Deliverables

At the end of this milestone the project must provide:

- Default terminal emulator installed
- Working terminal inside the graphical session
- Functional close control (●)

The desktop can now launch and run an application.

---

# Exit Criteria

When this document is fully satisfied, the project may proceed to:

**Slate OS Phase 4 — Wallpaper & Branding**
