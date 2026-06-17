# Threat Model

**Last updated:** 2026-05-17
**Status:** Draft

---

## 1. Purpose

A home surveillance system that lets a single user (me) watch their cat remotely. A Raspberry Pi captures video from a USB webcam, runs motion and object detection, and pushes events to a self-hosted server on the same LAN. The server stores clips and serves a web dashboard reachable over a private VPN.

---

## 2. Assets

What I am protecting, in rough priority order. Sensitivity: Critical / High / Medium / Low.

| Asset | Why it matters | Sensitivity |
|---|---|---|
| User credentials (password, session/refresh tokens) | Compromise gives full access. | Critical |
| The Pi as a foothold on my LAN | Compromised Pi could pivot to other devices on the network. | Critical |
| Recorded clips of the home interior | Privacy. Reveal when I'm home, layout, valuables. | High |
| Live video stream | Same as above but real-time. | High |
| Server (laptop) | Holds all data and auth state. | Critical |
| Audit logs | Useful for incident response if anything happens. | Medium |
| | | |

---

## 3. Adversaries

| Adversary | Capabilities | Motivation | In scope? |
|---|---|---|---|
| Untargeted internet scanner | Untargeted, automated. Tries known exploits, default creds, common ports. | Opportunistic compromise. | Yes |
| Attacker on my wifi | Can sniff unencrypted traffic, ARP-spoof, attempt LAN exploits. | Curiosity, neighbor with knowledge. | Yes |
| Physical access to the Pi | Can pull SD card, attach to console, read filesystem. | Theft of device. | Yes (degraded mode) |
| Compromised dependency | Malicious update somewhere in my stack (npm, pip, Docker image). | Supply-chain attack, not me specifically. | Partial — see out-of-scope |
| Me, making mistakes | Pushing secrets to GitHub, misconfiguring services, weak passwords. | N/A — accidents. | Yes |
| Targeted attacker with significant resources | Custom exploits, social engineering, 0-days. | Unrealistic for this project. | No — out of scope |

---

## 4. Trust Boundaries

[Diagram will be added, for now list:]

1. **Internet ↔ Tailscale** - only my devices are on the tailnet. Trust transitions from "nothing" to "my devices."
2. **Browser ↔ Server** - user is authenticated, but the browser environment itself is partly hostile (XSS, extensions).
3. **Pi ↔ Server** - Pi is a long-lived device with its own identity. Treated as low-trust because it's physically accessible and may be stolen.
4. **Server ↔ Database** - same host but separate process / container.
5. **Server ↔ Object storage (clips)** - large blobs handled differently from DB rows.

---

## 5. Threats and Controls

STRIDE per boundary. STRIDE = Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, Elevation of privilege.

### Boundary: Browser ↔ Server

- **Spoofing:** attacker impersonates a legitimate user.
  - Threat: stolen credentials, session fixation.
  - Control:

- **Tampering:** attacker modifies requests or responses in transit.
  - Threat: MITM on local network.
  - Control:

- **Repudiation:** user denies an action they performed.
  - Threat: not very relevant for a single-user system but still good to log.
  - Control:

- **Information disclosure:**
  - Threat: API leaks data the user shouldn't see, error messages reveal internals.
  - Control:

- **Denial of service:**
  - Threat: a bug or attacker exhausts server resources.
  - Control:

- **Elevation of privilege:**
  - Threat: a regular user gains admin rights, or a non-user gains any rights.
  - Control:

### Boundary: Pi ↔ Server

Repeat the STRIDE pattern. Key questions: how does the Pi prove it's the Pi? What if its credential is stolen? Can the Pi be denied service / replaced by an imposter Pi?

### Boundary: Server ↔ Database

Repeat. Key questions: how is the DB credential stored? Is the DB reachable from anywhere other than the server process? What does a SQL injection get you?

### Boundary: Internet ↔ Tailscale

Repeat. Key questions: what if my Tailscale account is compromised? What if a device on my tailnet is compromised?

---

## 6. Out of Scope

I am explicitly NOT defending against:

- Nation-state attackers with hardware-level capabilities. Unrealistic for a home cat cam.
- Physical attack on the laptop. Assumed to be in a trusted physical location.
- Total supply-chain compromise of major package registries (npm/PyPI catastrophic event). Mitigation: pinned versions, but ultimately accepted risk.

---

## 7. Accepted Risks

- **Risk:** the Pi's outbound credential to the server is a long-lived signed token rather than mTLS with rotation.
  - **Why accepted:** mTLS rotation for a single device adds operational complexity disproportionate to the threat.
  - **What would change our mind:** more than 2 cameras, or the Pi being physically less secure than assumed.

---

## 8. Open Questions

Things not yet decided.

- Pi network placement: main wifi vs. guest VLAN.
- Device authentication mechanism: mTLS vs. signed JWT vs. API key.
- Web session storage: cookie vs. localStorage. (Cookie with `HttpOnly` + `SameSite=Strict`?)
- MFA approach: TOTP only? Recovery codes? Is MFA needed at all for a single-user system?
- Retention: how long are clips kept by default?
