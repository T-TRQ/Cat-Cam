# Pi node

The Raspberry Pi side of the cat cam. Runs physically next to the camera and is responsible for:

- capturing video from the USB webcam
- motion detection (initially) and on-device AI detection (later)
- buffering clips locally during network outages
- sending events to the server over an encrypted channel

This is treated as a **low-trust device** in the threat model — see [../docs/threat-model.md](../docs/threat-model.md). The reasoning: the Pi is physically accessible (someone could pull the SD card), runs more code than the server, and is the most exposed surface even though it's not directly on the internet.

## Subfolders

(To be added as code is written.)
