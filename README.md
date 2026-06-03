# FH6 Head Tracking Mod
### Forza Horizon 6 | PC | Community Mod | v1.0.0

Adds immersive **head tracking** to Forza Horizon 6 — look into corners, glance at mirrors, and feel like you're actually sitting in the car. Two versions included: one for **Tobii Eye Tracker 5** and one for any **webcam**.

---

## What This Mod Does

FH6 has no native head tracking support. This mod bridges the gap using Python scripts that read your head angle (from Tobii or webcam) and feed it into FH6's built-in **Mouse Free Look** system as smooth camera movement. No game files are modified — it works entirely through standard Windows mouse input.

---

## Which Version Should I Use?

| | Tobii Version | Webcam Version |
|---|---|---|
| **Hardware needed** | Tobii Eye Tracker 5 | Any webcam |
| **Accuracy** | Excellent | Good |
| **Setup complexity** | Moderate (needs OpenTrack) | Simple |
| **Extra installs** | OpenTrack | opencv + mediapipe (auto-installed) |
| **CPU usage** | Very low | Low-moderate |

---

## Requirements — Both Versions

- **Windows 10 or 11**
- **Python 3.8 or newer**
  Download: https://www.python.org/downloads/
  **Important:** Tick *"Add Python to PATH"* during install
- **Forza Horizon 6** (PC, Steam or Xbox app)

---

## Requirements — Tobii Version Only

- **Tobii Eye Tracker 5** plugged in and calibrated
- **Tobii Experience** app installed and running
  Download: https://gaming.tobii.com/getstarted/
- **OpenTrack**
  Download: https://github.com/opentrack/opentrack/releases
  (get the latest `.exe` installer)

---

## Requirements — Webcam Version Only

No extra downloads needed — `install_dependencies.bat` handles everything.

For best results:
- Good lighting on your face (avoid sitting with a window behind you)
- Webcam at roughly eye level, centred on your face
- Sit 40–80cm from the camera
- A plain background improves face detection reliability

---

## Installation

### Step 1 — Install Python
Download from https://www.python.org/downloads/ and run the installer.
**Tick "Add Python to PATH"** — this is required or nothing will work.

### Step 2 — Extract This Mod
Extract the zip to anywhere, for example:
```
C:\FH6-HeadTracking\
```

### Step 3 — Install Dependencies
Double-click **`install_dependencies.bat`** in the mod root folder.

- Tobii users: nothing to install (shown for info only)
- Webcam users: installs `opencv-python` and `mediapipe` automatically

### Step 4 — Tobii Users Only: Set Up OpenTrack
1. Install OpenTrack from the link above
2. Open OpenTrack
3. Go to **Profile → Import** and select `shared\OpenTrack_FH6.ini`
4. This pre-configures OpenTrack with the correct Tobii input and UDP output settings

### Step 5 — Configure FH6 (do this once)
Launch FH6 and go to **Settings**, then make these changes:

| Setting | Location | Value |
|---------|----------|-------|
| Mouse Free Look | Settings → Advanced Controls | **ON** |
| Drift Camera | Settings → HUD & Gameplay | **ON** |
| Camera View | Settings → HUD & Gameplay | **Driver** |

> **Why Mouse Free Look?**
> This is FH6's built-in free-look system. When enabled, holding the right mouse button lets you move the camera freely. Our script automates the right mouse button press based on your head position — you never need to touch the mouse yourself.

> **Why Drift Camera?**
> Drift Camera is FH6's built-in smooth corner-look system. It adds inertia and natural weight to camera movement, making head tracking feel much more polished and less twitchy.

> **Why Driver / Cockpit view?**
> Head tracking only has an effect in first-person (cockpit/driver) camera. Chase cam and bonnet cam do not respond to look input.

---

## Running the Mod

### Tobii Version — launch order every session:
1. Make sure **Tobii Experience** is running and ET5 is calibrated
2. Run **`tobii\Launch_Tobii.bat`** (as Administrator recommended)
3. In the OpenTrack window that opens, click **Start**
4. Launch **Forza Horizon 6** — head tracking is now active
5. Switch to **Driver/Cockpit cam** and drive!

