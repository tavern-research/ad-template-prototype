# Ad Template Prototype

An interactive UX prototype for Tavern's ad-video tooling. It's a single,
self-contained HTML file — **open `prototype.html` (or `index.html`) in any modern
browser** to use the clickable mockup. No build step and no local dependencies; React 18
and Babel load from a CDN, so the first paint needs a network connection. All component
code, styles, sample data, and placeholder posters are inline.

## What's inside

A top **tab switcher** toggles between two prototypes:

- **Winning Videos Library** — a gallery of high-performing ads. Tap any of six
  "ingredient" rows (Script, Voiceover, Soundtrack, Creative Direction, Skill/Template,
  Visual Style) across different videos to assemble a new batch in a sticky composer. The
  composer enforces single- vs multi-value conflict rules and ends in a Create Batch
  confirmation. It also has an always-visible **"Add your own"** strip: write a custom
  script, pick a voiceover from a roster *or* mock-upload a file, pick a soundtrack from
  the library *or* upload audio, write custom creative direction, choose from the full
  template list *or* add a custom note, and configure a custom visual style. Every pick is
  tagged by origin (Custom / Uploaded / Roster / Library / from {video}).

- **New Batch Flow** — an 8-step Apple-clean wizard (Start → Project → Scripts →
  Voice & Audio → Creative → Visual → Skills → Review) with prefill-from-recipe, a
  persistent live recipe summary, and a Create Batch confirmation. Voice & Audio supports
  *Agent decides / Pick from roster / Upload your own* and *From library / Upload audio*,
  flowing into the summary and Review with source tags.

"Upload" is simulated: confirm a typed filename or tap a mock file chip, and the value is
tagged **Uploaded**.

## Notes

`index.html` and `prototype.html` are identical — `index.html` exists so GitHub Pages can
serve the prototype at the site root. Placeholder posters are inline flat SVG color blocks,
so the file works offline after the initial CDN load.
