# Loopmates: Launch Film (Branch: film)

**The cinematic product launch film for Loopmates.** Built using a deterministic GSAP motion runtime, frame-accurate headless Chrome rendering, layered spatial audio (ElevenLabs voice-over, custom generative ambient bed, and micro-SFX event tracks), and tactile neobrutalist 3D design.

> **License:** [MIT License](LICENSE) · Part of the [Loopmates](https://github.com/StarDust-Git-Code/loop-mates) autonomous AI team project.

---

## 🎬 Film Overview

- **Resolution:** 1080p Full HD (1920 × 1080) @ 30fps
- **Runtime:** GSAP-driven deterministic timeline with seek-safe architecture (`runtime/`)
- **Visual Design:** Neobrutalist tactile slabs, 45° extrusion depth, paper grid plane (`#FFFDF5`), official Loopmates mascots (`assets/m/`), and dynamic camera perspective rigs.
- **Audio Mix:** Multi-track composition in `audio/film/` and `audio/v2/` featuring synchronized voice-over, sound bed, and event-triggered UI micro-SFX.

---

## 📁 Repository Structure

```
film/
├── index.html          # Main GSAP animation stage and camera rig
├── film.js             # Core animation timeline logic and scene directors
├── v2.html             # Extended v2 film cut with tactile 3D perspective
├── v2.js & v2-nb-*.js  # Modular scene controllers (scenes 1 through 12 + outro)
├── assets/             # Vector icons, branding marks, and high-res Mate mascots
├── audio/              # Voice-over takes, word alignment timestamps, music beds, mixes
├── renders/            # Rendered video deliverables (film.mp4)
├── runtime/            # Headless seek-safe GSAP driver and render scripts
├── script/             # Screenplay, timing sheets, and storyboard guides
├── sfx/                # UI interaction sound effects (pops, clicks, thuds, snaps)
├── stills/             # Keyframe verification contact sheets and QC renders
└── tools/              # Python & Node automation for forced alignment and audio mastering
```

---

## 🚀 How to Run Locally

### 1. Preview in Browser
Serve the directory with any local HTTP server:
```bash
npx serve .
# Or with Python:
python -m http.server 8000
```
Open `http://localhost:8000/index.html` or `http://localhost:8000/v2.html` to watch the timeline with live audio scrubbing.

### 2. Render to MP4
Using the headless rendering pipeline in `runtime/`:
```bash
npm install
node runtime/render.mjs
```

---

## 📜 License
Distributed under the [MIT License](LICENSE).
