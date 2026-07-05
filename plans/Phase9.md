# PRD: Slate OS Phase 9 — Boot Animation

**Version:** Phase 9  
**Status:** Draft  
**Author:** Adam  
**Last Updated:** 2026-07-05

---

# Overview

Slate OS Phase 9 introduces the **animated boot screen**.

Until now the system has booted with either text output or a static logo. This milestone replaces that with the official Slate boot experience: a centered logo and an animated, bars-style loader that moves and then fades away.

This is the first thing every user sees, and the last visual piece of the MVP.

---

# Objective

Replace the boot output with a branded boot screen that:

- shows the centered Slate logo on a black background
- plays an animated bars-style loader
- fades the loader out when boot completes
- transitions smoothly into the Login screen

---

# Problem Statement

A raw boot log or static logo does not feel like a finished operating system.

The animated boot screen is part of the MVP definition in `prd-mvp.md` and is the user's first impression of Slate.

---

# Users

Primary user:

- Adam (developer)

---

# Goals

- Hide raw boot output behind a branded screen.
- Display the Slate logo centered on a black background.
- Play a bars-style animated loader.
- Transition smoothly to Login.

---

# Functional Requirements

## FR-001 — Black Background

The boot screen shall use a black background.

---

## FR-002 — Centered Logo

The Slate logo shall be displayed centered on the screen.

---

## FR-003 — Animated Bars Loader

Below the logo, an animated **bars-style** loader shall be displayed.

Reference animation: https://cliloaders.com/bars_3

The loader shall move and then disappear as boot completes.

---

## FR-004 — No `_Starting_` Label

The boot screen shall **not** display the `_Starting_` label.

---

## FR-005 — Smooth Transition to Login

When boot completes, the boot screen shall transition smoothly into the Login screen (`_Login_`).

---

## FR-006 — Hide Boot Output

Raw kernel / service boot output shall be hidden behind the boot screen.

---

# Non-Functional Requirements

## Performance

The boot screen shall not noticeably increase boot time.

---

## Smoothness

The loader animation shall run without stutter on the target QEMU configuration.

---

## Stability

The boot screen must not interfere with the boot process or hide errors that block boot.

---

# Out of Scope

The following remain excluded from this milestone:

- Custom window open/close animations (default Hyprland is sufficient for MVP).
- Animated wallpaper.
- Boot sound.
- Multi-stage boot screens (e.g. separate screens for different boot phases).
- Localization of any boot text.

> The loader is the only animation required for MVP. It does not report real progress — it is a visual indicator only.

---

# Design Principles

- minimal
- silent (no sound)
- dark
- no text labels
- one focal point (the logo)

The boot screen should feel calm and fast.

---

# Success Criteria

The milestone is complete when:

- The boot screen has a black background.
- The Slate logo is centered.
- The bars-style loader animates and disappears.
- No `_Starting_` label is shown.
- Raw boot output is hidden.
- The transition into Login is smooth.
- No regression from Phase 8 is introduced.

---

# Failure Criteria

The milestone fails if:

- The boot screen hides a boot-blocking error.
- The loader animation stutters severely.
- The `_Starting_` label is shown.
- The transition to Login is broken.
- Boot time increases noticeably.
- The boot screen does not appear.

---

# Validation Procedure

1. Boot the system.
2. Verify the boot screen appears with a black background.
3. Verify the Slate logo is centered.
4. Verify the bars-style loader animates.
5. Verify the loader disappears as boot completes.
6. Verify no `_Starting_` label is shown.
7. Verify a smooth transition into the Login screen.
8. Repeat several times.

---

# Risks

| Risk | Mitigation |
|------|------------|
| Boot screen hides real errors | Keep early-boot diagnostics accessible (e.g. on key press or fallback) |
| Animation stutters in QEMU | Use a lightweight, GPU-friendly animation |
| Boot time regression | Do not block boot on the animation |
| Scope creep | Single loader, no sound, no text |

---

# Deliverables

At the end of this milestone the project provides:

- Branded Slate boot screen (black background, centered logo)
- Animated bars-style loader (cliloaders.com/bars_3 reference)
- Smooth transition into Login
- Hidden raw boot output

The user-facing boot experience is now complete.

---

# Exit Criteria

When this document is fully satisfied, the project may proceed to:

**Slate OS Phase 10 — MVP Integration & Validation**
