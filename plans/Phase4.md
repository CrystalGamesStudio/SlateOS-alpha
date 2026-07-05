# PRD: Slate OS Phase 4 — Wallpaper & Branding

**Version:** Phase 4  
**Status:** Draft  
**Author:** Adam  
**Last Updated:** 2026-07-05

---

# Overview

Slate OS Phase 4 introduces the first **visual identity** of the operating system.

The previous milestone validated the graphical foundation and a working application. This release transforms the generic Linux desktop into an environment that is immediately recognizable as Slate OS.

No new functionality is introduced. The purpose of this milestone is visual consistency and first impressions only.

---

# Objective

Apply official Slate branding to the desktop:

- official Slate wallpaper (PNG/JPG with the Slate logo)
- Slate logo assets
- a minimal, consistent visual base for future UI

---

# Problem Statement

Although the desktop now works, it still looks like a default Hyprland installation.

Without a unique visual identity Slate is difficult to distinguish, screenshots are generic, and UI consistency cannot be evaluated. This milestone solves that.

---

# Users

Primary user:

- Adam (developer)

Secondary users:

- Early testers
- Designers
- Contributors

---

# Goals

- Bundle the official Slate wallpaper.
- Apply the wallpaper automatically.
- Ensure the wallpaper scales correctly.
- Remove all placeholder / generic assets.

---

# Functional Requirements

## FR-001 — Official Wallpaper

The official Slate wallpaper (PNG/JPG containing the Slate logo, provided by Adam) shall be bundled with the system.

---

## FR-002 — Automatic Wallpaper

The wallpaper shall load automatically on session start.

No manual command should be required to display it.

---

## FR-003 — Correct Scaling

The wallpaper shall scale correctly across common resolutions inside QEMU.

---

## FR-004 — Slate Logo Assets

Slate logo assets shall be bundled and available for use by future UI components (boot screen, login, launcher).

---

## FR-005 — No Placeholders

No placeholder logos, sample images or generic branding shall remain visible on the desktop.

---

# Non-Functional Requirements

## Consistency

All visual assets shall follow the Slate design language.

---

## Performance

Loading the wallpaper shall not noticeably increase startup time.

---

## Stability

Visual changes shall not introduce any regression from Phase 3.

---

# Out of Scope

The following remain excluded from this milestone:

- Boot screen animation — Phase 9 (a static logo boot may appear here, the animated loader comes later).
- Login screen — Phase 8.
- Top bar / dock / launcher — Phase 5 → Phase 7.
- Custom cursor theme, full typography system, frosted-glass / blur.
- Theme switching (light / contrast).
- Settings application.

> A minimal Slate color palette may be applied to existing UI (backgrounds, accents) so the desktop feels coherent, but a full design system is out of scope.

---

# Design Principles

- simplicity
- minimalism
- consistency
- readability

Every visual element must have a purpose. Decoration without function should be avoided.

---

# Success Criteria

The milestone is complete when:

- The official Slate wallpaper is bundled.
- The wallpaper loads automatically.
- The wallpaper scales correctly.
- Slate logo assets are available.
- No placeholder or generic assets remain visible.
- No regression from Phase 3 is introduced.

---

# Failure Criteria

The milestone fails if:

- The wallpaper does not load automatically.
- The wallpaper breaks scaling at common resolutions.
- Generic / placeholder assets remain visible.
- Visual changes degrade performance.
- Existing functionality regresses.

---

# Validation Procedure

For every build:

1. Boot into the graphical session.
2. Verify the Slate wallpaper is displayed automatically.
3. Verify correct scaling at common QEMU resolutions.
4. Verify Slate logo assets are present.
5. Confirm no placeholder assets remain.
6. Run smoke tests from Phase 3 (launch and close the terminal).

---

# Risks

| Risk | Mitigation |
|------|------------|
| Asset scaling issues | Test multiple resolutions |
| Wallpaper not auto-loading | Configure the compositor wallpaper tool explicitly |
| Performance regression | Keep asset sizes reasonable |
| Scope creep | Restrict this milestone to wallpaper + logo only |

---

# Deliverables

At the end of this milestone the project provides:

- Official Slate wallpaper (bundled, auto-loading, correctly scaled)
- Slate logo assets
- Removal of all placeholder assets

The operating system is now visually recognizable as Slate OS.

---

# Exit Criteria

When this document is fully satisfied, the project may proceed to:

**Slate OS Phase 5 — Top Bar**
