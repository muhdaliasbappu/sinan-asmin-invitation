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

After the opening tap, a tap or click anywhere (or "Skip introduction", or Esc) jumps straight to the invitation details. Skipping never interrupts the sound: the Bismillah always plays to its end and is then followed by the looping Ayat; if the envelope had not reached the blessing yet, the Bismillah starts at the skip. If the envelope layers have not loaded within 2.5 s of the tap, the cover fades straight onto the card instead. If the Bismillah recording cannot play (autoplay blocked, Low Power Mode, in-app browsers), the blessing still moves on to the names after the recording's length, and the next tap plays the Bismillah and then the Ayat. With reduced motion enabled, the envelope animation is skipped and the page goes straight to the blessing. Until the invitation is revealed the page cannot scroll: the body is pinned (iOS Safari ignores `overflow:hidden` for touch scrolling), swipes and the mouse wheel are cancelled, and the invitation is hidden, so nothing moves or shows behind the envelope and blessing.

## Layout

Phones in portrait use the full screen width. On anything wider (tablets, phones in landscape, desktops) the envelope, blessing and invitation are shown as one centred phone-shaped column on a plain #e6e1d9 backdrop: the opening keeps the 9:16 envelope frame, and the invitation column is min(560px, 56.25svh) but never narrower than 400px.

## Sound

The audio runs independently of the visuals: Bismillah first (once, to the end), then Ayat fading in and looping. Muting keeps the sequence running silently, so unmuting continues at the right recording. Leaving the tab pauses the sound and returning continues the same recording. Browsers that refuse to start sound get it on the next real tap. Both recordings play through one audio player (the Ayat is swapped in after the Bismillah), because iOS plays one page sound at a time and unlocks each player separately; the embedded MP3s are played from blob URLs. The end of the Bismillah is detected from the `ended` event, its position reaching the end, or playback no longer advancing, since iOS Safari does not always fire `ended`; the blessing also moves on by itself at most 2.5 s after the recording's length.

## Colours

The page always shows its own light colours, whatever the phone's theme. Android browsers that darken pages (Samsung Internet, in-app WebViews in WhatsApp/Instagram/Gmail, Chrome's auto-dark, phone makers' dark modes) leave a page alone only when it declares its own dark theme, and `only light` does not count as one. So the root declares `<meta name="color-scheme" content="light dark">` and `:root{color-scheme:light dark}`, a `prefers-color-scheme: dark` block restates the same light colours, and `body{color-scheme:only light}` keeps everything inside on light defaults. iOS Safari does not recolour pages.

## Content

Personal details come from New Invitation 02.pdf, with the groom's address updated at the user's request to Meethale Peedikayil House, P.O. Muthuvadathur, Purameri, and the bride's grandfather as Moosakoya Haji Mannangara. Event: Saturday, 19 December 2026, 10:30 AM India Standard Time, Athafy Auditorium, Vallikkad, Muttungal, Vadakara.

Both pages show the full family cards (bride: D/O …, Nadalakkandiyil House, Narikkuni P.O., Calicut; groom: S/O …, Meethale Peedikayil House, P.O. Muthuvadathur, Purameri), a live countdown, Get directions, Save the date (.ics download) and the contact number. The closing signature is "Asmin & Sinan" on the bride's page (couple-name script) and "Thayyil Family & MP Family" on the groom's page, set in Cormorant Garamond Italic 500 (SIL OFL, embedded) for readability. Pinyon Script, with larger initial capitals, is reserved for the couple's names; the location heading uses Cormorant. No video player controls, vendor branding, RSVP, hotel, transport, dress-code or gift sections are included.

All personal text can be edited directly in each page's `index.html`. Fonts, audio, the envelope layers and the pearl strip are embedded in each page, so a page still opens and animates correctly even if it is opened on its own; only the decorative paper textures and the .ics calendar files are loaded from this folder.

## Monogram

Monogram assets were edited with the built-in image generation tool. Prompt: "Precisely change ONLY the embossed monogram C & J to S & A, maintaining the same elegant interlocked calligraphy, material, lighting, texture, composition and framing; preserve everything else."

## Checks

Checked in headless Chromium at 390 × 844 and 1280 × 800: envelope layers line up exactly with the cover, flap/pocket timing against the reference film, fallback when the layers are blocked, countdown ticking, links and family cards on both pages. Not tested on a physical iPhone.

Live: https://sinan-asmin.com/
