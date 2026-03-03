# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Kumbara is a Turkish-language savings tracking app ("kumbara" = piggy bank). It's a **single-file SPA** — all HTML, CSS, and JS live in `index.html`. No build system, no bundler, no package.json.

## Development

- **Run**: Open `index.html` directly in a browser
- **Deploy**: Static file hosting (no build step needed)
- **No tests or linting** configured

## Architecture

Single-file (`index.html`) with embedded `<style>` and `<script>` sections. JS code is organized with section comments (`// --- Section Name ---`):

- **Auth**: Supabase email/password auth with `onAuthStateChange` listener
- **Data layer**: Supabase client for CRUD on `kumbara_entries` and `kumbara_goals` tables
- **Badges**: 10 gamification badges (count-based and amount-based milestones), state in localStorage
- **UI rendering**: Single `render()` function rebuilds the DOM from Supabase data
- **Goal tracking**: Progress bar with confetti celebration on completion

## Tech Stack

- Vanilla JS (ES6+), no framework
- Supabase JS SDK v2 (loaded via CDN from jsDelivr)
- Supabase Auth + PostgreSQL (RLS-protected tables)
- Inter font from Google Fonts

## Database Tables

- **kumbara_entries**: `id`, `user_id`, `amount`, `note`, `entry_date`, `created_at`
- **kumbara_goals**: `id`, `user_id`, `name`, `amount`, `created_at`

## Conventions

- All user-facing text is in **Turkish**
- camelCase for JS variables/functions
- Currency: Turkish Lira (₺), formatted with `tr-TR` locale
- Dates formatted in Turkish long format
- Dark theme with emerald/teal accent colors, glassmorphic design
- Supabase anon key is intentionally public (RLS handles security)
- localStorage keys: `kumbara_seen_badges`, `kumbara_goal_celebrated`
