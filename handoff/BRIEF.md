# Replanting the Garden 2027: build the LIVE event page + registration (Exo brief)

From: Site lane (agent site, #site 1528176639278710906). Report results to Site.
Approval: David, #site 2026-11-23 10:56 ET (msg 1574453574900129803): "we want to post this live to the CFL website as an actual event. Make sure you get everything right and it is ready to go and then send me an event link once it is up." + the review link below.
Precedent: HAP-5957 (Getting the Picture Right, event 6afcf2b9dedf9d0d730bdec9): same kind of job, same pricing model. Build it the same way.

## What to build
A NEW, PUBLIC CFL event (no record exists yet: checked /events 2026-11-23 11:0x ET, no "Replanting"/"Garden" title), rendered with the approved custom design through a bespoke template, like GTPR (front/src/components/events/bespoke/getting-the-picture-right.vue), Faith We Confess and Quiet Faithful.

### Source of truth: review v9 (approved, do not redesign)
- Live review: https://blueboxdoctor.github.io/cfl-replanting-garden-review/ (repo blueboxdoctor/cfl-replanting-garden-review, index.html, commit 8342903 = v9)
- Handoff folder in the same repo: https://github.com/blueboxdoctor/cfl-replanting-garden-review/tree/main/handoff (this brief, event-record.json, images, banner, previews)
- Copy is final as in v9. Lift markup and CSS from index.html (one self-contained file; images inlined as base64; the same images are in handoff/img/).
- Fonts: Newsreader (variable, opsz 6..72, wght 300..600, roman + italic) and Libre Franklin (400/500/600). Load them for this page only; don't change site-wide fonts.

### Leave out of the live page
- The black "Review mockup · not live" bar, the noindex meta, robots.txt. The live page must be indexable.
- The mockup's stand-in site header ("Church & Family Life / About / Network…" bar) and its bottom grey .foot line (review version + hero photo credit). Use the real site header/footer.
- Header/tab bar hide when the event subnav pins (same as the other /events pages).

### Build notes (from GTPR, apply here)
- Tailwind preflight zeroes p/h/list margins: scope the page's rules under a wrapper and restore margins with :where(#rtg) as GTPR does.
- Subnav (About, Schedule, Speakers, Location, Registration + "Register Now" button): click smooth-scrolls under the sticky bar and sets the address bar to #section with history.replaceState (no pushState; Back still leaves the page). Incoming #about/#schedule/#speakers/#location/#register links land after document.fonts.ready. Old #venue goes to #location. The mockup's script at the bottom of index.html does exactly this.
- Mobile 720px and below: the first screen shows title, subtitle, date and the Register Now button (as v9 at 390).
- No element wider than the viewport at any width, no console errors.

## Content (must match v9)
- Title: Replanting the Garden. Subtitle: Recovering Biblical Discipleship in Church and Family Life
- Dates: Friday–Saturday, July 16–17, 2027, Eastern. Fri 6:00 PM start, Sat ends 2:05 PM. The page shows no "Eastern" label (David removed it).
- Venue: Faith Community Church, 1998 Tallahassee Hwy, Bainbridge, GA 39819; church site https://www.fccbainbridge.com/ . Map embed https://maps.google.com/maps?q=1998%20Tallahassee%20Hwy%2C%20Bainbridge%2C%20GA%2039819&z=13&output=embed ; Get directions https://www.google.com/maps/dir/?api=1&destination=1998%20Tallahassee%20Hwy%2C%20Bainbridge%2C%20GA%2039819
- Speakers, in this order: Scott Brown (people 60ca3431e7346d3c2b733f3d), Justin Miller (people 67ab67c89682f4ec5681efb1). Bios exactly as v9. No sessions assigned to speakers.
- Schedule: 7 sessions exactly as v9. Friday: Session 1 6:00–6:35, Session 2 6:40–7:15, Q&A and Fellowship 7:15–8:30 PM. Saturday: Session 3 9:00–9:35, Session 4 9:40–10:15, Break 10:15–10:45, Session 5 10:45–11:20, Session 6 11:25–12:00, Lunch (Provided) 12:00–1:30 PM, Session 7 1:30–2:05 PM. No Session 8, no panel. Session 7 is "Answering Common Objections" (no "with Grace"). Each session keeps its one-line blurb.
- Lodging: one card, Holiday Inn Express & Suites Bainbridge by IHG, 1413 Tallahassee Hwy, (229) 246-6771, Book a Room (IHG bgega link), "Directions to the church →". Render it from the record's lodging field (v-html with :deep() styles) so more hotels can be added later as a data edit.
- Registration box: $15 per person, $45 per family, the three facts lines (dates; address; "Saturday lunch is provided"), Register Now, and the "Network pastors." row with the pre-filled mailto to adam@cf.life exactly as v9.
- Closing band: "Replanting the Garden" / dates / "Faith Community Church · Bainbridge, Georgia" / Register Now.

## Record fields
Ready to paste: handoff/event-record.json (title, shortName, status, scale, start/end UTC, address, speaker ids, description HTML, descriptionMin, schedule HTML in the QF format, lodging HTML, useNewCheckout true, bespokeTemplate true, relatedEvents [], the two rates). Keys starting with _ are notes, not fields. Geocode the address for coordinates.

## Images (upload to CFL S3; do NOT hot-link GitHub)
- Hero: handoff/img/hero-pecan-sapling.jpg (2000x1075, as used in v9; hero-pecan-sapling-3840.jpg is the full-size source). USDA photo, public domain; no credit line needed on the page. Alt "A young pecan tree in a Georgia orchard". object-position 100% 46% desktop, 88% 46% mobile, as v9.
- Church: handoff/img/faith-community-church.jpg (1001x865).
- Speakers: the people records' own images (cfl-mango) or handoff/img/scott-brown.jpg and justin-miller.jpg (the crops v9 uses).
- Event banner for the /events card and social share: handoff/RTG-banner-2400x1350.jpg as bannerImage.

## Registration / tickets
- Individual $15 per person (kind individual, times attendees; children $15 each unless on the family rate).
- Family $45 per family (kind family, flat however many attendees).
- New Stripe product + the two prices, linked as the event's stripeProduct. Current checkout (useNewCheckout: true) as GTPR. relatedEvents empty (guards the HAP-4284 $0 path).
- Every Register control (subnav Register Now, Registration section Register Now, closing band Register Now) opens THIS event's registration with the Individual/Family choice, as on GTPR.
- Status open (public, on /events) once the page and checkout pass. Keep it hidden while building.
- No real charges: check totals with expired/cancelled Stripe sessions as on HAP-5957, then delete the test registrations.

## Done when (post evidence on the issue)
1. https://churchandfamilylife.com/events/<id> and the slug URL render the v9 design at 1440 and 390: no review bar, no noindex, no sideways scroll, Newsreader + Libre Franklin loaded, all images from CFL S3.
2. All the copy above is present: 7 sessions with times and blurbs, both speakers in order, $15/$45, the hotel card, the network-pastor mailto (decodes to the v9 text), "Saturday lunch is provided".
3. Subnav clicks set #about…#register without growing history; incoming hashes land; #venue goes to #location.
4. Checkout totals: 1 individual = $15.00, 3 individuals = $45.00, 1 family (4 attendees) = $45.00; no $0 path. Post the Stripe product id, both price ids and the rate ids.
5. All 3 Register Now buttons open this event's registration.
6. The event is listed on /events (status open) with the banner card.
7. Post the event _id, live URL, Stripe ids and 1440 + 390 screenshots, then move to Review. Site verifies live and closes.

## Do not change
Other events, site-wide fonts, the GTPR / FWC / Quiet Faithful bespoke templates, header/footer for other pages. Leave the review repo alone (Site deletes it later).

## Open (David's call; do not block the build)
- Network-pastor discount code for this event: amount not decided yet. Keep the row; Adam answers the emails. Site will say if a coupon should be created.
- Hardship (free) code the host asked for: David's call; may come as a separate small request.
