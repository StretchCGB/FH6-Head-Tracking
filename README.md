FH6 Head Tracking
Tobii Eye Tracker 5  •  TrackIR  •  Any Webcam




FH6 has no native head tracking support. This mod fixes that.

Turn your head to look into corners, glance at approaching traffic, or check your mirrors — using your Tobii Eye Tracker 5, TrackIR, or any standard webcam. The camera follows your head smoothly and returns to centre when you look forward again. No game files are touched.



━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FEATURES
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Three tracking methods — Tobii Eye Tracker 5, TrackIR, or any webcam (via MediaPipe AI face tracking)
Any OpenTrack-compatible tracker supported — if OpenTrack can read it, this mod can use it
Smooth, natural feel — non-linear curve means small head turns are precise, big turns give full look
Auto-return to centre — look forward and the camera follows back
Spike filter — ignores car jolts and direction changes so the camera stays stable
Alt-tab safe — input is paused the moment FH6 loses focus, your desktop mouse is never affected
No game files modified — works entirely through FH6's built-in Mouse Free Look system
Fully tunable — sensitivity, smoothing, curve and dead zone all adjustable at the top of the script
Free, open source tools only — Python, OpenTrack, MediaPipe



━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
WHICH VERSION IS RIGHT FOR ME?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Tobii Eye Tracker 5 — Best accuracy and lowest CPU usage. Requires OpenTrack (free). Recommended if you already own a Tobii.

TrackIR (any version) — Fully supported via OpenTrack. Use the Tobii launcher — OpenTrack handles all the input, the script only cares about the UDP data it receives. In OpenTrack set Input to TrackIR instead of Tobii. Everything else is identical.

Any other OpenTrack-compatible tracker — FaceTrackNoIR, SteamVR, phone-based trackers, Arduino IMU — if OpenTrack can read it and output UDP on port 4242, this mod will work with it.

Webcam — Works with any webcam you already own. Uses AI face detection (MediaPipe) to estimate head angle. No OpenTrack needed. Slightly more CPU usage than hardware trackers but very capable in good lighting.



━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
REQUIREMENTS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

All versions:
Windows 10 or 11
Python 3.8+ — tick "Add Python to PATH" during install
Forza Horizon 6 (PC)

Tobii / TrackIR / hardware tracker:
Your tracking hardware (plugged in and set up)
OpenTrack (latest release, free)
Tobii users also need Tobii Experience running
TrackIR users also need NaturalPoint TrackIR software running

Webcam version only:
Any webcam
opencv-python + mediapipe — installed automatically by the included bat file



━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
INSTALLATION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Step 1 — Install Python. Tick "Add Python to PATH".

Step 2 — Extract this mod to any folder, e.g. C:\FH6-HeadTracking\

Step 3 — Run install_dependencies.bat once to set up packages.

Step 4 (hardware trackers only) — Install and open OpenTrack. Go to Profile → Import and select shared\OpenTrack_FH6.ini. Then set your Input to match your device (Tobii, TrackIR, etc.) and set Output to UDP over network → 127.0.0.1 port 4242.

Step 5 — In FH6 make these one-time settings changes:
Settings → Advanced Controls → Mouse Free Look = ON
Settings → HUD & Gameplay → Drift Camera = ON
Settings → HUD & Gameplay → Camera View = Driver



━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
USAGE — EVERY SESSION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Tobii / TrackIR / hardware tracker:
Ensure your tracking software is running (Tobii Experience / TrackIR software)
Run tobii\Launch_Tobii.bat as Administrator
Click Start in OpenTrack — check the octopus moves with your head
Launch FH6 and switch to Driver / Cockpit cam

Webcam:
Run webcam\Launch_Webcam.bat as Administrator
A preview window opens — confirm your face is detected (green text)
Launch FH6 and switch to Driver / Cockpit cam



━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FINE TUNING
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Open the script in Notepad to adjust settings at the top of the file:


DEAD_ZONE            = 0.20  # Raise if camera drifts when head is still
SMOOTHING            = 0.97  # Raise for smoother, lower for more responsive
MOUSE_SPEED          = 5      # Raise for faster camera tracking
MAX_DELTA_PER_FRAME  = 8.0    # Lower if camera jerks on direction changes
CURVE                = 3.0    # Raise for more precision at small angles




━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
TROUBLESHOOTING
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Camera doesn't move — Check Mouse Free Look is ON in Advanced Controls. Check you are in Driver/Cockpit cam. Hardware trackers: make sure OpenTrack is running and you clicked Start.

Camera jerks on direction changes — Lower MAX_DELTA_PER_FRAME to 5.0

Camera drifts when head is still — Raise DEAD_ZONE to 0.22–0.25

Camera too twitchy — Raise SMOOTHING to 0.98

Camera too slow / unresponsive — Lower SMOOTHING to 0.93, raise MOUSE_SPEED to 7

Webcam not detecting face — Improve lighting on your face, move closer to camera (40–80cm), try CAMERA_INDEX = 1 if you have multiple cameras

TrackIR not working — Make sure NaturalPoint TrackIR software is running, then in OpenTrack set Input to TrackIR and Output to UDP over network (127.0.0.1 port 4242)

Script shows [standby] and never [IN GAME] — Run as Administrator. Make sure FH6's window is titled exactly Forza Horizon 6



━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
COMING SOON
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

SteamVR support — reading headset rotation via OpenVR to drive the camera. Currently being investigated.
Further stability improvements — ongoing tuning based on community feedback

Have a feature request or bug? Post in the Posts tab and I'll look into it.



━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
CREDITS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

OpenTrack — open source head tracking software
MediaPipe by Google — AI face landmark detection
OpenCV — webcam capture
The FH6 Steam community for discovering the Mouse Free Look workaround
Catsmecha for confirming TrackIR compatibility



No game files are modified. This mod uses only standard Windows mouse input via FH6's built-in Mouse Free Look system. Use at your own risk in online modes.
