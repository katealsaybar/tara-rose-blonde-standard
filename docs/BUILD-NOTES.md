# The Blonde Standard, build notes

## Pass 1, 27 Aug 2026: the standalone page exists

Built from Kate's build brief (27 Aug), on the junior page's conventions: the
same shared design system (`trs-core.css`, `trs-blocks.css`, `fonts.css` and the
four woff2 files, copied byte for byte from `a junior experience`), a page-only
sheet at `css/blonde-standard.css`, and the same four-script JS layer. The page
ships `noindex,nofollow` and carries **zero price tokens, zero week numbers, zero
named stylists and zero branch promises**, all by instruction.

**The standalone only.** The repo name, the slug and whether a
`tara-rose-pages-main` second copy exists were flagged for Kate to confirm and
she had not answered when the build ran, so per the brief this pass built the
standalone in `blonde framework 2026/` and left the port as an open item. No
GitHub repo has been created and nothing is pushed; the brief's "committed and
pushed, live URL re-checked" closes only after Kate names the repo.

### The page order, as shipped

nav · hero · her words (#her-words) · it is not you (#environment) · name your
lane (#lanes) · the rhythm, on black (#rhythm) · in the chair (#chair) ·
insurance (#insurance) · promise, on black (#promise) · identity shift (#shift)
· book (#book) · faq, on black (#faq). The brief's canonical order, exactly.

### How the seven resolved conflicts were executed

1. **Order:** as above, nothing moved. Her words sits directly under the hero,
   above every selling section.
2. **Release-the-blame is structural.** Each section lands its own version:
   her words ("none of them is a complaint... nobody has ever read it back to
   you"), environment ("your hair did not let you down and neither did you"),
   lanes ("you had a lane nobody ever named for you"), rhythm ("you were not
   forgetting to book, nobody ever gave you the plan"), insurance ("the purple
   shampoo did not fail you, nobody finished the sentence"), promise (Campaign
   2's own wording).
3. **No week numerals anywhere.** The three touchpoints are named One-words
   only (Create · Protect and maintain · Top-up). Each `.tstep` carries one
   hidden `<span class="tp-weeks">` as the single token slot per touchpoint for
   when Tara picks a rhythm, and the copy says the stylist gives her her weeks
   in the chair. Tara had not picked when this pass shipped.
4. **No tier names.** The three lanes only: Soft · Signature · Transformation
   Blonde, one card each, no prices, no durations, each ending with one
   where-it-sits line. Balayage is one line under the cards, explicitly a
   placement technique inside the family, never a fourth lane.
5. **No *physics*.** The idea ships as the cleared locked line, "The
   environment moves your colour. Your plan holds it.", as the environment
   section's anchor. The one analogy on the page is the manicure topcoat, a
   beauty analogy per the rule; no household comparisons.
6. **No branch promise.** The salon selector stays (same six options as the
   junior form), the help text and the FAQ both say we confirm the stylist and
   the booking at her chosen salon before anything is fixed, "all four
   branches" appears nowhere, and the footer contact link reads "Find your
   salon". JSON-LD HairSalon nodes carry addresses only, no makesOffer.
7. **No prices.** No price token anywhere, no Offer or price markup in the
   JSON-LD, and the cards are designed complete without a number (the
   where-it-sits line or the Because sits where a price block would). The only
   CTA on the page is the free consultation. The FAQ answers "What does it
   cost?" honestly: it depends on the lane, and the free consultation is where
   she leaves knowing every number before committing.

### Verbatim sources, so nobody re-derives them

- **Her words pairs:** the five pairs exactly as the brief (and The Blonde
  System page) give them, both halves untouched, labels "You say" / "What's
  actually happening". On a phone the two halves stack inside one bordered
  card, so the pairing survives; they never split into two lists.
- **The Promise:** the full Campaign 2 ad copy, lifted exactly, headed by its
  first line as the lead. Never called anything but a Promise.
- **The identity shift:** the three pairs from The Blonde System. The source's
  em dashes are rendered as full stops (house style bans em dashes; the brief
  itself renders Tara's em-dashed lines with commas), nothing else changed:
  "I'm not high maintenance. I've finally got the right plan." and "My blonde
  is protected at every stage. Bond repair is the standard."
- **The Becauses:** verbatim in quotes on each insurance card, lowercase as
  written, comma rendering as in the brief. Bundle contents from The Blonde
  System's retail table (BlondMe pair · Fibre Clinix Bond Repair Mask · thermal
  spray, shower water filter, UV protectant).
- **Tara's locked lines:** all five ship verbatim, one place each. The
  brassy/canvas line anchors her words; environment/plan anchors the
  environment; high-maintenance/plan is the hero support line; toner/finish
  line anchors the rhythm; closer-blonde/protection anchors in-the-chair.
- **Bond protection named:** Fibreplex, Olaplex, K18, in the chair section and
  the damage FAQ, because naming it is the proof.

### The tracking layer

Junior page's layer, same mechanics: UTMs, gclid/fbclid stores, first/last
touch, session ref (prefix `TBS-`) appended to the WhatsApp links,
`?branch=`/`?channel=` from the URL winning over the form, derived fields
clearing as well as filling. `campaign:blonde-standard-2026`.

**One mapping decision to flag to Emma.** The brief says to copy the junior
page's GHL `offering` vocabulary, and blonde lanes are not in it, so no new
values were invented: the three lanes and "never been blonde" map to
`colour-package`, "keeps going warm" to `toner-reset`, "dry or rough" to
`treatment-blowdry`, "not sure" to blank. The raw self-selection (lane or
symptom) travels in `product`, so the pipeline can still tell a named-lane lead
from a symptom lead. If Emma wants blonde-specific offering tags instead, it is
one map in `js/tracking.js`.

Form endpoint is the same `__FORM_ENDPOINT__` template as the junior page,
inert until the GHL webhook is set.

### What was verified, 27 Aug

- 375, 390, 768 and 1280: `scrollWidth` never exceeds the viewport, no element
  overflows its box, no console errors.
- JSON-LD parses; the FAQPage mirrors the visible FAQ **byte for byte** (seven
  questions; one typographic-apostrophe mismatch was caught and fixed).
- No dead `href="#..."` anchors.
- Source-level banned-word sweep: clean. The only greppable hits are "depends
  on" and the mandated `offering` field name, neither of which is copy.
- No price digits, no AED, no ppm or hardness figure, no em dashes.
- Form behaviour: submit disabled until every required field is satisfiable,
  lane cards prefill the reason select, "a friend told me" reveals the
  who-should-we-thank field, transformation+Saadiyat derives
  `colour-package`/`abudhabi`/`abudhabi`, switching to "not sure" clears the
  derived fields, a `?branch=dubai-alquoz` URL keeps its branch tag after she
  picks Khalifa City (attribution wins, her answer stays in `salon`/`emirate`),
  and the WhatsApp link carries the session ref.
- Environment note: the preview pane would not composite for screenshots
  (known quirk, recorded on the junior build too), so the width checks were
  measured via `scrollWidth`/`getBoundingClientRect` rather than eyeballed
  frames. Worth a human scroll on the Pages URL once the repo exists.

### Design decisions this pass made

- **Text-first hero, centred.** No blonde photography with consent exists (the
  brief's own open item), and the junior build already established that
  borrowing another campaign's photographs is a fault. So the page carries no
  photographs at all this pass, and the hero gives the support line, "You're
  not high maintenance. You've never had the right plan.", real size as the
  emotional hook. Photography slots in later without reflowing anything.
- **FAQ is on black** per the canonical order, which means it sits above the
  dark footer. The junior page stepped its FAQ to light for exactly that
  adjacency; if Kate wants the same here it is one class and four override
  rules.
- **The environment section names the five** (sun, pool, hard water, air
  conditioning, SPF) as five small cards with one soft mechanism line each, no
  numbers anywhere.
- OG image meta points at the production path
  (`/og/blonde-standard.jpg?v=1`), junior-page convention; the file does not
  exist yet, so shares render blank until it does.

### Still open after this pass

- **Kate: the repo name and slug**, and whether the `tara-rose-pages-main`
  second copy should exist yet. Until then: no GitHub repo, no push, no port,
  no `build.py --check`.
- **Which rhythm.** Week 7/12 or 4-6/8-12. Only Tara. The token slots are in
  the markup; the copy already reads correctly either way.
- **The stylist sign-off table** (four stylists, eight treatment families,
  dated, signed). Decides one-branch vs four-branch, and gates geo-targeting.
- **The deposit exemption in writing**, or the funnel is modelled wrong. The
  page already routes everything through the free consultation, which is the
  safe side of that question, but the exemption still needs to exist.
- **The from-price content file** for blonde. Does not exist; two published
  prices contradict elsewhere.
- **Blonde proof.** No before/after, no blonde testimonial, no client consent
  on file. The page ships without proof and that is the biggest thing missing.
- **Photography**, same consent gate as proof. The page is deliberately
  text-first until it exists.
- **The OG image file** at `/og/blonde-standard.jpg`.
- **`trs-brand-guardian` has not seen any of this copy.** Every visible
  sentence on the page is client-facing and new (or locked-verbatim), and the
  gate has to run before hand-off.
- **`/your-blonde-journey` still says five branches plus Bahrain** elsewhere.
  Not this page's job; nothing was copied from it.
- **Emma's yes/no on the `offering` tag mapping** above.

### Settled, do not reopen

- **No discount in any form.** The page's argument is that blonde is a plan,
  and a plan is not a thing you take 30% off.
- **The Blonde Pack's claim that no blonde campaign exists in Notion is
  wrong.** The Blonde System is the source; two of its findings (sign-off gap,
  deposit rule) survive as open items above.
- **The three visits are Tara's, not Daisy's.** The journey shipped; no package
  exists on the page to price.
- **Tier names.** Two vocabularies are live and *ritual* is banned; the lanes
  are the client-facing names. Do not reintroduce Essential/Reset/Ceremony here.
