# PRD: Slate OS Phase 10 — MVP Integration & Validation

**Version:** Phase 10  
**Status:** Draft  
**Author:** Adam  
**Last Updated:** 2026-07-05

---

# Overview

Slate OS Phase 10 is the **closing milestone of the MVP**.

All MVP components have been built in Phase 1 → Phase 9. This release does not add new features. Its sole purpose is to **integrate everything into a single, stable, end-to-end flow** and validate that the MVP definition from `prd-mvp.md` is fully satisfied.

If this milestone passes, **MVP is done** and the project can move to Phase 2 (personas, Slate Store, file compatibility).

---

# Objective

Prove that the complete MVP flow works as one continuous experience inside QEMU:

> Boot (animated logo + loader) → Login (password + Enter) → Desktop (wallpaper, top bar with live clock, dock with clickable icons + launchpad) → Terminal launches and works → ● closes the window.

---

# Problem Statement

Each component was validated in isolation. The MVP is only complete when they work **together**, repeatedly, without crashes and with smooth animations.

The previous attempt at building Slate failed at exactly this level — the pieces did not come together into a usable graphical experience. This milestone is the final proof that they do.

---

# Users

Primary user:

- Adam (developer)

---

# Goals

- Verify the full end-to-end MVP flow.
- Verify stability across repeated boots.
- Verify there are no crashes during normal use.
- Confirm the MVP definition from `prd-mvp.md` is met.

---

# Functional Requirements

This milestone has no new features. It validates the integration of:

## FR-001 — Full Boot Flow

The system shall boot through:

1. animated boot screen (logo + bars loader)
2. Login screen (`_Login_`)
3. desktop session

without manual intervention.

---

## FR-002 — Desktop Completeness

The desktop shall present:

- Slate wallpaper
- top bar with a live clock
- bottom dock with clickable icons
- Apps icon opening the Launchpad

---

## FR-003 — Application Workflow

The user shall be able to:

- open the Launchpad from the dock
- launch the Terminal from the Launchpad (or dock)
- use the Terminal
- close the Terminal using ●

---

## FR-004 — No Regressions

All functionality from Phase 1 → Phase 9 shall continue to work together.

---

# Non-Functional Requirements

## Stability

The complete flow shall survive ten consecutive full cycles (boot → login → desktop → launch terminal → close → reboot) without failure.

---

## Smoothness

Boot animation, Launchpad blur transition and default window behavior shall feel smooth.

---

## Reliability

No compositor crash, black screen or freeze is acceptable during the validation cycles.

---

# Out of Scope

This milestone adds **nothing new**. Anything not already built in Phase 1 → Phase 9 is out of scope for the MVP, including (but not limited to):

- Personas / onboarding.
- Slate Store.
- File compatibility (.exe / .dmg / .deb / .tar.gz / .AppImage).
- Notifications, control center, quick toggles.
- WiFi / Bluetooth functionality.
- Weather, battery, audio indicators.
- Settings application.
- File manager, calculator, image viewer (Terminal only for MVP).
- Window snapping, fill, minimize.
- Multi-user, encryption, firewall.

---

# Success Criteria — "MVP Ready"

The MVP is complete only if **all** of the following are true (mirrors `prd-mvp.md`):

- [ ] System boots inside QEMU.
- [ ] Base is Arch Linux.
- [ ] Wayland + Hyprland runs stably.
- [ ] Boot screen shows the Slate logo + animated bars loader (no `_Starting_`).
- [ ] Login screen (`_Login_`) works (password + Enter).
- [ ] Desktop renders correctly:
  - [ ] top bar with a live clock
  - [ ] wallpaper (default Slate image)
  - [ ] bottom dock (clickable icons, Apps opens the Launchpad)
- [ ] Terminal launches and works.
- [ ] ● close button works.
- [ ] Ten consecutive full cycles complete without crashes.

When every box above is checked, **MVP is done**.

---

# Failure Criteria

The MVP is not ready if any of the following occur during validation:

- Black screen, frozen desktop, or Hyprland crash.
- Login fails or can be bypassed.
- The desktop is missing any required element (wallpaper, top bar, dock, launchpad).
- The Terminal cannot launch or be closed.
- Manual intervention is required during boot.
- Any of the ten validation cycles fails.

---

# Validation Procedure

Run the following cycle **ten times**. Every cycle must pass.

1. Boot the system in QEMU.
2. Observe the animated boot screen (logo + bars loader, no `_Starting_`).
3. Reach the Login screen.
4. Enter the password and press Enter.
5. Reach the desktop.
6. Verify wallpaper, top bar (live clock) and dock.
7. Open the Launchpad from the dock.
8. Launch the Terminal.
9. Run a basic command.
10. Close the Terminal using ●.
11. Reboot.

After ten successful cycles, the MVP is declared complete.

---

# Risks

| Risk | Mitigation |
|------|------------|
| Components conflict when combined | Test integration early and often |
| Intermittent crashes | Run the full validation cycle repeatedly |
| Performance issues only visible end-to-end | Profile the full flow, not individual components |
| Scope creep near the finish | Freeze scope; defer everything new to Phase 2 |

---

# Deliverables

At the end of this milestone the project provides:

- A single, integrated, bootable Slate OS MVP image
- A validated end-to-end MVP flow
- Evidence of stability (ten successful cycles)
- Confirmation that the `prd-mvp.md` definition of "MVP ready" is satisfied

---

# Exit Criteria

When this milestone passes, **Phase 1 (MVP) is closed**.

The project may then proceed to **Phase 2**, which covers (out of MVP scope):

- Persona onboarding in Calamares
- Slate Store
- File compatibility layers (.exe / .dmg / .deb / .tar.gz / .AppImage)
- Hardware detection and optimization
- Notifications, control center, WiFi / Bluetooth
- Settings application and additional native apps

> The MVP is the proof that Slate can boot into a stable, usable graphical desktop. Everything else builds on top of this foundation.
