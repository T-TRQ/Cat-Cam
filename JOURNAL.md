# Development Journal

A running log of what I worked on, decisions I made, things I tried, things that broke. Newest entry at the top.

Entries are dated. They're not polished — that's the point. Future-me thanks present-me for writing them.

---

## 2026-05-13 — Project kickoff

Set up the repo skeleton. Read through OWASP ASVS section on authentication (V2). Honestly surprised by how much I would have skipped if I'd just started coding — there's a difference between "I know about JWTs" and "I have actually thought about refresh token reuse detection."

Decided to write the threat model before writing any code, so the design decisions have something to point at.

**Open questions for next session:**
- Does the Pi go on the main wifi or on a guest VLAN? My router supports VLANs but I've never configured one.
- Device authentication: mTLS or a long-lived signed token? mTLS is "more correct" but cert rotation for a single device feels like a lot.
- Do I want the server to be reachable from outside the tailnet at all? Probably not for v1.

**Next session plan:** finish a first draft of the threat model. Don't worry about it being final — that's what `Status: Draft` is for.

---

<!-- Add new entries above this line. Older entries go below. -->
