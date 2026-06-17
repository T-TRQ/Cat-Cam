# ADR-0002: Three-tier physical architecture (Pi4, laptop server, browser client)

**Status:** Accepted
**Date:** 2026-06-11

## Context

There was a need for something to host the camera and logic, as well as a server with some sort of DB. There was also a need to consider the security aspect of the architecture as well as the scalability.

Four possible architectures were considered:

1. **All-in-one on the Pi 4 4GB.** Logic, camera, server is located on the Pi. Browser client to access camera for end user.
2. **All-in-one on a Pi 4 8GB or Pi 5.** Logic, camera, server is located on the Pi. Browser client to access camera for end user.
3. **All-in-one on the laptop:** Logic, camera, server is located on the laptop. Browser client to access camera for end user.
4. **Pi, Laptop/PC and browser client.** Pi has logic and camera, PC has server with DB etc. and browser client to access camera for end user.

## Decision

For better security and scalability option 4 was the most relevant. The threat model treats the camera node as low-trust (physically accessible, runs more code, has USB peripherals attached) and authoritative state as high-trust. A core property of the design is that these two trust levels live on physically separate hardware, so a compromise of one doesn't automatically yield the other.

## Consequences

Having the server on a separate device from the Pi is highly beneficial as The camera node is the most exposed component, it runs more code, has a USB device attached, and is physically accessible. If it's compromised, you want the database, auth state, and recorded clips to be elsewhere so the attacker doesn't get everything by owning one device

The laptop has a real GPU. The Pi doesn't. AI object detection on the laptop is feasible without an accelerator. The laptop can also be backed up, rebooted, and rebuilt without disturbing the camera. The Pi can be moved, replaced, or wiped without losing data. 

The trade-offs of this split include
The server-tier hardware is to be reformatted with Ubuntu Server (see ADR-0004). Which will come with it's own set of challenges and learning curve. This also leads to two devices to keep updated and patched, not one and a second device's worth of attack surface added to the system.

Network coupling between Pi and Server is now a hard dependency if the Server is offline, the Pi can't push events. the Pi must buffer locally or drop events (see ADR-XX once buffering policy is decided).

## Alternatives Considered

1. **All-in-one on the Pi 4 4GB:** The 4GB RAM is tight for running capture, motion detection, and an API server simultaneously, and there's no headroom for AI inference. 
2. **All-in-one on a Pi 4 8GB or Pi 5:** would be capacity-sufficient but collapses the trust separation.
3. **All-in-one on the laptop:** sufficient on every axis but means the laptop has to be physically near the cat, which is operationally awkward and means the high-value component is in a more exposed location. It also becomes a single point of compromise.
