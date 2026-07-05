# PRD: Slate OS Phase 7 — Launchpad

**Version:** Phase 7  
**Status:** Draft  
**Author:** Adam  
**Last Updated:** 2026-07-05

---

# Overview

Slate OS Phase 7 introduces the **Launchpad** — a full-screen grid view of all installed applications, opened from the dock.

This completes the primary application workflow: users can now browse, discover and launch any installed graphical application without the terminal or keyboard shortcuts.

---

# Objective

Provide a launchpad that:

- opens from the Apps icon in the dock
- displays all installed graphical applications in a grid
- uses a blur transition when opening
- launches the selected application and closes itself

---

# Problem Statement

The dock (Phase 6) only holds pinned applications. Users have no way to see or launch applications that are not pinned.

The launchpad is the standard Slate way to discover and open any installed application.

---

# Users

Primary user:

- Adam (developer)

---

# Goals

- Add the Apps icon to the dock.
- Open a launchpad view from that icon.
- Show all installed graphical applications in a grid.
- Use a blur transition when the launchpad appears.
- Launch applications from the launchpad.

---

# Functional Requirements

## FR-001 — Apps Icon

An Apps icon shall be present in the dock, on the system side of the separator.

---

## FR-002 — Launchpad Activation

Clicking the Apps icon shall open the Launchpad.

---

## FR-003 — Application Grid

The Launchpad shall display all installed graphical applications in a grid layout.

Each application shall display:

- icon
- name

Folders are out of scope.

---

## FR-004 — Blur Transition

The Launchpad shall open with a blur transition (the desktop blurs as the grid appears).

---

## FR-005 — Launch Application

Selecting an application shall launch it.

The Launchpad shall close automatically after launch.

---

## FR-006 — Close Launchpad

The Launchpad shall be closable without launching anything (e.g. clicking outside, pressing Escape).

---

# Non-Functional Requirements

## Performance

The Launchpad should open within approximately 300 ms.

---

## Stability

The Launchpad must not crash during repeated opening and closing.

---

## Adaptability

The grid shall adapt to the screen resolution.

---

# Out of Scope

The following remain excluded from this milestone:

- Search inside the launchpad — OUT OF SCOPE for MVP.
- Categories and folders.
- Favorites management.
- Drag-and-drop organization.
- Slate Store integration (post-MVP).
- Custom window controls styling (rounded corners, fill, minimize).

---

# Design Principles

- minimal
- distraction-free
- visually consistent (macOS Sequoia-style grid)
- single responsibility (browse + launch)

Users should understand how to launch an application immediately.

---

# Success Criteria

The milestone is complete when:

- The Apps icon is present in the dock.
- Clicking it opens the Launchpad.
- The grid shows all installed graphical applications.
- A blur transition is used when opening.
- Selecting an application launches it and closes the Launchpad.
- The Launchpad can be closed without launching anything.
- No regression from Phase 6 is introduced.

---

# Failure Criteria

The milestone fails if:

- The Launchpad fails to open.
- Applications cannot be launched from it.
- The blur transition is missing or janky.
- The Launchpad does not close after launch.
- Existing desktop functionality regresses.

---

# Validation Procedure

1. Boot into the graphical session.
2. Click the Apps icon in the dock.
3. Verify the Launchpad opens with a blur transition.
4. Verify all installed applications are shown in the grid.
5. Select the Terminal.
6. Verify the Terminal launches and the Launchpad closes.
7. Open the Launchpad again and close it without launching.
8. Repeat several times.

---

# Risks

| Risk | Mitigation |
|------|------------|
| Launchpad becomes overly complex | Focus on browse + launch only |
| Blur transition performance | Use compositor-native blur |
| Grid does not adapt | Auto-layout based on resolution |
| Scope creep | Exclude search / categories / folders |

---

# Deliverables

At the end of this milestone the project provides:

- Apps icon in the dock
- Slate Launchpad (grid of all applications)
- Blur transition
- Application launching from the grid
- Automatic close after launch

Slate OS can now be operated fully with the mouse.

---

# Exit Criteria

When this document is fully satisfied, the project may proceed to:

**Slate OS Phase 8 — Login Screen**
