# Ad Template Prototype

An **interactive UX prototype** (a clickable mockup — not production code) that explores a
more intuitive way to create batches of AI-generated political/advocacy ad videos in
Tavern by **reusing the parts of past videos that already performed well**.

## Why this exists

Today, starting a new batch means filling out one long form from scratch every single time
— scripts, voiceover, soundtrack, creative direction, visual style, and skills/templates —
with no easy way to reuse what worked in a high-performing past ad. This prototype shows an
alternative: an Apple-clean, skimmable flow where you can **cherry-pick proven ingredients**
inside a single Bulk Studio that handles both quick batches and per-video fine-tuning,
instead of wrestling with a cramped form.

## What's new in v2

The standalone **New Batch Flow** wizard tab has been removed and folded into **Bulk Studio**
via a top-of-tab **Mode toggle**. Bulk Studio now offers two modes: **Quick batch** (one
shared recipe — voiceover, soundtrack, creative direction, multi-skill stack, visual style —
applied to every script in the batch, with per-row cards collapsed to a script-only editor)
and **Per-video customization** (the existing Library-style expandable cards where each
video has its own full six-ingredient recipe). Mode is persisted; switching from Quick →
Per-video preserves your per-card data and offers a "Copy shared recipe to each card?"
prompt that fills only fields not already set per-card. The new IA is **Library → Bulk
Studio → Skills**.

A **Skills** tab is a browser for the full template library — every skill the bulk flow can
layer onto a video. Each skill renders as a Library-style card with a flat poster preview,
the kebab-id name (e.g. `front-porch-positive`), a one-sentence description, an inferred
tone (Positive / Contrast / Persuasion), and chips listing which winning videos use it. A
**Use in new batch** button on each card jumps to **Bulk Studio** (Per-video mode) and
creates a fresh row pre-attached with that skill in its multi-skill chip set. **Multi-select
is supported**: tap any card (or its checkbox) to add it to a selection, and a sticky
header action bar appears with a running count, a **"Use N skills in new batch"** primary
CTA that hands the whole stack off to a single new Bulk Studio Per-video card, and a
**Clear selection** button. Selections persist across filter changes (hidden selections
stay in state and are noted in the action bar). The header has a stat strip (skills in
library, used by winning videos, winning videos covered) and filter pills (All / Used /
Unused / Positive / Contrast / Persuasion).

In Bulk Studio, **each expanded video card now matches the Winning Videos library card
visually**: video-sourced rows render with the flat-color **poster + play glyph + duration
and format chips + performance badge**, the title + category, and the **CTR / Views /
Watch-through** stat strip — exactly like a winning-video card — followed by the same six
ingredient rows the Library card uses (with the swap/pick/add-skill chip pattern that
shipped earlier). Library, custom, upload, and skill-prefilled cards omit poster/badges/stats
(no invented metrics) but render the same six ingredient rows.

A new inline **Play preview** lives on each expanded bulk card. If the row has an
**uploaded** voiceover with the actual audio file (from the multi-audio drop zone), it plays
that file via an `<audio>` element and `URL.createObjectURL`. For **Roster / Generated /
From-{video}** voices (no real audio in the prototype), it uses the browser's
**Web Speech API** (`speechSynthesis` + `SpeechSynthesisUtterance`) to read the row's script
aloud, picking a `SpeechSynthesisVoice` whose name token matches the chosen voice (with an
English fallback). The button is disabled with the tooltip "Add or generate a voiceover to
preview" until a voice is set, and the card honestly notes "Audio preview unavailable in this
browser" if `speechSynthesis` is missing. Audio is cleaned up on stop, row removal, or unmount.

