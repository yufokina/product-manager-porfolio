# 02 · Booking.com "Anywhere": design, prototype & functional requirements

**STRV Product Academy · Homework 2 · Design: Strategy, AI Prototyping & Bulletproof Specs**

Builds on [01 · Feature proposal](../01-feature-proposal-booking-anywhere/): a travel search that starts with *when* and *who* and helps people discover *where*.

| Deliverable | Where |
|---|---|
| 1. Moodboards (3) + design brief | [1-moodboard/brief.md](1-moodboard/brief.md) |
| 2. Clickable prototype of 3 flows, built with AI | [2-prototype/](2-prototype/) · **[▶ Open the prototype](https://yufokina.github.io/product-manager-porfolio/02-design-prototype-booking-anywhere/2-prototype/)** |
| 3. Functional requirements doc (FRD v1.1) | [3-requirements/frd.md](3-requirements/frd.md) · [PDF](3-requirements/frd.pdf) |
| AI first draft vs. my edits | [3-requirements/edits-log.md](3-requirements/edits-log.md) · [line-by-line diff](ADD-COMMIT-LINK) |

---

## The 3 flows

| 1. Search "Anywhere" | 2. Pick a destination | 3. Explore stays → book |
|---|---|---|
| ![Screen 1](2-prototype/screenshots/screen-1-home-anywhere.jpg) | ![Screen 2](2-prototype/screenshots/screen-2-destination-results.jpg) | ![Screen 3](2-prototype/screenshots/screen-3-explore-stays.jpg) |

## FRD highlights

- **Written so engineering can start without a walkthrough:** every requirement has an ID, a priority (Must / Should / Could) and Given/When/Then acceptance criteria.
- **Precise business rules:** what counts as a "qualifying offer" and an "eligible destination", how the destination price is calculated, the ranking formula (availability × affordability × popularity, with configurable weights), and how destination summaries and tags are computed from existing data.
- **Covers every state:** loading, empty results, empty after filters, partial failure, timeout, and "just sold out".
- **Measurable from day one:** 10 analytics events mapped to the North Star, plus A/B design, ramp-up plan, guardrails and stop rules.
- **Traceability:** user story → requirements → acceptance criteria → metric.

## Key decisions & trade-offs

- **Evolve the design system, don't redesign it.** A redesign would change two variables at once and make the experiment impossible to read.
- **Fixed dates only in the MVP.** Flexible dates were the first cut in the budget scenario. They add a lot of search cost before we know whether the core idea works.
- **Screen 3 reuses the existing search results page** with three additions (the "via Anywhere" tag, a destination overview, a "back to all destinations" link), instead of being a new page. Its filter panel is Booking.com's standard one, unchanged: users find the filters they know, and nothing extra has to be built or tested.
- **Destination information comes only from existing data.** Booking.com has no written content about cities today, and writing it for ~350 destinations in every language would cost more than the interface. So the overview shows a factual summary (what guests mention in reviews, most booked areas, guest rating) and rule-based tags (e.g. Beaches, Culture, Family-friendly). Tags are for display only, since Booking.com has no theme filters.
- **Cut what the data can't support.** A neighbourhood filter, a "popular nearby" list and a "mild weather" tag were removed: they added cost or needed data Booking.com doesn't have, without helping the core decision.
- **Prices are indicative until the property page**, which matches existing behaviour and avoids a new pricing commitment.

## What I learned

- [add 2–3 points: e.g. what the AI did well, where it was wrong or vague, what you'd prompt differently next time]
