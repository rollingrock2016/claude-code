# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

A collection of independent, single-file business front pages. Each page is one self-contained HTML file with its CSS in a `<style>` block and its JS in an inline `<script>`. The pages share no code, and each has its own brand, palette and type.

| Page | Business | External dependencies |
|------|----------|-----------------------|
| `wealthpath.html` | Wealth Path, financial planning | None |
| `Business-frontpage/sugar_and_bloom_v2.html` | Sugar & Bloom, bakery | Google Fonts, Unsplash images |
| `Business Name/mindful_paws.html` | Mindful Paws, pet grooming | None |

## Running

There is no build step, package manager, linter or test suite. Open a page directly in a browser to run it. Verify changes there, at both desktop and narrow mobile widths.

## Conventions across the pages

- Keep each page in a single file with no framework or build tooling. New businesses get a new standalone HTML file.
- Design tokens live in `:root` custom properties at the top of the `<style>` block. Use them rather than hard-coding colors or fonts.
- Each page follows the same shape: a hero, an interactive feature (quiz or intake flow), content sections, then a booking or order form.
- All three pages honor `prefers-reduced-motion` in CSS. `mindful_paws.html` and `sugar_and_bloom_v2.html` also check it in JS for timers and scrolling, while `wealthpath.html` does not. Keep this when adding animation.
- None of the booking forms reach a real backend yet:
  - `mindful_paws.html` has a `TODO` in the submit handler, and nothing leaves the browser.
  - `wealthpath.html` posts to `BOOKING_ENDPOINT` when it is set. It is empty by default, so requests stay in `localStorage`.
  - `sugar_and_bloom_v2.html` validates and shows a confirmation, but sends and stores nothing.

## Mindful Paws details

- The `.menu-row[data-service]` elements in the Services section are the source of truth for services. The quiz reads each name, description and price from the DOM, so change a price or add a service there, not in JS.
  - Each row needs an `h3`, `p`, `.menu-price` and `.menu-book`.
  - Prices must be whole dollars: the parser strips all non-digits, so `$45.50` becomes 4550.
  - `data-dogs-only` hides a service from the cat path. `data-flat-price` skips the size surcharge.
- Size surcharges and weight hints are in `SIZE_SURCHARGE` and `SIZE_HINTS` at the top of the script.
- The paw shape is duplicated in four places: the favicon data URI, the `#paw` symbol, the hero SVG and the quiz SVG. Update all of them if it changes.
- Gallery images are placeholders. The HTML comment above `.gallery-grid` explains how to swap in a photo.
