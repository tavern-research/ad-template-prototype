# Ad Template Prototype

An **interactive UX prototype** (a clickable mockup — not production code) that explores a
more intuitive way to create batches of AI-generated political/advocacy ad videos in
Tavern by **reusing the parts of past videos that already performed well**.

## Why this exists

Today, starting a new batch means filling out one long form from scratch every single time
— scripts, voiceover, soundtrack, creative direction, visual style, and skills/templates —
with no easy way to reuse what worked in a high-performing past ad. This prototype shows an
alternative: an Apple-clean, skimmable flow where you can **cherry-pick proven ingredients**
or step through a **guided wizard** instead of wrestling with a cramped form.

## What's new in v2

A third tab — **Bulk Voiceovers** — lets you generate the final voiceovers for many scripts
at once. You assemble a list (up to **50 rows**), pairing each script with a voiceover artist,
then hit **"Generate N final voiceovers"** to produce them in one pass. Any row that has a
script but **no voice assigned** is flagged **"Needs voiceover"** and prompts you to resolve it
two ways: **Generate** (mock TTS — pick a voice from the roster, watch it go *generating →
generated*) or **Upload** (confirm a filename / pick a mock file). Resolved rows show the voice
with an origin tag (**Roster / Generated / Uploaded**), and the bulk action won't run until
every row has a voice. See [Bulk Voiceovers](#3-bulk-voiceovers) below for details.

## What you can do in it

Open it and use the **tab switcher** at the top to move between three ideas:

### 1. Winning Videos Library
Browse past high-performing ads as a gallery. Each card shows its performance stats
(CTR / views / watch-through) and **every ingredient that went into it** — Script,
Voiceover artist, Soundtrack, Creative Direction, Skill/Template, and Visual Style.

- **Mix and match across videos:** tap individual ingredients from *different* winning
  videos and they collect in a running **New Batch composer** on the side — e.g. the script
  from one ad, the voiceover from another, the soundtrack from a third.
- **Bring your own:** don't want to reuse a past ad's piece? Write a **custom script**, pick
  a **voiceover** from a roster *or upload your own*, pick/upload a **soundtrack**, write
  **custom creative direction**, choose a **template skill**, or configure a **visual style**.
- **Origin tags:** every pick is labeled by where it came from — *Custom / Uploaded /
  Roster / Library / from a specific video* — so the recipe stays clear.
- Finish with **Create Batch** to see a confirmation summary of the assembled recipe.

### 2. New Batch Flow
A guided **8-step wizard** that replaces the cramped single form: Start → Project → Scripts
→ Voice & Audio → Creative → Visual → Skills → Review.

- **Prefill from a "winning recipe"** to start from a proven setup, or start from scratch
  with **smart defaults** already filled in.
- A **live recipe summary** updates as you go, and a **final review** confirms everything
  before you create the batch.
- Voice & Audio supports *Agent decides / pick from a roster / upload your own*, and the
  backing track supports *pick from the library / upload audio* — all tagged by source.

### 3. Bulk Voiceovers
*(new in v2)* A focused workspace for pairing many scripts with voiceover artists and
generating the final voiceovers in bulk.

- **Build a list of up to 50 rows.** A running **N / 50** counter is shown, and "add" is
  disabled with a gentle note once you hit the cap.
- **Populate rows fast:** add individual scripts **from the library**, write a **custom
  script**, or **bulk-add all library scripts** at once. Remove any row, and assign or
  reassign its voiceover artist from the **6-artist roster** at any time.
- **Missing-voiceover prompt:** any row without a voice is clearly flagged **"Needs
  voiceover"** and offers two actions — **Generate** (simulated TTS using a roster voice) or
  **Upload** (mock file). Once resolved, the row shows the voice and its **Roster / Generated /
  Uploaded** origin tag.
- **Bulk generate:** **"Generate N final voiceovers"** validates that no rows are still
  missing a voice (pointing you to resolve them if so), then shows a confirmation summary
  listing every script ↔ voiceover ↔ origin. *(Prototype — no audio is actually rendered.)*

## Template Skills referenced

The **Skill / Template** ingredient maps to the real visual/style templates in
`tavern-research/delivery-video/ad-assets/templates`. The ones referenced here:

| Template | What it looks like |
| --- | --- |
| `front-porch-positive` | Warm, hopeful neighborhood tone — soft lower-third name bar, gentle civic captions. |
| `two-panel-skewed-bar` | Authoritative side-by-side layout (candidate + endorsers/contrast) with an angled lower-third bar. |
| `documentary-negative` | Desaturated, urgent attack-ad look — hard cuts and slamming headline cards. |
| `dossier` | Investigative "paper trail" style — stamped documents, redaction bars, citation footnotes. |
| `clean-letterbox` | Cinematic letterboxed framing — restrained titles, archival-to-present dissolves. |
| `riso-poster-stamp` | Bold riso-print poster aesthetic — oversized word-by-word captions, duotone stamps. |
| `soft-rounded-civic-pill` | Friendly, approachable captions in soft rounded "pill" shapes with a gentle name bar. |
| `condensed-red-banner` | Punchy condensed banner captions with deadline/urgency emphasis (great for GOTV). |
| `lower-third-positive` | Clean lower-third name bar with full-line captions and calm, positive pacing. |

*(Descriptions are plain-language summaries based on each template's intent; they're the
visual/style presets the Skill/Template ingredient points at.)*

## How to view it

- **GitHub Pages:** https://tavern-research.github.io/ad-template-prototype/
- **Or open locally:** open `prototype.html` (or `index.html`) in any modern browser.
  It needs a network connection on first load to pull React + Babel from a CDN; everything
  else (code, styles, sample data, placeholder posters) is inline.

`index.html` is a duplicate of `prototype.html` so GitHub Pages serves the prototype at the
site root. It's a single, **no-build, self-contained** file — nothing to install or compile.

## Status

This is a **prototype / mockup** built with **invented sample data**. It is not connected to
real production data, and creating a batch here does not render anything — it just shows the
intended experience.
