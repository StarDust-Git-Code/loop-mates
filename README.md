# Loopmates: Synchronized Launch Film (Branch: film-copy)

**The re-timed, precision-synchronized launch film for Loopmates.** Specifically aligned to the ElevenLabs Lyan (*Female Genuine Casual Ads*) voiceover take using forced alignment, micro-SFX retiming, and GSAP cue synchronization.

> **License:** [MIT License](LICENSE) · Part of the [Loopmates](https://github.com/StarDust-Git-Code/loop-mates) autonomous AI team project.

---

## 🎬 Film Specs

- **Voice Talent:** ElevenLabs *Lyan* (`Female Genuine Casual Ads`, `pvc_s50_sim75_v4`)
- **Alignment:** PyTorch / Torchaudio MMS Forced Alignment (`tools/align_mms.py`) with word-by-word timestamp extraction (`audio/vo/vo.alignment.json`).
- **Resolution:** 1080p Full HD (1920 × 1080) @ 30fps
- **Render Output:** `renders/film.mp4` (~24.5 MB, high-efficiency H.264 + AAC 48kHz).
- **Audio Mix:** Layered in `audio/film/mix.wav` and `audio/film/bed.wav` with procedural ducking and synchronized sound effects.

---

## 📁 Repository Structure

```
film-copy/
├── index.html          # Main GSAP animation stage and camera rig
├── film.js             # Synchronized animation timeline with cue triggers
├── assets/             # Vector icons, branding marks, and high-res Mate mascots
├── audio/              # Voice-over takes, word alignment timestamps, music beds, mixes
├── renders/            # Rendered video deliverables (film.mp4)
├── runtime/            # Headless seek-safe GSAP driver and render scripts
├── script/             # Screenplay, timing sheets, and storyboard guides
├── sfx/                # UI interaction sound effects (pops, clicks, thuds, snaps)
├── stills/             # Keyframe verification contact sheets and QC renders
└── tools/              # Forced alignment, cue testing, and audio mastering scripts
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
Open `http://localhost:8000/index.html` to watch the timeline with live audio scrubbing.

### 2. Render to MP4
Using the headless rendering pipeline in `runtime/`:
```bash
npm install
node runtime/render.mjs
```

---

## 📜 License
Distributed under the [MIT License](LICENSE).
