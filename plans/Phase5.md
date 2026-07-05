# PRD: Slate OS Phase 5 — Top Bar

**Version:** Phase 5  
**Status:** Draft  
**Author:** Adam  
**Last Updated:** 2026-07-05

---

# Overview

Slate OS Phase 5 introduces the **top bar** — the first persistent desktop UI component.

The objective is a simple, always-visible bar at the top of the screen displaying a **live clock**. This is the first piece of the Slate desktop interface.

---

# Objective

Add a persistent top bar to the desktop that:

- stays visible during normal use
- displays the current system time
- updates the time automatically

---

# Problem Statement

The desktop currently shows only a wallpaper and applications. There is no persistent system interface.

The top bar is the first step in replacing Hyprland defaults with a desktop that behaves like Slate. It is intentionally minimal — only a clock for now.

---

# Users

Primary user:

- Adam (developer)

---

# Goals

- Display a persistent top bar.
- Show a live, automatically updating clock.
- Keep the bar minimal and lightweight.

---

# Functional Requirements

## FR-001 — Persistent Top Bar

A top bar shall be displayed at the top of the screen and remain visible during normal desktop usage.

---

## FR-002 — Live Clock

The top bar shall display the current system time.

---

## FR-003 — Automatic Update

The clock shall update automatically without user interaction.

---

## FR-004 — Correct Time

The displayed time shall match the system clock.

---

# Non-Functional Requirements

## Performance

The top bar shall not introduce noticeable lag.

---

## Stability

The top bar must not crash or disappear during normal use.

---

## Simplicity

Only the clock is shown. No additional indicators in this milestone.

---

# Out of Scope

The following remain excluded from this milestone (they belong to later phases or are out of MVP entirely):

- WiFi / Bluetooth icons and menus — OUT OF SCOPE for MVP.
- Weather indicator — OUT OF SCOPE for MVP.
- Battery / audio / network status indicators — OUT OF SCOPE for MVP.
- `_AppName_` switcher in the top bar — OUT OF SCOPE for MVP.
- Editable / draggable top bar, widgets, auto-hide.
- Calendar popup.

> The full top bar (WiFi, BT, weather, battery, `_AppName_`) is a post-MVP feature. For MVP, only the live clock is required.

---

# Design Principles

- minimal
- distraction-free
- consistent spacing
- predictable behavior

The bar should never feel visually cluttered.

---

# Success Criteria

The milestone is complete when:

- The top bar is displayed persistently.
- The clock displays the correct time.
- The clock updates automatically.
- No regression from Phase 4 is introduced.

---

# Failure Criteria

The milestone fails if:

- The top bar disappears unexpectedly.
- The clock shows the wrong time.
- The clock does not update.
- Existing desktop functionality regresses.

---

# Validation Procedure

1. Boot into the graphical session.
2. Verify the top bar is visible.
3. Verify the clock displays the correct time.
4. Wait and verify the clock updates automatically.
5. Launch and close the terminal to confirm no regression.

---

# Risks

| Risk | Mitigation |
|------|------------|
| Bar becomes too feature-rich | Limit to clock only |
| Performance degradation | Keep rendering lightweight |
| Scope creep | Exclude WiFi / BT / weather / battery |
| UI inconsistency | Follow the Slate design language |

---

# Deliverables

At the end of this milestone the project provides:

- Persistent Slate Top Bar
- Live Clock

The desktop now has its first persistent interface element.

---

# Exit Criteria

When this document is fully satisfied, the project may proceed to:

**Slate OS Phase 6 — Bottom Dock**