### Webcam Version — launch order every session:
1. Run **`webcam\Launch_Webcam.bat`** (as Administrator recommended)
2. A small **preview window** will open showing your webcam feed
3. Check your face is detected (green text = good, red = not detected)
4. Launch **Forza Horizon 6** and switch to **Driver/Cockpit cam**
5. Drive and look into corners!

> The preview window can be closed or disabled by setting `SHOW_PREVIEW = False` in the script. Closing it also stops tracking, so set it to False instead while racing.

---

## How It Works

```
Tobii ET5 ──► OpenTrack ──► UDP (port 4242) ──► FH6_Tobii_HeadTrack.py
                                                        │
Webcam ─────► MediaPipe face mesh ──────────► FH6_Webcam_HeadTrack.py
                                                        │
                                              Windows SendInput API
                                                        │
                                            Forza Horizon 6 (Mouse Free Look)
```

The script reads your head angle, applies smoothing and a non-linear curve (so small movements are very precise), then sends the equivalent mouse movement to FH6 via the Windows `SendInput` API — the same method as a real mouse. Input is only sent when FH6 is the active window, so alt-tabbing works normally.

---

## Fine-Tuning

Open the script in Notepad to adjust these settings at the top:

| Setting | Default | Effect |
|---------|---------|--------|
| `MAX_YAW` | 45.0° | How far you turn your head for full camera pan. Lower = less effort. |
| `DEAD_ZONE` | 0.20 | Filters micro-tremor. Raise if camera drifts when head is still. |
| `SMOOTHING` | 0.97 | Camera lag. Higher = smoother. Lower = more responsive. |
| `MOUSE_SPEED` | 5 | How fast camera moves when tracking. |
| `RETURN_SPEED` | 3 | How fast camera returns to centre. |
| `CURVE` | 3.0 | 1.0 = linear. 3.0 = very precise at small angles. |
| `MAX_DELTA_PER_FRAME` | 8.0° | Spike filter. Lower to reduce jitter on direction changes. |
| `INVERT_PITCH` | False | Set True if up/down feels backwards. |

---

## Troubleshooting

**Camera doesn't move at all**
- Make sure Mouse Free Look is ON in FH6 Advanced Controls
- Make sure you are in Driver/Cockpit camera view
- Tobii: check OpenTrack is running and you clicked Start
- Make sure the script console window is open and shows `[IN GAME]` when FH6 is focused

**Camera goes mad on direction changes / bumps**
- Lower `MAX_DELTA_PER_FRAME` to 5.0 or 4.0

**Camera drifts when head is still**
- Raise `DEAD_ZONE` to 0.22 or 0.25

**Camera too slow / unresponsive**
- Lower `SMOOTHING` to 0.93–0.95
- Raise `MOUSE_SPEED` to 7–8

**Camera too jerky / twitchy**
- Raise `SMOOTHING` to 0.97–0.98
- Lower `MOUSE_SPEED` to 3–4

**Webcam: face not detected**
- Improve lighting on your face
- Move webcam closer (40–80cm ideal)
- Try `CAMERA_INDEX = 1` if you have multiple cameras

**Script shows `[standby]` and never `[IN GAME]`**
- Run the script as Administrator
- Make sure FH6's window title is exactly `Forza Horizon 6`

**Alt-tabbing moves my desktop mouse cursor**
- This should not happen in v1.0 — input is only sent to the FH6 window
- If it does occur, make sure you are running the script as Administrator

---

## Uninstalling

Stop the script (Ctrl+C or close the window). Delete the mod folder. No files are written to the game directory at any point.

---

## Credits

- **OpenTrack** — open source head tracking software (Tobii version)
- **MediaPipe** by Google — face landmark detection (webcam version)
- **OpenCV** — camera capture (webcam version)
- The FH6 community on Steam forums for figuring out the Mouse Free Look workaround

---

## Permissions

Free to use, share, and modify with credit.
Do not re-upload to other sites without crediting the original author.

---

## Changelog

### v1.0.0
- Initial public release
- Tobii Eye Tracker 5 support via OpenTrack UDP
- Webcam support via MediaPipe face mesh
- Non-linear curve for precision at small head angles
- Spike rejection filter for direction changes and bumps
- Hysteresis dead zone to prevent camera drift
- Alt-tab safe — input pauses when FH6 is not focused
- Live console bar showing head angle and camera state
