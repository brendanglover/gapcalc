---
name: gapcalc-conventions
description: Use when building, editing, or reviewing anything in the GapCalc project. Defines the full design system, calculator structure, brand rules, and workflow conventions.
---

# GapCalc Project Conventions

## Brand & Design System
- Accent colour: #f5820a (orange)
- Headings: Bebas Neue
- Numbers/outputs: DM Mono
- Theme: Dark industrial, dark background first
- Layout: Card-grid homepage, individual calculator pages
- Tone: No-nonsense, practical. No emoji in copy.

## Rules
- Always explain a change before making it
- Never change the colour scheme or typography without approval
- Never add dependencies or npm packages
- Bump patch version in footer for any meaningful update
- Three separate Git commands always: git add . then git commit then git push
- Commit messages: lowercase, descriptive, no emoji
- Do not add calculators without a full spec discussion first

## Stack
- Vanilla HTML/CSS/JS only, no frameworks, no build steps
- Google Analytics installed - never remove the GA script tag
- Hosted on Cloudflare Pages - push to main to deploy
