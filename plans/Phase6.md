# PRD: Slate OS Phase 6 — Bottom Dock

**Version:** Phase 6  
**Status:** Draft  
**Author:** Adam  
**Last Updated:** 2026-07-05

---

# Overview

Slate OS Phase 6 introduces the **bottom dock** — a persistent bar at the bottom of the screen holding clickable application icons.

This is the second half of the desktop's persistent interface (after the top bar) and the primary way users launch applications without the terminal.

---

# Objective

Add a persistent bottom dock that:

- stays visible during normal use
- contains clickable icons
- launches pinned applications when an icon is clicked
- visually indicates running applications

---

# Problem Statement

There is currently no mouse-driven way to launch applications.

The dock provides the primary interaction model for opening apps, and prepares the ground for the launchpad (Phase 7).

---

# Users

Primary user:

- Adam (developer)

---

# Goals

- Display a persistent dock.
- Provide clickable icons.
- Launch applications from the dock.
- Indicate running applications visually.

---

# Functional Requirements

## FR-001 — Persistent Dock

A dock shall be displayed at the bottom of the screen and remain visible during normal desktop usage.

---

## FR-002 — Clickable Icons

The dock shall contain clickable application icons.

---

## FR-003 — Application Launch

Clicking a pinned icon shall launch the corresponding application.

Initially supported:

- Terminal

Future applications are added in later phases.

---

## FR-004 — Running Application Indicator

The dock shall visually indicate which applications are currently running.

Indicators follow the Slate convention:

- a long line under the icon → application is active (in focus)
- a dot under the icon → application is open but not active

---

## FR-005 — Separator

The dock shall include a vertical separator `|` between application shortcuts and the system area (where the Apps / launchpad icon will live in Phase 7).

---

# Non-Functional Requirements

## Performance

Clicking an icon should launch the application without noticeable delay.

---

## Stability

The dock must not crash during repeated launching and closing of applications.

---

## Simplicity

The dock launches applications only. Advanced features are excluded.

---

# Out of Scope

The following remain excluded from this milestone:

- The Apps / launchpad icon and launchpad itself — Phase 7.
- Slate Store entry (post-MVP).
- Open-at-login apps (post-MVP).
- Drag-and-drop reordering.
- Auto-hide.
- Search field — OUT OF SCOPE for MVP.

---

# Design Principles

- minimal
- predictable
- visually consistent with the top bar
- single responsibility (launch + indicate)

---

# Success Criteria

The milestone is complete when:

- The dock is displayed persistently.
- Icons are clickable.
- The Terminal launches from the dock.
- Running applications are visually indicated (line = active, dot = open).
- The separator is present.
- No regression from Phase 5 is introduced.

---

# Failure Criteria

The milestone fails if:

- The dock disappears unexpectedly.
- Applications fail to launch from the dock.
- Running indicators are missing or incorrect.
- Existing desktop functionality regresses.

---

# Validation Procedure

1. Boot into the graphical session.
2. Verify the dock is visible.
3. Click the Terminal icon.
4. Verify the Terminal launches.
5. Verify the active indicator (line) appears.
6. Close the Terminal.
7. Verify the indicator disappears.
8. Repeat several times.

---

# Risks

| Risk | Mitigation |
|------|------------|
| Dock becomes too feature-rich | Limit to launching + indicating |
| Incorrect running state | Sync dock state with the compositor |
| Performance degradation | Keep rendering lightweight |
| Scope creep | Exclude launchpad / search / store |

---

# Deliverables

At the end of this milestone the project provides:

- Persistent Slate Dock
- Clickable application icons
- Dock-based application launching
- Running application indicators (line / dot)
- Separator between apps and system area

Applications can now be launched with the mouse.

---

# Exit Criteria

When this document is fully satisfied, the project may proceed to:

**Slate OS Phase 7 — Launchpad**
