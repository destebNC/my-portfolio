# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Daniel Esteban's personal portfolio (backend developer / junior software engineer). It is a static site: everything lives in `index.html`, with inline `<style>` and `<script>`, no build step, no dependencies and no tests. The only external resource is Google Fonts (Inter and JetBrains Mono). To preview it, open `index.html` directly in a browser. Python is not installed on this machine, so `python -m http.server` won't work.

Images go in `img/`, referenced by relative path. Right now that is `myface.jpg` (the avatar) and `akatama.png` (the game screenshot).

## Content rules

- **Source of truth:** the CV PDF in the repo root. It is gitignored because it contains a phone number. Never commit it and never put the phone number on the page. Don't invent experience, numbers or projects that aren't in the CV.
- **Language:** everything visible on the page and in code comments is in Spanish.
- **No emojis.** Icons are inline SVGs from the sprite of `<symbol id="i-*">` (Lucide style) at the top of `<body>`, used as `<svg class="icon"><use href="#i-name"/></svg>`. For a new icon, add a `<symbol>` to the sprite. Colour comes from `currentColor`.
- **Projects:** the main backend project (API REST + CI/CD + SDKs + Docker) is ONE project shown as a single card with four `.pillar` blocks. Don't split it into separate cards. The Mobbeel internship belongs only in Experiencia.
- **The video game** (Unity psychological horror, started as the TFG) is important to the user but the portfolio is not about it. It lives as a special subsection (`#videojuego`, `.game-spotlight`) inside Proyectos, with its own red-tinted style.
- **Self-directed learning:** keep it visible (hero, the `.learning` box in Sobre mí, first item in the timeline).

## Structure of `index.html`

- **CSS:** colour tokens and gradients live in `:root` (dark purple theme). Blocks are separated by `/* ---------- Section ---------- */` comments in page order. The responsive breakpoints are at the end: `900px` and `720px`, plus `prefers-reduced-motion`.
- **Sections** (`<section id>`): `inicio`, `sobre-mi`, `habilidades`, `proyectos` (which contains `#videojuego`), `experiencia`, `contacto`. The nav links point at these ids, and the scroll handler marks the active link from `main section[id]`. If you add or remove a section, update the nav too.
- **JS** (at the end of the file):
  - typing effect driven by the `roles` array;
  - an `IntersectionObserver` that adds `.visible` to every `.reveal` and animates the counters `[data-count]` / `data-suffix`;
  - scroll progress bar, active nav link and mobile menu;
  - 3D tilt on `.project`;
  - "copy email" button;
  - lightbox (`<dialog id="lightbox">`) for the game screenshot.
- **Game screenshot:** the `<img>` inside `.game-media` adds `.has-img` to its parent `onload` and removes itself `onerror`. That way the placeholder shows if the image is missing, and the lightbox only opens when there is an image.

## Workflow

- After every round of changes, commit (message in Spanish) and push to `origin main` (`github.com/destebNC/my-portfolio`) without waiting to be asked.
