# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

This is **not a software application** — it's a set of static, standalone Chinese-language reference/study pages that summarize fire-protection engineering standards for semiconductor fab facilities, plus the original source PDFs they're derived from. There is no build system, package manager, server, or test suite. Pages are meant to be opened directly in a browser or served as static files (e.g. GitHub Pages).

Author context: the content is written by a TSMC fire protection engineer ("騏佑") as a personal reference/training series. It's part of a small family of sibling sites (this repo plus `beartechnician.github.io/osh-manager`) cross-linked to each other.

## Files

- `index.html` — FM Global **Data Sheet 7-7** (Semiconductor Fabrication Facilities) Chinese summary. The "main"/flagship page of this repo.
- `nfpa13.html` — **NFPA 13** (Standard for the Installation of Sprinkler Systems) Chinese summary.
- `ds20.html` — FM Global **Data Sheet 2-0** (Installation Guidelines for Automatic Sprinklers) Chinese summary.
- `intro.html` — "消防系統速成班" — a crash-course/primer page for colleagues without a fire-protection background; links out to the three detailed pages above.
- `FMDS0200.pdf`, `NFPA 13.本）.pdf` — original source standards documents that the summaries are translated/condensed from. Treat these as reference source-of-truth when verifying or expanding a summary; do not edit them.

Each HTML file is fully self-contained: one inline `<style>` block, no `<link>` stylesheets, no `<script>` tags, no external assets or CDN dependencies. There is no shared CSS file — the same design system is duplicated in each page's `<head>`.

## Working with these files

There is nothing to build, install, lint, or test. To preview a change, just open the HTML file directly in a browser (or any static file server) — there is no dev server command.

When editing content, always cross-check against the corresponding source PDF (`FMDS0200.pdf` for `ds20.html`, `NFPA 13.本）.pdf` for `nfpa13.html`) rather than inventing or guessing clause text.

## Content structure conventions

Each summary page follows the source standard's own clause/section numbering, not an independent outline — this lets readers cross-reference back to the original document:

- Top-level `<div class="section" id="sN">` blocks correspond to major numbered sections of the source standard.
- `<span class="clause-ref">2.4.3</span>` marks the specific clause number a bullet/paragraph/table summarizes — always precedes the summarized text, matching the source document's numbering exactly.
- The sidebar `<nav class="toc">` (desktop) and `<nav class="mobile-nav">` (mobile, hidden on desktop) both link to the same section `id`s and must be kept in sync when sections are added/renamed.
- Sections/subsections not yet summarized are marked incomplete inline (e.g. "...，待補" — "to be completed") or given `class="pending"` in the TOC (dimmed, italic) rather than being silently omitted — this keeps the TOC representing the full source outline even for gaps.

Reusable UI vocabulary shared across pages (defined per-page in the inline `<style>`, same class names/semantics everywhere):
- `.section` / `.section-header` / `.section-num` (with color modifiers `danger`/`purple`/`green`/`yellow`/`muted`) — section containers and their numbered badges.
- `.clause-ref` — inline clause-number tag preceding summarized text.
- `.clause-table` — tables presenting clause data (e.g. spacing/area/hazard-class tables).
- `.tag` with `green`/`yellow`/`red` modifiers — hazard/severity level badges (e.g. Light/Ordinary/Extra Hazard classifications).
- `.callout` with `info`/`green`/`danger` modifiers — highlighted notes/warnings.
- `.std-card` / `.std-id` / `.std-desc` — cards linking to sibling standards/pages.
- `.stat-card` / `.stat-grid` / `.stat-value` (with `red`/`yellow` modifiers) — key-number highlight blocks.

The `.header-meta` block at the top of each page records source edition/date, page count, summarization progress, compilation date, and author, plus cross-links to the sibling pages — update this metadata (especially 整理進度/progress and 整理日期/date) whenever a page's content coverage changes.

## Terminology conventions (important)

This content is domain-specific fire-protection engineering Chinese, and precise terminology matters because readers cross-reference back to Taiwanese/industry standard usage:

- Use **撒水** (not 灑水) for "sprinkler"-related terms (撒水系統, 撒水頭, 撒水系統配管, etc.) — this was an explicit fix applied across all pages (see commit `0b4decc`); do not reintroduce 灑水.
- Preserve the pattern of giving the English standard term alongside the Chinese translation on first use in a section (e.g. `製程安全（Process Safety）`, `Standard-Spray Automatic Sprinkler / 標準噴撒型撒水頭`).
- Keep numeric/unit conventions consistent with existing tables (dual imperial/metric where the source gives both, e.g. `8 ft (2.4m)`).

## Cross-linking

Pages link to each other via relative paths (`index.html`, `nfpa13.html`, `ds20.html`, `intro.html`) and to the external sibling site `https://beartechnician.github.io/osh-manager/`. When adding a new page or renaming an existing one, update the `.header-meta` cross-link block in **every** existing page, not just the new one.
