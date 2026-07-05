# PRD: Slate OS Phase 1 — Arch Linux Base

**Version:** Phase 1  
**Status:** Draft  
**Author:** Adam  
**Last Updated:** 2026-07-05

---

# Overview

Slate OS Phase 1 establishes the foundational operating system.

The objective of this release is to produce a **bootable Arch Linux image that starts reliably inside QEMU and reaches a working text console (TTY)**.

No graphical interface is introduced in this milestone. Before any GUI work can begin, Slate needs a stable, reproducible base system that boots cleanly.

---

# Objective

Produce a bootable Arch Linux image that:

- boots successfully inside QEMU
- reaches a usable text console
- has network access
- can be rebuilt reproducibly from a script

---

# Problem Statement

Every later milestone (GUI, terminal, branding, login) depends on a working base system.

If Arch Linux does not boot cleanly inside QEMU, every subsequent milestone is blocked. This milestone exists to remove that risk first, in isolation, before any graphical complexity is added.

---

# Users

Primary user:

- Adam (developer)

No external users are considered during this milestone.

---

# Goals

- Bootable Arch Linux image.
- Successful boot inside QEMU.
- Working text console (TTY).
- Functional network connectivity.
- Reproducible build process.

---

# Functional Requirements

## FR-001

The system shall be based on **Arch Linux**.

---

## FR-002

The system shall boot successfully inside **QEMU**.

---

## FR-003

The system shall reach a text console (TTY) after boot without manual intervention.

---

## FR-004

A non-root user account shall exist and be usable.

---

## FR-005

Network connectivity shall be available (DHCP).

---

## FR-006

Basic system tooling shall be installed:

- pacman
- a text editor
- common UNIX utilities

---

# Non-Functional Requirements

## Reproducibility

The image shall be buildable from a script, not assembled manually.

---

## Boot Time

The system should reach the console within approximately 20 seconds inside QEMU.

---

## Stability

The system shall complete ten consecutive boots without failure.

---

# Out of Scope

The following are explicitly excluded from this milestone and belong to later phases:

- Graphical interface (Wayland / Hyprland) — Phase 2
- GUI terminal emulator — Phase 3
- Wallpaper and branding — Phase 4
- Top bar / dock / launcher — Phase 5 → Phase 7
- Login screen — Phase 8
- Boot animation — Phase 9

---

# Success Criteria

The milestone is complete only if all conditions are met:

- Arch Linux boots successfully in QEMU.
- TTY console is usable.
- User can log in at the text console.
- Network connectivity works.
- Ten consecutive successful boots are completed.

---

# Failure Criteria

The milestone is considered failed if any of the following occur:

- Kernel panic.
- Boot hangs.
- No console appears.
- Network is unavailable.
- Manual intervention is required during boot.

---

# Validation Procedure

For every build:

1. Build the image from the script.
2. Boot inside QEMU.
3. Log in at the TTY.
4. Verify network connectivity (e.g. `ping`).
5. Repeat ten times.

Every run must complete successfully.

---

# Risks

| Risk | Mitigation |
|------|------------|
| Boot configuration errors | Use a proven Arch Linux installation method |
| QEMU incompatibility | Test with standard QEMU flags and virtio devices |
| Network setup issues | Enable DHCP by default |
| Non-reproducible build | Script the entire image build |

---

# Deliverables

At the end of this milestone the project must provide:

- Bootable Arch Linux image
- Reproducible build script
- Working TTY console
- Network access

Nothing else is required.

---

# Exit Criteria

When this document is fully satisfied, the project may proceed to:

**Slate OS Phase 2 — Hyprland Compositor**

No graphical work should begin before this milestone is complete.
