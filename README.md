# Svarupa — Working Prototype

**Svarupa** (sva-ROO-pa, Sanskrit: "one's own true form") — *Meet your true form.*

An AI practice companion for movement learning. **GPS for the body:** your teacher sets the destination; Svarupa guides your solo practice back to it. Students learn a movement from a teacher, then practice alone in front of a phone camera and receive one clear, plain-language correction at a time.

This repository is a **genuinely working prototype**, built for the **MIT Solve 2027 Global Learning Challenge**. It is not a mockup — pose estimation, joint-angle measurement, scoring, and correction all run for real, in the browser.

**Live:** https://bhavanaangadi123.github.io/svarupa-prototype/

## What works

- **Live camera mode** — webcam feed with a real-time skeleton overlay (MediaPipe Pose, 33 landmarks).
- **Joint-angle engine** — computes 8 joint angles in degrees (left/right knee, elbow, shoulder, hip) from the pose landmarks, with a live readout and light smoothing.
- **Real-time match score (0–100%)** — compares your angles against the selected reference pose; a score ring updates every frame. Hold **85%+ for ~2 seconds** to complete a pose.
- **One correction at a time** — the joint furthest from the reference drives a single direction-aware cue, e.g. *"Bend your left knee more"*, *"Raise your left arm higher"*, *"Sink lower through both knees"*.
- **3 starter reference poses** — Standing Tall, Half-Sit Stance (ardha-mandala inspired), Raised-Arm Pose. Honestly labeled in the UI as a starter set with illustrative target angles.
- **Teacher Record mode** — the product's core thesis. A teacher holds a pose, clicks *Capture reference*, and the 8 measured angles are saved as a new named reference (persisted in `localStorage`) that students can immediately practice against.
- **Photo fallback** — upload a still photo; it is analyzed and scored against the selected reference, with the skeleton drawn on the image. Useful where no camera is available.
- **Session panel** — practice timer, attempts, best score per pose, poses held, and a running session summary.
- **Graceful failure** — camera denial, missing camera APIs, or a failed library load produce clear human messages; photo mode remains available wherever possible.

## Privacy

All pose processing happens **on-device in your browser** via MediaPipe. No video, photo, or angle data is uploaded or stored on any server. Teacher-captured references live only in your browser's `localStorage`.

## Tech

- Single-file web app (`index.html`) — no build step.
- [MediaPipe Pose](https://cdn.jsdelivr.net/npm/@mediapipe/pose/pose.js) via CDN (`Pose`, `Camera`, `drawConnectors`, `POSE_CONNECTIONS`), with `locateFile` pointed at the `@mediapipe/pose` CDN package.
- Tailwind CSS (CDN) + custom CSS for a dark, cinematic "practice studio at night" design: Fraunces display type + Inter, temple-gold and teal accents, subtle grain.
- Motion (motion.dev) via CDN for micro-animation — fully guarded, so the app works even if that CDN fails.

## Run locally

```bash
# any static server works, e.g.:
python3 -m http.server 8000
# then open http://localhost:8000  (camera requires localhost or HTTPS)
```

## Honest limitations

- The built-in reference angles are illustrative starting points, not guru-certified targets — the real product's references are recorded by teachers (try Teacher Record mode).
- Standard pose estimation tracks major body joints; fine hand gestures (mudras) are out of scope for this prototype.
- Feedback is for movement practice only — not medical or rehabilitation advice.

---

*Svarupa — meet your true form.*
