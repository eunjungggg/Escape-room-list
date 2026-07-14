# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single static landing page (`index.html`) that lists escape-room web games built by students of 인천비즈니스고등학교 콘텐츠디자인과 (a web-programming class). Each card links out to a student's game deployed on Vercel/Netlify. Everything — markup, CSS, and JS — lives in `index.html`; there is no build step, no dependencies, and no tests. Open the file in a browser to preview; deploy by serving the file statically.

The UI is in Korean and locale is `lang="ko"`.

## Adding or editing a room

Rooms are `<a class="room-card">` elements inside `<section class="rooms">`, numbered `ROOM 01`…`ROOM 11`. To add a game, fill in an existing placeholder card (or append a new one) with:
- `href` — the deployed game URL (`target="_blank" rel="noopener"` on every card)
- `.room-title` — game name
- `.room-maker` — student, e.g. `3학년 강O연` (student surnames are intentionally masked with `O` for privacy — preserve this masking)

## The locked-card mechanism (key convention)

A card with an empty `href` is automatically disabled at runtime. The inline `<script>` at the bottom adds the `.locked` class to any card whose `href` is blank, which:
- greys the card out and shows a 🔒 (via the `.locked` CSS rules)
- calls `preventDefault()` on click so it can't be followed

Placeholder cards therefore use `href=""` and a `TO BE CONTINUED...` title. **To publish a room, just set its real `href`** — the script unlocks it automatically; do not manually add/remove the `.locked` class. Keep the header count ("총 11개의 방탈출 게임") in sync with the number of cards when adding rooms.

## Styling

All CSS is in the `<head>` `<style>` block. The dark/gold "escape file" theme is driven by CSS custom properties in `:root` (`--gold`, `--panel`, `--bg`, etc.) — change the palette there rather than editing individual rules. Fonts (Cinzel, Noto Sans KR) load from Google Fonts via `@import`.