**Bulk Studio** lets you build a batch of up to **50 videos** at once. In Per-video mode,
**each video expands into the same six-ingredient editor as a Winning Videos card**; in
Quick batch mode, every script renders with one shared recipe.
Collapsed, a card shows a compact summary (index, title, voiceover status, ingredient
indicators, and a **skills: N** count); expand it and you get the familiar Library-style rows
for **Script, Voiceover, Soundtrack, Creative Direction, Skill/Template, and Visual Style**,
each with an inline **Swap / Pick / Add skill** picker that lets you choose from a winning
video, the roster/library, write/upload your own, or layer multiple skills. **Pulling a
winning video prefills the entire recipe** (tagged **"From {video}"**) and every field stays
editable. **Skills are multi-select per video** — winning-video skills come over as chips,
you can keep adding more from the full template list, remove any with **✕**, and the final
summary lists every attached skill. **Bulk uploads** speed up batch building: drop a
**`.csv`, `.txt`, or `.docx`** file to create a row per parsed script (CSV honors a
`script/text` + `title/id` header, TXT splits on blank-line paragraphs or per-line,
**`.docx` parsing is simulated** in the prototype with a "Preview parse — real .docx import
will run server-side in production" note), or **drop multiple audio files** (`.mp3 / .wav /
.m4a / .ogg`) and they **pair into existing rows by filename** (case-insensitive, ignoring
punctuation/spaces/extension) — unmatched audio becomes new script-blank rows tagged
**Uploaded**. Any card without a voice is flagged **"Needs voiceover"** and is resolved with
**Roster / Generate / Upload / From a winning video**, with origin tags. The primary CTA —
**"Generate N videos"** — validates every card has a voiceover (expanding and pointing you
to unresolved ones) and confirms the full per-video recipe. See
[Bulk Studio](#2-bulk-studio) below for details.

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

### 2. Bulk Studio
*(new in v2 — replaces the standalone New Batch Flow tab)* A workspace for building a batch
of up to 50 videos at once. A top-of-tab **Mode toggle** picks between **Quick batch** (one
shared recipe applied to every script) and **Per-video customization** (each video has its
own full six-ingredient recipe in the same Library-style card UI). Pull from winning
recipes, bulk-upload scripts and voiceovers, and either share one recipe across the batch
or fine-tune each video individually.

#### Modes
- **Quick batch** — at the top of the tab, a **Shared recipe** panel sets one Voiceover
  (Agent decides / Roster / Upload / from a winning video), one Soundtrack (Library /
  Upload / from a winning video / None), one Creative Direction textarea, a multi-skill
  stack, and one Visual Style configurator (format / duration / grade / captions). Per-row
  cards collapse to a **script-only editor** (title + script text + the Play preview, which
  read-alouds via the *shared* voiceover); the per-row Voiceover / Soundtrack / Creative /
  Skill / Visual rows are hidden and each card carries a small "Uses shared recipe" tag.
  Adding a winning video offers an **"Add script"** action *and* a one-click **"Use recipe
  for all videos"** that copies its full recipe into the shared panel. Multi-audio
  voiceover upload is disabled in Quick batch with a tooltip pointing back to Per-video
  customization. The "Generate N videos" confirmation shows the shared recipe once + the
  list of scripts.
- **Per-video customization** — the existing flow. Each card expands into the full Winning
  Videos card UI: poster + performance badge + duration/format chips + CTR / Views /
  Watch-through stat strip (for video-prefilled rows; library/custom/upload/skill-prefilled
  cards omit poster/badges/stats), Play preview, and the six ingredient rows with
  Swap/Pick/Add-skill chip pickers (multi-skill, with the "skills: N" count chip on the
  collapsed card). The "Generate N videos" confirmation lists every video's full recipe.
- **Switching modes** preserves data. Per-video → Quick keeps your per-card data hidden
  while you work in Quick mode; Quick → Per-video shows a confirm dialog **"Copy shared
  recipe to each card?"** with Yes / No / Cancel — Yes fills any per-card field that's
  still empty (voice, soundtrack, creative, skills, visual), No keeps cards as-is, Cancel
  aborts the switch.

- **Build up to 50 videos.** A running **N / 50** counter is shown, and "add" is disabled with a
  gentle note once you hit the cap. **Expand all / Collapse all** keeps the list scannable, and
  the header shows how many videos still need a voiceover.
- **Five ways to add videos:** pull a **winning video** to **prefill the entire recipe**
  (script + voiceover + soundtrack + creative + skills + visual; one at a time or **add all
  winning videos**), tagged **"From {video title}"**; add a **library script** (script only,
  other fields blank/defaults, voiceover shows *Needs voiceover*); add a **custom** blank
  card; **bulk-upload scripts** from a `.csv`, `.txt`, or `.docx` file (one row per parsed
  script); or **bulk-upload voiceovers** as multiple audio files. Remove any video at any
  time.
- **Bulk upload — scripts:** drag-and-drop or browse a `.csv`, `.txt`, or `.docx` file. CSV
  with a header row uses the `script`/`text` column for the script body and `title`/`id`
  for the row title; CSV without a header uses the first cell as script and the second cell
  as title. TXT splits into scripts on blank-line paragraphs (or one-per-line if there are
  no blank lines). **`.docx` is simulated** for the prototype — the file is read so you see
  the filename, then a small in-band note ("Preview parse — real .docx import will run
  server-side in production") confirms the simulation, and N rows are produced so the rest
  of the UX flow is identical. A status callout confirms how many rows were added (and how
  many were skipped if the 50-video cap is hit).
- **Bulk upload — voiceovers:** drag-and-drop or browse multiple `.mp3` / `.wav` / `.m4a` /
  `.ogg` files. **Filenames are paired into existing rows** (case-insensitive, ignoring
  punctuation/spaces/extension): if `working-families-promise.mp3` matches a row titled
  *Working families promise*, the voice attaches there with origin **Uploaded**; unmatched
  audio becomes a new script-blank row tagged **Uploaded** that you can fill the script in
  later. The status callout summarizes "*N paired by filename, M added as new rows*", and
  audio that pairs into existing rows still works at cap.
- **Expandable Library-style cards:** collapsed shows index, title, voiceover status, on/off
  indicators for voiceover/soundtrack/creative/visual, and a **skills: N** count chip. Expand
  to see the **full Winning Videos card UI** — for video-prefilled rows, the same flat-color
  poster with play glyph + duration/format chips + performance badge, the title and category,
  and the **CTR / Views / Watch-through** stat strip exactly like a Winning Videos library
  card. Library/custom/upload/skill-prefilled cards omit poster/badges/stats (no invented
  metrics) but render the same six ingredient rows. Below that, an inline **Play preview**
  button reads the script aloud — for **uploaded** voices it plays the actual audio file via
  `URL.createObjectURL`; for **roster / generated / from-{video}** voices it uses the
  browser's `speechSynthesis` API (matching the picked voice's name when possible) so you
  hear an honest read-aloud preview right in the prototype. The button is disabled until a
  voiceover is set; if `speechSynthesis` is missing, the card shows a small "Audio preview
  unavailable in this browser" note. Then come the **six ingredient rows**, each with a
  **Swap / Pick / Add skill** chip that opens an inline picker:
  - **Script** — title + text inline; Swap to use a winning video's script or a library script.
  - **Voiceover** — current value with origin tag; picker offers **Roster** select,
    **Generate** (mock TTS), **Upload** (mock file), or **Use a winning video's voiceover**.
  - **Soundtrack** — current track with origin tag; picker offers track library, mock audio
    upload, or a winning video's soundtrack; **Remove** clears it.
  - **Creative Direction** — inline textarea; Swap to copy from a winning video.
  - **Skill/Template — multi-select.** Attached skills appear as removable **✕** chips; **Add
    skill** opens the full template list (with **✓ Added** state on already-attached ones) and
    a "winning video skill" shortcut, so you can layer several skills on one video.
  - **Visual Style** — Format / Duration / Color grade / Captions configurator inline; Swap to
    copy from a winning video's visual style.
- **Missing-voiceover prompt:** any card without a voice is clearly flagged **"Needs
  voiceover"**, the picker is auto-shown, and the card border/background turn warning-tinted
  until resolved. Resolved voices carry an origin tag — **Roster / Generated / Uploaded /
  From {video}** — and a winning-video voice can still be swapped.
- **Generate the batch:** **"Generate N videos"** validates that every card has a voiceover
  (expanding and pointing you to any that don't), then shows a confirmation listing each
  video's full recipe — script ↔ voiceover (+origin) ↔ soundtrack ↔ creative ↔ **all attached
  skills as chips** ↔ visual. *(Prototype — nothing is actually rendered.)*

### 3. Skills
*(new in v2)* A browser for the full template library — every skill the bulk flow can layer
onto a video. Each skill renders as a Library-style card and the tab supports
**multi-select** so you can layer several skills onto a single new video at once:

- **Flat-color poster preview** seeded from the skill's id (consistent visual signature).
- **Kebab-id name** (e.g. `front-porch-positive`) plus a one-sentence description, an
  inferred **tone tag** (Positive / Contrast / Persuasion), and a "Used in N winning videos"
  count with chip-listed video titles colored by their performance badge.
- **Multi-select selection model** — every card has a checkmark ring in the top-left of
  its poster; tap the card or the ring to toggle selection. Selected cards get an accent
  border and a subtle accent-tinted background. Selection state is persisted (`skills.selected`)
  and survives filter changes — flipping between **All / Used / Positive** etc. never drops a
  hidden selection.
- **Sticky action bar** — appears at the top of the Skills tab body the moment you select
  one or more skills. It shows a running **"N skills selected"** count, a brief explainer
  ("All N skills will be layered onto a single new Per-video Bulk Studio card"), a
  **Clear selection** ghost button, and a primary **"Use N skills in new batch"** CTA. When
  the selection is empty, the bar disappears.
- **Use in new batch** (per-card) — when no other skills are selected, this primary button
  hands the single skill off to **Bulk Studio** as before. When a selection already exists,
  the per-card button shifts to a secondary **Add to selection** affordance (or **✓ In
  selection** when this card is already selected) so the bottom button can never silently
  drop a multi-select.
- **Hand-off** — the **"Use N skills in new batch"** CTA jumps to **Bulk Studio**, force-
  switches Mode to **Per-video customization**, and creates a fresh expanded card with all
  selected skills loaded into the multi-skill chip stack. The selection clears once the
  hand-off is complete (the skills now live on the new Bulk Studio card).
- The header shows a stat strip (skills in library, used by winning videos, winning videos
  covered) and filter pills: **All / Used / Unused / Positive / Contrast / Persuasion**.

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
