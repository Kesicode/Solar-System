# 🌌 3D Solar System Explorer

[![License: Apache-2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![React 19](https://img.shields.io/badge/React-19.0.0-61dafb.svg?logo=react&logoColor=black)](https://react.dev/)
[![Three.js](https://img.shields.io/badge/Three.js-r183-black.svg?logo=threedotjs&logoColor=white)](https://threejs.org/)
[![Vite](https://img.shields.io/badge/Vite-6.2-646CFF.svg?logo=vite&logoColor=white)](https://vitejs.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.8-3178C6.svg?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-v4-38B2AC.svg?logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)

> An immersive, cinematic 3D celestial journey through our planetary neighborhood, crafted with **React 19**, **Three.js**, **GSAP**, and **Tailwind CSS**.

Developed & Maintained with passion by **[Kesicode](https://github.com/Kesicode)**.

---

## 📖 Overview

**3D Solar System Explorer** brings the wonder of space exploration right to your web browser. Rather than a flat, static diagram or an overwhelming orbital simulator, this project takes an editorial, cinematic approach to planetary visualization.

Experience each celestial body from an orbital horizon perspective — gliding smoothly from inner terrestrial worlds like Mercury and Venus out across the gas giants to the icy realms of Neptune and Pluto. Every transition is dynamically choreographed with custom lighting, atmospheric Fresnel glows, and smooth camera tweening.

---

## ✨ Key Highlights & Features

- 🪐 **Realistic Planetary Rendering**: Detailed planetary surfaces with high-resolution texture maps and realistic topographic bump maps.
- 🎨 **Atmospheric Fresnel Glow**: Custom GLSL vertex and fragment shaders render soft, radiant atmospheric halos that react naturally to planetary lighting.
- 🎬 **Cinematic Camera Choreography**: Powered by **GSAP**, camera transitions smoothly sweep through deep space over 2.5-second easing curves (`power3.inOut`), seamlessly repositioning the horizon and re-targeting lighting.
- 💡 **Dynamic Lighting Rig**: Features high-fidelity directional sunlight with **PCF Soft Shadows** and a dynamic, color-matched rim light that shifts hue to complement each planet's atmosphere.
- 🖐️ **Intuitive Orbital Controls**:
  - **Manual Rotation**: Click and drag across the viewport to inspect any angle of the active planet.
  - **Raycasted Selection**: Click directly on visible 3D planets to instantly travel to them.
  - **Continuous Axial Spin**: Subtle, lifelike auto-rotation keeps the cosmos feeling alive.
- 📱 **Sleek Minimalist HUD**: Clean, modern space-age user interface with smooth text morphing and entrance animations via **Motion / AnimatePresence**.
- 🛡️ **Built-in Procedural Fallbacks**: Includes a canvas-based procedural noise generator ensuring planets render cleanly even when offline or experiencing network latency.

---

## 🔭 The Planetary Roster

Explore all 9 major celestial bodies, each with distinct physical representations and astrophysical data:

| Planet | Distance (from Sun) | Atmosphere / Color | Highlights |
| :--- | :--- | :--- | :--- |
| **Mercury** | `0.39 AU` | `#888888` (Cratered Slate) | Smallest planet, extreme temperatures, lunar-like terrain. |
| **Venus** | `0.723 AU` | `#E89C51` (Sulfuric Amber) | Dense runaway greenhouse atmosphere, volcanic plains. |
| **Earth** | `1.00 AU` | `#4B759E` (Oasis Blue) | The cradle of life, dynamic oceans, swirling cloud systems. |
| **Mars** | `1.524 AU` | `#C1440E` (Iron Rust) | The Red Planet, towering Olympus Mons, ancient river valleys. |
| **Jupiter** | `5.203 AU` | `#C99B75` (Jovian Bands) | King of planets, swirling storms, centuries-old Great Red Spot. |
| **Saturn** | `9.539 AU` | `#E3CB8F` (Golden Ochre) | Crown jewel of the solar system, vast icy ring architecture. |
| **Uranus** | `19.18 AU` | `#82B3D1` (Cyan Ice) | Tilted ice giant with high methane haze and pastel glow. |
| **Neptune** | `30.06 AU` | `#274687` (Deep Azure) | Supersonic storm systems, dynamic dark spots, frigid winds. |
| **Pluto** | `39.5 AU` | `#8B7355` (Nitrogen Frost) | Kuiper belt dwarf planet with nitrogen glaciers and water-ice peaks. |

---

## 🎮 Navigation & Controls

| Action | Control | Description |
| :--- | :--- | :--- |
| **Inspect Planet** | `Left-Click + Drag` | Rotate the currently focused planet across both the X and Y axes. |
| **Select from Rail** | `Click Left Sidebar Item` | Jump directly to any of the 9 celestial bodies via the navigation rail. |
| **Jump to Next Planet**| `Click "PLANET" Header` | Hop outward along the orbital chain to the adjacent celestial neighbor. |
| **3D Raycast Travel** | `Click Mesh in Scene` | Click directly on a planet's sphere in the 3D viewport to engage camera travel. |

---

## 🏗️ Architecture & Codebase Map

```
solar-system/
├── public/                     # Static assets
├── src/
│   ├── components/
│   │   └── PlanetScene.tsx     # Three.js scene, GLSL shaders, lighting & GSAP camera rig
│   ├── App.tsx                 # UI HUD overlay, navigation rail, planet data & animations
│   ├── index.css               # Tailwind CSS v4 directives & Inter web font configuration
│   └── main.tsx                # React 19 application root
├── .env.example                # Sample environment configuration
├── index.html                  # HTML entry template with viewport metadata
├── package.json                # Project dependencies and script runner commands
├── tsconfig.json               # TypeScript compiler configuration
└── vite.config.ts              # Vite bundling, Tailwind v4 plugin & build configuration
```

### Deep Dive: Graphic & Lighting Pipeline

1. **Scene Layout (`PlanetScene.tsx`)**:
   - Planets are aligned linearly along the deep Z-axis with `400` units spacing between orbital stations.
   - A linear space fog (`scene.fog = new THREE.Fog('#000000', 300, 800)`) naturally dissolves distant planets into deep space, eliminating visual clutter.
2. **Atmosphere Glow Shaders**:
   - Atmospheric hulls are rendered with `THREE.BackSide` geometry and custom GLSL vertex/fragment shaders using a Fresnel falloff curve:
     $$\text{intensity} = \left(\max(0.0, c - \mathbf{n} \cdot \mathbf{v})\right)^p$$
   - Blended additively with scene lighting to create realistic planetary halos.
3. **Camera Choreography**:
   - Rather than rigid cuts, GSAP interpolates both the camera position and its look-at focus vector simultaneously, keeping the focal planet curving low on the screen while framing the next planet rising on the horizon.

---

## 🚀 Getting Started

Follow these steps to run the 3D Solar System locally on your machine.

### Prerequisites

Ensure you have the following installed:
- **[Node.js](https://nodejs.org/)** (v18.0.0 or higher recommended)
- **npm**, **pnpm**, or **yarn**

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Kesicode/Solar-System.git
   cd Solar-System
   ```

2. **Install project dependencies:**
   ```bash
   npm install
   ```

3. **Start the development server:**
   ```bash
   npm run dev
   ```
   Open your browser and navigate to `http://localhost:3000` (or the URL displayed in your terminal).

4. **Build for production:**
   ```bash
   npm run build
   ```

5. **Preview production build:**
   ```bash
   npm run preview
   ```

---

## 🛠️ Tech Stack & Dependencies

- **Core Framework**: [React 19](https://react.dev/)
- **Bundler & Tooling**: [Vite 6](https://vitejs.dev/) with [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react)
- **3D Graphics**: [Three.js](https://threejs.org/) (`@types/three`)
- **Animation & Transitions**: [GSAP 3](https://greensock.com/gsap/) (3D camera/lights) & [Motion](https://motion.dev/) (UI HUD)
- **Styling**: [Tailwind CSS v4](https://tailwindcss.com/) with `@tailwindcss/vite`
- **Type Safety**: [TypeScript 5.8](https://www.typescriptlang.org/)
- **Icons**: [Lucide React](https://lucide.dev/)

---

## 📜 Available Scripts

| Command | Action |
| :--- | :--- |
| `npm run dev` | Starts the local Vite development server with hot module reloading. |
| `npm run build` | Compiles TypeScript and generates an optimized production bundle in `/dist`. |
| `npm run preview`| Locally serves the production build for testing. |
| `npm run lint` | Performs a TypeScript type-check across the codebase (`tsc --noEmit`). |
| `npm run clean` | Cleans up previous build artifacts in `/dist`. |

---

## 🗺️ Roadmap & Future Explorations

- [ ] **3D Rings**: Add realistic volumetric ring geometry and alpha-transparency maps for Saturn and Uranus.
- [ ] **Moons & Satellites**: Render orbiting major moons (e.g. Earth's Moon, Europa, Titan, Ganymede).
- [ ] **Touch Gestures for Mobile**: Enhanced touch drag and pinch-to-zoom for tablet and mobile devices.
- [ ] **Cosmic Soundscapes**: Ambient audio synth backdrop with interactive sound effects on planetary warp transitions.
- [ ] **Orrery Mode**: Scale-toggle view to see true orbital inclinations and proportional speeds.

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](https://github.com/Kesicode/Solar-System/issues).

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is open source and available under the [Apache-2.0 License](LICENSE).

---

<div align="center">
  <sub>Built with 💙 by <a href="https://github.com/Kesicode">Kesicode</a> • Ad Astra per Aspera 🚀</sub>
</div>
