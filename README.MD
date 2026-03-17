<div align="center">

# ⚛️ NEXUS REACTION BENCHMARK

### CYBER-TITAN LLC · CERN Edition

**A Three.js 3D neural reaction benchmark game inspired by the CERN Control Centre.**
**Assess your reflexes within our NEXUS.**

[![Version](https://img.shields.io/badge/version-4.0-2962FF?style=flat-square&labelColor=0B1730)](https://github.com/the-cybertitan)
[![Three.js](https://img.shields.io/badge/Three.js-r128-00BFA5?style=flat-square&labelColor=0B1730)](https://threejs.org/)
[![Claude AI](https://img.shields.io/badge/Claude_AI-Sonnet-E040FB?style=flat-square&labelColor=0B1730)](https://anthropic.com)
[![License](https://img.shields.io/badge/license-MIT-FFB300?style=flat-square&labelColor=0B1730)](LICENSE)

<br>

<img src="https://img.shields.io/badge/-%E2%9A%9B%EF%B8%8F_PARTICLE_COLLIDER_MEETS_HUMAN_REFLEX_TESTING-020612?style=for-the-badge&labelColor=020612" alt="Tagline">

</div>

---

## 🔬 What Is This?

NEXUS is a production-grade reaction time benchmark disguised as a CERN particle collider control room simulator. Built as a single HTML file with zero dependencies beyond Three.js, it combines 3D WebGL graphics, adaptive difficulty AI, synthesized audio, power-up mechanics, and a Claude AI post-session analysis — all rendered in a glassmorphism control room aesthetic.

This isn't a tutorial project. It's a portfolio artifact engineered to demonstrate senior-level frontend architecture, 3D graphics programming, and AI integration in a single deliverable.

---

## ⚡ Features

### Core Gameplay
- **10-round reaction benchmark** with millisecond-precision timing (`Date.now()` isolated from render loop)
- **5-tier adaptive difficulty** engine: PS Ring → SPS → LHC → ATLAS → FCC (driven by rolling 5-round average)
- **4 power-ups**: Slow Time, 2× Streak, Higgs Boost (auto-135ms god-mode), Beam Overclock (rush mode)
- **Ghost comparison** system showing per-round delta against your previous best run

### Three.js 3D Engine
- **5 unique collider geometries** per difficulty tier (TorusGeometry → TorusKnotGeometry → IcosahedronGeometry)
- **Orbiting antimatter particles** (antiprotons p̄, positrons e⁺, antineutrons n̄) with independent orbits
- **Additive-blend halo layer** on colliders for volumetric glow effect
- **FogExp2 depth**, HemisphereLight, 3-point lighting rig with rim light
- **State-driven animation**: spring pop-in on collision, rapid spin on early fire, breathing idle
- **Full memory management**: dispose-first pattern on every geometry/material swap

### Analytics & AI
- **Biometric analysis panel**: trend detection, population σ variance, consistency score, fatigue index
- **Anomaly detection** at 2.5σ threshold
- **Canvas sparkline** graph with plasma gradient fill
- **Global percentile estimation** via linear interpolation from research baseline data
- **Claude AI post-session debrief** (Sonnet) with CERN physics metaphors + graceful local fallback

### Polish
- **Synthesized SFX** (Web Audio oscillator tones — zero external audio files)
- **PS1-style boot screen** with staggered animations, reaction tier guide, and pulsing START
- **Glassmorphism UI** with backdrop-filter blur, CRT scanlines, vignette overlay
- **Settings panel**: SFX toggle, volume, reduced motion, colorblind mode, font scaling, power-up toggle
- **Full ARIA accessibility**: role attributes, aria-live regions, aria-labels on all interactives
- **Touch-optimized**: explicit `touchstart` handlers, 44px+ touch targets, tap-highlight suppression

---

## 🎯 Reaction Tiers

| Tier | Time | Rating |
|:--:|:--:|:--|
| 🟢 | < 150ms | **Amazing** |
| 🔵 | 150 – 200ms | **Very Good** |
| 🔷 | 200 – 250ms | **Good** |
| 🟡 | 250 – 300ms | **Average** |
| 🔴 | > 300ms | **Below Average** |

---

## 🚀 Quick Start

```bash
# Clone the repo
git clone https://github.com/the-cybertitan/nexus-reaction-game.git
cd nexus-reaction-game

# That's it. Open in any browser.
open index.html
```

No build tools. No npm install. No framework. Just open the HTML file.

### Controls

| Input | Action |
|:--|:--|
| `SPACE` | Start game / capture collision / continue |
| `Click` | Same as spacebar (works everywhere) |
| `Tap` | Touch-optimized for mobile (zero delay) |

---

## 🏗️ Architecture

```
Single-file architecture (index.html)
├── CSS ─────────── CERN Control Centre design system (CSS custom properties)
│   ├── Glassmorphism panels (backdrop-filter + layered box-shadows)
│   ├── CRT scanline + vignette overlays
│   ├── Colorblind-safe pattern system
│   └── Responsive grid (6-col → 3-col at ≤700px, centered at ≤480px)
│
├── Three.js IIFE ─ Encapsulated 3D engine
│   ├── WebGLRenderer (alpha, antialias, pixelRatio capped at 2)
│   ├── FogExp2 + HemisphereLight + 3-point rig + rim light
│   ├── Geometry factory (5 tiers × unique collider shape)
│   ├── Additive-blend halo mesh layer
│   ├── Antimatter particle orbit system
│   ├── Power-up orb spawner (4 types × unique geometry)
│   ├── State machine (idle/wait/target/result/early)
│   └── Public API: buildMesh() · setState() · flashHalo() · dispose()
│
├── Sound IIFE ──── Web Audio oscillator synthesis (7 sound events)
├── Particle IIFE ─ Canvas 2D burst system (RAF-guarded)
├── Game Logic ──── State machine + timing + difficulty + power-ups
├── Analytics ───── Biometrics + sparkline + percentile + ghost
└── AI Debrief ──── Claude Sonnet API + local fallback
```

### Key Architectural Decisions

**Timing isolation**: `targetShownAt = Date.now()` is set *before* any Three.js state transitions. Reaction measurement uses `Date.now()` exclusively — the Three.js `Clock` drives only animation. Two completely independent timing systems.

**Memory management**: Every `buildMesh()` call invokes `disposeMesh()` first. Decoy arrays, halo meshes, orbit particles, and power-up orbs are all fully disposed before recreation. No orphaned GPU buffers.

**Sound without files**: All SFX are generated via `OscillatorNode` + `GainNode` with exponential ramps. Zero network requests for audio. Context initializes lazily on first user gesture (Chrome autoplay compliant).

**Single-file constraint**: The entire application — HTML, CSS, and JS — lives in one file. This is a deliberate portfolio decision: it proves the architecture can hold at scale without a build system.

---

## 📱 Platform Support

| Platform | Status | Notes |
|:--|:--:|:--|
| Chrome (Desktop) | ✅ | Primary target |
| Firefox | ✅ | Full support |
| Safari | ✅ | WebGL + Web Audio supported |
| Edge | ✅ | Chromium-based |
| iOS Safari | ✅ | Touch-optimized, audio on gesture |
| Android Chrome | ✅ | Touch-optimized, responsive layout |
| Mobile (≤480px) | ✅ | Centered header, 3×2 HUD grid, right panel hidden |

---

## ⚙️ Settings

Accessible via the **SETTINGS** button in the header:

| Setting | Description |
|:--|:--|
| **Sound Effects** | Toggle oscillator SFX on/off |
| **Volume** | Master volume slider (0–100%) |
| **Reduced Motion** | Kills all CSS animations + Three.js rotation (auto-detects `prefers-reduced-motion`) |
| **Colorblind Mode** | Adds pattern overlays (stripes/crosshatch) to color-coded elements |
| **Font Scale** | Adjust base font size (80%–130%) |
| **Power-ups** | Enable/disable power-up spawning |
| **Ghost** | Show/hide previous-best comparison overlay |

---

## 🧪 Power-Ups

| Power-Up | Rarity | Effect | 3D Orb |
|:--|:--:|:--|:--|
| **Slow Time** | 18% | Records RT at 85% of actual. Wait extended 1.35× | Purple icosahedron |
| **2× Streak** | 16% | Doubles streak increment on good rounds | Gold icosahedron |
| **Higgs Boost** | 14% | Auto-scores 135ms (Amazing). Massive teal particle burst | Teal spiky icosahedron |
| **Beam Overclock** | 12% | Wait window slashed to 400–1100ms. Pure adrenaline | Orange torus ring |

Power-ups spawn after round 2 with randomized probability. Each lasts 1 round. Toggable in settings.

---

## 🎨 Design System

**CERN Control Centre** palette derived from CERN's official visual identity guidelines:

| Token | Hex | Usage |
|:--|:--|:--|
| `--cern-blue` | `#0033A0` | Primary brand, buttons |
| `--cern-blue-hi` | `#2962FF` | Accents, highlights |
| `--higgs-teal` | `#00BFA5` | Secondary, fill light |
| `--beam-gold` | `#FFB300` | Wait state, warnings |
| `--signal-go` | `#00E676` | Amazing tier, collision |
| `--signal-err` | `#FF1744` | Below avg, early fire |
| `--antimatter` | `#E040FB` | Antimatter particles |
| `--xenon` | `#D6E4FF` | Primary text |

**Typography**: Syne 800 (display/headlines) · Exo 2 (body/UI) · DM Mono (data/telemetry)

---

## 📂 Project Structure

```
nexus-reaction-game/
├── index.html      ← Complete single-file application
├── favicon.png     ← Browser tab icon
├── README.md       ← You are here
└── ROADMAP.md      ← Feature roadmap & priorities
```

---

## 👤 Author

**Kendell Anderson** · [the-cybertitan](https://github.com/the-cybertitan)
Information Security Senior Cloud Analyst · Geisinger Health System
Founder, Cyber-Titan LLC · TitanFabricator

CISSP · CCSP · CASP+ · AWS Solutions Architect · AWS AI Practitioner · GCP Generative AI Leader

---

## 📋 License

MIT — build on it, remix it, ship it.

---

<div align="center">

**Built with Three.js · Powered by Claude AI · Designed at the speed of light**

*ZTM Vibe Coding Series · v4.0 · CERN Edition*

</div>
