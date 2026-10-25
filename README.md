# Sinan & Asmin — Mother of Pearl invitation

Reference: https://www.thedigitalyes.com/demo/mother-of-pearl

## Pages

- `sinan/` — groom's side: names read "Muhammed Sinan & Asmin Nishana", groom's family card first, calendar file `nikah.ics`.
- `asmin/` — bride's side: names read "Asmin Nishana & Muhammed Sinan", bride's family card first, calendar file `asmin-nikah.ics`.
- `index.html` at the root is the earlier single-page version.

Each page has its own canonical URL, title, Open Graph / Twitter metadata and preview image (`sinan-asmin-preview.jpg`, `asmin-sinan-preview.jpg`). Keep those JPEGs next to the hosted pages; link crawlers fetch them by their public URL.

## Opening sequence

The envelope stays sealed on the S & A wax-seal cover until the guest taps anywhere (or activates the open button). The opening is coded (CSS keyframes, no video):

1. **Envelope opens onto the card** — the cover is split into three transparent layers cut from `opening-cover.webp` along the envelope's own crease lines: `envelope-pocket.webp`, `envelope-flap.webp` and `envelope-seal.webp`. The pocket area that was hidden under the seal was filled from the approved reference film. At the tap the static cover is swapped for these identical layers, then the top flap tilts up and slides off the top carrying the seal (2.9 s), while the pocket accelerates down off the bottom (3.4 s). The pearl-bordered Bismillah card sits directly underneath, so the envelope opens straight onto the design with no blank stage. Timings were matched to the reference film by tracking the seal frame by frame.
2. **Blessing** — at 2.8 s, as the last of the pocket leaves, the Arabic calligraphy from the supplied PDF writes right-to-left, followed by "In the name of Allah". Bismillah MP3 plays with this scene.
3. **Invitation** — when the Bismillah ends, the blessing fades and the names appear; Ayat MP3 fades in and loops.

If the envelope layers have not loaded within 2.5 s of the tap, the cover fades straight onto the card instead. "Skip introduction" is available throughout. With reduced motion enabled, the envelope animation is skipped and the page goes straight to the blessing.

## Sound

Bismillah and Ayat play with their scenes. The mute control silences tracks and effects; each reload starts with sound enabled. Browsers may block audible autoplay; the first tap retries at the current scene position so the track stays synchronized instead of restarting.

## Content

Personal details come from New Invitation 02.pdf, with the groom's address updated at the user's request to Meethale Peedikayil (H), P.O.: Muthuvadathur. Event: Saturday, 19 December 2026, 10:30 AM India Standard Time, Athafy Auditorium, Vallikkad, Muttungal, Vadakara.

Both pages show the full family cards (bride: D/O. …, Nadalakkandiyil House, Narikkuni PO, Calicut; groom: S/O. …, Meethale Peedikayil (H), P.O.: Muthuvadathur), a live countdown, Get directions, Save the date (.ics download) and the contact number. Pinyon Script, with larger initial capitals, is reserved for the couple's names; the location heading uses Cormorant. No video player controls, vendor branding, RSVP, hotel, transport, dress-code or gift sections are included.

All personal text can be edited directly in each page's `index.html`. Fonts, audio and most textures are embedded in the page; the cover, envelope layers and paper textures are loaded from this folder.

## Monogram

Monogram assets were edited with the built-in image generation tool. Prompt: "Precisely change ONLY the embossed monogram C & J to S & A, maintaining the same elegant interlocked calligraphy, material, lighting, texture, composition and framing; preserve everything else."

## Checks

Checked in headless Chromium at 390 × 844 and 1280 × 800: envelope layers line up exactly with the cover, flap/pocket timing against the reference film, fallback when the layers are blocked, countdown ticking, links and family cards on both pages. Not tested on a physical iPhone.

Live: https://muhdaliasbappu.github.io/sinan-asmin-invitation/
