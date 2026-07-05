# PRD: Slate OS Phase 8 — Login Screen

**Version:** Phase 8  
**Status:** Draft  
**Author:** Adam  
**Last Updated:** 2026-07-05

---

# Overview

Slate OS Phase 8 introduces the **Login screen** (`_Login_`).

Until now the desktop has started directly via a temporary auto-login. This milestone replaces that with a real authentication step: the user must enter a password and press Enter before reaching the desktop.

The login screen is intentionally minimal — only a password field and Enter.

---

# Objective

Implement a minimal login screen that:

- appears before the desktop session
- accepts a password
- logs the user in on Enter
- rejects incorrect passwords
- starts the desktop session automatically after a successful login

The temporary auto-login from Phase 2 is removed.

---

# Problem Statement

Auto-login is fine for development, but unsuitable for a real operating system.

Authentication is a required step before Slate OS can be considered usable beyond a single developer machine.

---

# Users

Primary user:

- Adam (developer)

---

# Goals

- Display the Login screen before the desktop session.
- Authenticate with a password.
- Handle incorrect passwords gracefully.
- Remove the temporary auto-login.
- Recover safely from session crashes.

---

# Functional Requirements

## FR-001 — Login Screen

The Slate Login screen (`_Login_`) shall be displayed before the desktop session starts.

---

## FR-002 — Password Input

The Login screen shall contain a centered, pill-shaped password input.

---

## FR-003 — Login via Enter

Pressing **Enter** shall submit the password.

No submit button is required.

---

## FR-004 — Password Authentication

Users authenticate using a password (standard Linux / PAM authentication).

---

## FR-005 — Incorrect Password Handling

An incorrect password shall display an error and must not start the desktop session.

---

## FR-006 — Automatic Session Start

After a successful login:

- the desktop launches
- the user session starts
- the desktop becomes interactive

---

## FR-007 — Remove Auto-Login

The temporary auto-login introduced in Phase 2 shall be removed.

The desktop is now reachable only through Login.

---

## FR-008 — Session Recovery

If the desktop session crashes unexpectedly, the system shall return to the Login screen instead of showing a black screen.

---

# Non-Functional Requirements

## Security

Passwords must never be stored in plaintext.

Standard Linux authentication (PAM) shall be used.

---

## Stability

Authentication failures must never crash the desktop.

---

## Reliability

The transition from Login to desktop shall complete without graphical glitches.

---

# Out of Scope

The following remain excluded from this milestone:

- Multiple users / user switching — OUT OF SCOPE for MVP.
- Profile picture / avatar — OUT OF SCOPE for MVP.
- Password recovery via email — OUT OF SCOPE for MVP.
- Fingerprint / Face ID / PIN.
- Power / sleep / restart buttons on the login screen — OUT OF SCOPE for MVP.
- WiFi / Bluetooth controls on the login screen.
- Child accounts, permissions, online accounts.

> A single user with a single password is sufficient for MVP.

---

# Design Principles

- minimal (only a password field)
- centered, pill-shaped input
- dark background
- login via Enter, no submit button

---

# Success Criteria

The milestone is complete when:

- The Login screen appears before the desktop.
- The password input is present and pill-shaped.
- Enter submits the password.
- Correct password starts the desktop session.
- Incorrect password shows an error and does not start the session.
- Auto-login is removed.
- A crashed session returns to Login.
- No regression from Phase 7 is introduced.

---

# Failure Criteria

The milestone fails if:

- Authentication can be bypassed.
- A black screen appears instead of Login.
- The login screen freezes.
- The desktop crashes immediately after login.
- An incorrect password starts the session.

---

# Validation Procedure

1. Boot the system.
2. Verify the Login screen appears.
3. Enter an incorrect password and press Enter.
4. Verify the error is shown and the desktop does not start.
5. Enter the correct password and press Enter.
6. Verify the desktop session starts.
7. Trigger a session crash and verify the system returns to Login.
8. Repeat several times.

---

# Risks

| Risk | Mitigation |
|------|------------|
| PAM configuration issues | Use standard Linux authentication |
| Session crashes leave a black screen | Return safely to Login |
| Authentication bugs | Extensive repeated testing |
| Scope creep | Single user, single password only |

---

# Deliverables

At the end of this milestone the project provides:

- Slate Login screen (`_Login_`)
- Password authentication via Enter
- Incorrect password handling
- Removal of temporary auto-login
- Safe session recovery

The desktop is now protected by authentication.

---

# Exit Criteria

When this document is fully satisfied, the project may proceed to:

**Slate OS Phase 9 — Boot Animation**
