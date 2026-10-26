# Functional Requirements Document: "Anywhere", date-led destination discovery

**Booking.com · MVP release · Web (desktop and mobile)**

| Field | Value |
|---|---|
| Document | FRD-ANYWHERE-001 |
| Version | 1.0 (draft for engineering review) |
| Date | 26 October 2026 |
| Status | Draft. Open questions in section 13 must be resolved before sprint planning. |
| Related documents | ["Anywhere" feature proposal](../../01-feature-proposal-booking-anywhere/proposal.md) (problem, personas, metrics) · Screens 1–3 (concept) · [Clickable prototype](../2-prototype/) · [Moodboard](../1-moodboard/brief.md) |
| Reviewers | Engineering lead (search), Engineering lead (front end), Design, Data/Analytics, QA, Legal (pricing display) |

> **Context:** this is a Product Management Academy exercise. Booking.com is used as the example product; system names, services and numbers are assumptions made for the exercise, not Booking.com internals.

**Contents:** [1 Purpose and scope](#1-purpose-and-scope) · [2 Glossary](#2-glossary) · [3 Assumptions](#3-assumptions-and-dependencies) · [4 User stories](#4-users-and-user-stories) · [5 Screen 1](#5-functional-requirements-screen-1-search-entry) · [6 Screen 2](#6-functional-requirements-screen-2-destination-results) · [7 Screen 3](#7-functional-requirements-screen-3-explore-stays) · [8 Business rules, data, interfaces](#8-business-rules-data-and-interfaces) · [9 UI rules](#9-ui-and-design-rules) · [10 NFRs](#10-non-functional-requirements) · [11 Analytics](#11-analytics-events) · [12 Experiment](#12-experiment-and-rollout) · [13 Open questions](#13-open-questions) · [14 Traceability](#14-traceability)

---

## 1. Purpose and scope

This document specifies the functional and non-functional requirements for the MVP of "Anywhere": a search mode that lets a traveller enter only travel dates and group size, see destinations with suitable available accommodation, and continue into the existing booking flow.

It is written so that engineering, design and QA can estimate, build and test the feature without a walkthrough. Requirements use "shall" for mandatory behaviour. Every requirement has an ID, a priority (Must / Should / Could) and at least one acceptance criterion.

### 1.1 In scope (MVP)
- "Anywhere" option in the destination field of the existing search box (Screen 1).
- A new Destination results page listing destinations with availability for the exact dates and group (Screen 2).
- A destination-level stays page (Screen 3), built on the existing property search results page, with a destination overview and Anywhere context.
- Hand-off to the existing property page and checkout, with source attribution.
- Feature flag, A/B experiment set-up and analytics events.
- Desktop web and mobile web (responsive).

### 1.2 Out of scope
- Flexible dates ("a weekend in October", "any 7 nights"). Fixed check-in and check-out only.
- Personalised ranking or recommendations.
- Saved collections, wish lists and sharing of destination lists.
- Flights, transport or total trip cost.
- Native iOS and Android apps (planned for phase 2 after the experiment).
- Changes to the property page, checkout, payments or confirmation flow.
- Any visual redesign of existing components (see section 9.1).

## 2. Glossary

| Term | Definition |
|---|---|
| Anywhere search | A search submitted with the destination value "Anywhere", fixed dates and occupancy. |
| Occupancy | Number of adults, number of children with ages, and number of rooms. |
| Candidate destination | A destination in the curated list that Anywhere can show (BR-01). |
| Qualifying offer | A room offer that is bookable now for the exact dates and fits the full occupancy (BR-02). |
| Available stay | A property with at least one qualifying offer. |
| Eligible destination | A candidate destination with at least the minimum number of available stays after filters (BR-03). |
| Destination card | One result row on Screen 2. |
| Destination page | Screen 3: stays in one destination, opened from Anywhere. |
| Source tag | The value `src=anywhere` carried from Screen 2 to booking, used for attribution. |
| Treatment / control | Users who see Anywhere (treatment) or the current experience (control) in the experiment. |

## 3. Assumptions and dependencies

| ID | Assumption or dependency | Impact if false |
|---|---|---|
| AS-01 | The availability and pricing service can return the cheapest qualifying offer per property for a list of destinations in one batch call. | A new aggregation job is needed; estimate grows. |
| AS-02 | Destination content (hero image, short description, theme tags, neighbourhoods) exists in the content system for every candidate destination, or the content team can create it before launch. | Launch with fewer candidate destinations or a fallback layout (FR-306). |
| AS-03 | The existing property search results page accepts a destination ID, occupancy, dates, filters and a source parameter, and can render an extra header block. | Screen 3 becomes a new page; estimate grows. |
| AS-04 | The experimentation platform supports user-level assignment for logged-in and logged-out users. | Experiment design must change. |
| AS-05 | The booking record can store an entry source (`entry_source`). | Attribution relies on analytics only. |
| AS-06 | Prices shown follow existing market rules for taxes and fees. | Legal review required per market. |

## 4. Users and user stories

Personas are described in the [feature proposal](../../01-feature-proposal-booking-anywhere/proposal.md#5-user-personas). Stories below are the ones the MVP must satisfy.

| ID | User story | Persona |
|---|---|---|
| US-01 | As a traveller who knows my dates but not my destination, I want to search without choosing a place, so that I can see where I could go. | Yuliya, Tomáš |
| US-02 | As a traveller with a budget, I want to see the price per night and the total for my stay for each destination, so that I only consider places I can afford. | Yuliya, Lucie |
| US-03 | As a family, I want to see only destinations and stays that fit all of us, so that I don't waste time on results that don't work. | Lucie |
| US-04 | As a traveller, I want to filter by budget, property type and key facilities, so that results match what matters to me. | Tomáš, Lucie |
| US-05 | As a traveller who doesn't know a destination, I want a short overview of it, so that I can judge if it suits me. | Tomáš, Maya |
| US-06 | As a traveller comparing places, I want to go back to the destination list without losing my filters, so that comparing is quick. | All |
| US-07 | As a traveller who has chosen a stay, I want to continue to the normal property page and booking, so that booking feels familiar and safe. | All |
| US-08 | As the product team, we want every Anywhere session and booking to be attributable, so that we can measure incremental bookings. | Internal |

## 5. Functional requirements: Screen 1 (search entry)

![Screen 1](../2-prototype/screenshots/screen-1-home-anywhere.jpg)
*Screen 1 (concept): "Anywhere" in the destination field.*

| ID | Requirement | Priority |
|---|---|---|
| FR-101 | When the destination field receives focus and is empty, the suggestion list shall show "Anywhere" as the first option, with the subtitle "Discover destinations that fit your dates" and a globe icon. | Must |
| FR-102 | When the user types, "Anywhere" shall remain in the list if the input matches "any", "anywhere" or "everywhere" (localised equivalents per language). Otherwise normal suggestions apply. | Should |
| FR-103 | Selecting "Anywhere" shall set the field value to "Anywhere" and move focus to the date picker if dates are empty. | Must |
| FR-104 | An Anywhere search shall require check-in date, check-out date, at least 1 adult and at least 1 room. Existing validation rules for dates, stay length and child ages shall apply unchanged. | Must |
| FR-105 | If the user submits without dates, the date picker shall open with the inline message "Add dates to see destinations with available stays". No request is sent. | Must |
| FR-106 | Submitting a valid Anywhere search shall navigate to the Destination results page (Screen 2) with all inputs in the URL (section 8.1). | Must |
| FR-107 | The homepage module "Trending destinations" shall show up to 5 eligible destinations for the current inputs, with name, country and "From €X/night". Clicking a card opens Screen 3 for that destination with the current inputs. | Could |
| FR-108 | For control users, or when the feature flag is off, the "Anywhere" option and module shall not appear. | Must |

| AC | Given / When / Then | Covers |
|---|---|---|
| AC-101 | Given a treatment user on the homepage, when they focus the empty destination field, then "Anywhere" is the first suggestion. | FR-101 |
| AC-102 | Given "Anywhere" is selected and dates are empty, when the user clicks Search, then the date picker opens with the inline message and no network request for results is sent. | FR-104, FR-105 |
| AC-103 | Given "Anywhere", 17–24 Oct, 2 adults, 1 room, when the user clicks Search, then Screen 2 loads and the URL contains `checkin=2026-10-17&checkout=2026-10-24&adults=2&rooms=1`. | FR-106 |
| AC-104 | Given a control user, when they focus the destination field, then "Anywhere" is not offered. | FR-108 |

## 6. Functional requirements: Screen 2 (destination results)

![Screen 2](../2-prototype/screenshots/screen-2-destination-results.jpg)
*Screen 2 (concept): destination results for 17–24 Oct, 2 adults.*

### 6.1 Results list

| ID | Requirement | Priority |
|---|---|---|
| FR-201 | The page shall show only eligible destinations (BR-03) for the exact dates and occupancy. | Must |
| FR-202 | The page header shall read "{n} destinations found" with the subtitle "Explore destinations with availability for your dates and guests." | Must |
| FR-203 | Each destination card shall show: hero image, destination name and country, description (max 160 characters, truncated with an ellipsis), up to 4 theme tags, the link "{n} stays available", up to 4 thumbnail images, average price per night, total price for the stay with "for {nights} nights", and the button "Explore stays". | Must |
| FR-204 | Prices shall be calculated as in BR-04 and shown in the user's selected currency, following existing market rules for taxes and fees. | Must |
| FR-205 | The count "{n} stays available" shall equal the number of available stays in that destination after the active filters are applied. | Must |
| FR-206 | Clicking the card image, title, "{n} stays available" or "Explore stays" shall open Screen 3 for that destination, carrying dates, occupancy, active filters and `src=anywhere`. | Must |
| FR-207 | Results shall load 20 destinations at a time. A "Show more destinations" button shall load the next 20 without losing scroll position. | Must |
| FR-208 | The default sort shall be "Best match" (BR-05). Other options: "Lowest price" (by average price per night, ascending) and "Most stays" (descending). | Must |
| FR-209 | A List / Map toggle should be offered. Map view shows one pin per eligible destination labelled with the average price per night. Clicking a pin opens a preview card with the same actions as FR-206. | Should |

### 6.2 Filters

| ID | Requirement | Priority |
|---|---|---|
| FR-210 | The filter panel shall contain: Budget per night (range slider, €0 to €1,200+ in the user's currency, steps of 10), Popular filters, Property type, Facilities. Options and labels reuse the existing filter definitions. | Must |
| FR-211 | A destination shall remain in results only if at least the minimum number of available stays (BR-03) pass all active filters (BR-06). | Must |
| FR-212 | Each filter option shall show a count of available stays across all eligible destinations that match it, given the other active filters. | Should |
| FR-213 | Changing a filter shall update the results without a full page reload and shall update the URL so that refresh, back and share restore the same state. | Must |
| FR-214 | "Clear all" shall remove all filters and restore the unfiltered results. | Must |
| FR-215 | On mobile web, filters shall open in a full-screen sheet with a "Show {n} destinations" button. | Must |

### 6.3 States

| ID | Requirement | Priority |
|---|---|---|
| FR-216 | While loading, the page shall show 3 skeleton cards and the filter panel in a disabled state. | Must |
| FR-217 | If no destination is eligible, the page shall show "No destinations match all your filters" with a "Clear all filters" button. If no filters are active, the message shall be "No destinations have availability for these dates and guests. Try other dates." with a button that opens the date picker. | Must |
| FR-218 | If the results service fails or exceeds the timeout (NFR-02), the page shall show "We couldn't load destinations right now" with a "Try again" button, and log an error event. | Must |
| FR-219 | If some destinations fail to load but others succeed, the page shall show the successful ones and not show an error. | Should |

| AC | Given / When / Then | Covers |
|---|---|---|
| AC-201 | Given dates 17–24 Oct and 2 adults, when Screen 2 loads, then every card shows a total price equal to the average price per night × 7 (±1 currency unit for rounding). | FR-203, BR-04 |
| AC-202 | Given 2 adults and 2 children, when Screen 2 loads, then no destination appears whose available stays cannot fit 4 guests in 1 room. | FR-201, BR-02 |
| AC-203 | Given results are shown, when the user sets the budget maximum to €80, then each remaining card's stay count only includes properties whose cheapest qualifying offer is ≤ €80 per night, and the URL contains the budget parameter. | FR-211, FR-213 |
| AC-204 | Given filters remove all destinations, when the list updates, then the empty state with "Clear all filters" is shown; clicking it restores the results. | FR-217, FR-214 |
| AC-205 | Given the user clicks "Explore stays" on Valencia, then Screen 3 opens with the same dates, occupancy and filters, and `src=anywhere` in the URL. | FR-206 |
| AC-206 | Given the user has scrolled to the 30th card, when they open Screen 3 and press "Back to all destinations", then Screen 2 shows the same filters and scroll position. | FR-207, FR-304 |

## 7. Functional requirements: Screen 3 (explore stays)

![Screen 3](../2-prototype/screenshots/screen-3-explore-stays.jpg)
*Screen 3 (concept). Numbers 1–6 map to the requirements below.*

Screen 3 is the existing property search results page for one destination, with three additions: the Anywhere context in the search bar, a destination overview block, and the "Back to all destinations" link.

| ID | Requirement | Priority |
|---|---|---|
| FR-301 | [1] The search bar shall show the destination name and country with a "via Anywhere" tag. Changing dates or occupancy shall reload Screen 3 for the same destination and keep the tag. | Must |
| FR-302 | [1] Selecting a different specific destination in the search bar shall open the standard search results for that destination without the tag and without `src=anywhere`. Selecting "Anywhere" shall return to Screen 2 with the current inputs. | Must |
| FR-303 | [2] A breadcrumb shall read "Home › Explore anywhere › Results › {Destination}". "Home" opens the homepage, "Explore anywhere" and "Results" open Screen 2 with current inputs and filters. The last item is not a link. | Must |
| FR-304 | [4] "Back to all destinations" shall return to Screen 2 restoring filters, sort and scroll position (browser history state). | Must |
| FR-305 | [3] The destination overview shall show: hero image, destination name and country, a description of 2–3 sentences (max 400 characters) including the main neighbourhoods, and up to 4 theme tags. | Must |
| FR-306 | [3] If description or hero image is missing for a destination, the overview shall show the name, country and tags only, without an empty image area. | Must |
| FR-307 | [5] Budget, property type and facility filters chosen on Screen 2 shall be pre-applied. A "Neighbourhood" filter shall list the destination's districts with counts. The mini-map shall open the existing map view. | Must |
| FR-308 | [6] The heading shall read "{Destination}: {shown} of {total} stays shown", where total is the number of available stays before Screen 3 filters. | Must |
| FR-309 | [6] Property cards shall reuse the existing property card component and show: photo, name, area and distance, review score and count, the cheapest qualifying room for the full occupancy, cancellation policy, total price for the stay with "{nights} nights, {occupancy}", price per night, and "See availability". | Must |
| FR-310 | [6] Only properties with a qualifying offer (BR-02) shall be listed. | Must |
| FR-311 | [6] "See availability" shall open the existing property page with dates, occupancy and `src=anywhere`. The source shall persist through checkout and be stored on the booking (`entry_source=anywhere`). | Must |
| FR-312 | If filters on Screen 3 leave no properties, the list shall show "No stays match all your filters" with one-tap removal of the last applied filter and a link "Back to all destinations". | Must |
| FR-313 | If availability changed since Screen 2 and the destination now has no available stays, Screen 3 shall show "Stays in {Destination} just sold out for these dates" and a link back to Screen 2. | Must |

| AC | Given / When / Then | Covers |
|---|---|---|
| AC-301 | Given Screen 3 for Valencia from Anywhere, when the page loads, then the search bar shows "Valencia, Spain" with "via Anywhere", the breadcrumb ends with "Valencia, Spain", and the overview is shown. | FR-301, FR-303, FR-305 |
| AC-302 | Given Screen 3, when the user changes guests from 2 to 4 adults, then the page reloads for Valencia, the tag stays, and every listed property fits 4 adults in the selected rooms. | FR-301, FR-310 |
| AC-303 | Given Screen 3, when the user types and selects "Lisbon" in the destination field, then the standard Lisbon results open without the tag and without `src=anywhere`. | FR-302 |
| AC-304 | Given a destination without a description, when Screen 3 loads, then the overview shows name, country and tags and no empty image placeholder. | FR-306 |
| AC-305 | Given the user books a property after clicking "See availability" on Screen 3, then the booking record has `entry_source=anywhere` and the `booking_completed` event carries `src=anywhere`. | FR-311, AN-08 |
| AC-306 | Given filters leave no properties, then the empty state is shown with a one-tap removal of the last filter. | FR-312 |

## 8. Business rules, data and interfaces

### 8.0 Business rules

| ID | Rule |
|---|---|
| BR-01 | **Candidate destinations.** A curated list of cities and regions maintained by the content team (initially about 350, matching the "345 destinations found" example). Each has a destination ID, name, country, coordinates, content (BR-07) and a popularity score. The list is configurable without a release. |
| BR-02 | **Qualifying offer.** A room offer is qualifying if it is bookable now for the exact check-in and check-out dates and the selected rooms can accommodate all adults and children (using existing occupancy and child-age rules). |
| BR-03 | **Eligible destination.** A candidate destination with at least `min_stays` available stays after filters. Default `min_stays = 3` (configurable) so that users don't open destinations with almost no choice. |
| BR-04 | **Destination price.** For each available stay, take the cheapest qualifying offer's total stay price for the full occupancy, including taxes and fees as required by the market. Total = arithmetic mean of these values across the destination's available stays after filters. Average per night = Total ÷ number of nights. Both are rounded to the nearest whole currency unit for display. |
| BR-05 | **Best match ranking.** `score = 0.4 × availability + 0.3 × affordability + 0.3 × popularity`, where availability = available stays ÷ max available stays among eligible destinations; affordability = 1 − (avg price per night ÷ max avg price per night); popularity = destination popularity score (0–1) for the travel month. Weights are configurable. Ties: higher availability first. No user-level personalisation. |
| BR-06 | **Budget filter.** A stay passes if its cheapest qualifying offer, per night, is between the selected minimum and maximum. "€1,200+" means no upper limit. |
| BR-07 | **Destination content.** Hero image (min 1200×800 px), up to 4 thumbnails, description (max 160 characters for Screen 2, max 400 for Screen 3), up to 4 theme tags from a fixed list (Beaches, Culture, Great food, Nature, Relaxation, Nightlife, Outdoors, History, Mild weather), neighbourhood list. All text is localised. |
| BR-08 | **Attribution.** `src=anywhere` is added on Screen 2 → 3 navigation and kept until booking or until the user starts a non-Anywhere search. The booking stores `entry_source=anywhere`. |

### 8.1 URL schema

```
Screen 2: /anywhere?checkin=2026-10-17&checkout=2026-10-24&adults=2&children=2&ages=6,9
          &rooms=1&budget_min=0&budget_max=150&types=apartment,hotel&fac=pool&sort=best
Screen 3: /searchresults?dest_id={id}&checkin=...&checkout=...&adults=...&rooms=...
          &budget_max=150&types=apartment&src=anywhere
```

### 8.2 Destination results API (new)

`GET /api/anywhere/destinations`. Request parameters as in the Screen 2 URL plus `currency`, `locale`, `offset`, `limit` (default 20).

```json
{
  "total_destinations": 345,
  "nights": 7,
  "currency": "EUR",
  "destinations": [
    {
      "dest_id": "valencia-es",
      "name": "Valencia", "country": "Spain",
      "description_short": "Sunny beaches, historic old town ...",
      "tags": ["beaches", "culture", "great_food", "mild_weather"],
      "hero_image_url": "...", "thumbnail_urls": ["...", "...", "...", "..."],
      "available_stays": 128,
      "avg_price_per_night": 92, "avg_total_price": 644,
      "rank_score": 0.81,
      "lat": 39.47, "lng": -0.38
    }
  ],
  "facets": { "property_type": {"hotel": 982, "...": 0}, "facility": {} },
  "partial": false
}
```

Screen 3 uses the existing property search API with `dest_id` and `src`. The destination overview block uses a new content call `GET /api/destinations/{dest_id}/overview?locale=` returning name, country, description_long, tags, hero_image_url and neighbourhoods.

### 8.3 Computation and caching
- Results are computed by fanning out availability requests for the candidate set (BR-01) and aggregating per destination (BR-04).
- Aggregates shall be cached per key (check-in, check-out, occupancy, currency) for 15 minutes. Filters are applied on the cached per-property data, not by new availability calls.
- Prices on Screen 2 and Screen 3 are indicative. The property page always shows the live price; this matches existing behaviour.

## 9. UI and design rules

### 9.1 Design approach
The MVP evolves the existing design system; it is not a redesign. A redesign would change two variables at once and make the experiment impossible to read.

| Element | Rule |
|---|---|
| Reuse as-is | Header, search box, date picker, occupancy picker, filter panel, checkboxes, range slider, sort dropdown, map view, property card, buttons, breadcrumb, review score badge. |
| New components | Destination card (Screen 2), destination overview block (Screen 3), "via Anywhere" tag, "Anywhere" suggestion row. Built only from existing design tokens (colour, type, spacing, radius, elevation). |
| Copy | Sentence case, short, existing tone of voice. All strings in the translation system; no hard-coded text. |
| Imagery | Destination photos from the content library: bright, real places, no text on images, 3:2 ratio for heroes. |
| Reference | See the [moodboard](../1-moodboard/brief.md). |

### 9.2 Responsive behaviour
- ≥ 1024 px: two columns (filters left, results right) as in Screens 2 and 3.
- < 1024 px: single column; filters in a full-screen sheet; destination card stacks image above text and price.
- Screen 3 overview stacks image above text below 768 px.

## 10. Non-functional requirements

| ID | Requirement |
|---|---|
| NFR-01 | **Performance.** Screen 2 first 20 results: p95 ≤ 2.5 s server response on a cold cache, ≤ 600 ms on a warm cache. Largest Contentful Paint ≤ 2.5 s at p75 on mobile. |
| NFR-02 | **Timeout.** The results API times out at 6 s and returns partial results if at least 10 destinations are ready (`partial: true`). |
| NFR-03 | **Resilience.** A kill switch (feature flag) hides the Anywhere option within 5 minutes without a deploy. Failure of the Anywhere service never affects standard search. |
| NFR-04 | **Scalability.** Support peak traffic of the treatment group at 50% allocation without raising availability-service error rate above its current SLO. |
| NFR-05 | **Accessibility.** WCAG 2.2 AA: suggestion list and slider are keyboard and screen-reader operable; images have alt text (destination name); colour contrast ≥ 4.5:1 for text; focus is visible; result count changes are announced. |
| NFR-06 | **Localisation.** All supported languages and currencies at launch in the experiment markets; destination names and descriptions localised; dates and numbers in locale format. |
| NFR-07 | **Privacy.** No new personal data is collected. Analytics events follow existing consent rules (GDPR); no event is sent before consent where consent is required. |
| NFR-08 | **SEO.** `/anywhere` result pages are noindex (parameterised, user-specific). |
| NFR-09 | **Browser support.** Same as the current website. |
| NFR-10 | **Monitoring.** Dashboards and alerts for API latency, error rate, partial-result rate and cache hit rate. |

## 11. Analytics events

Every event carries: `user_id` (or device ID), `session_id`, `experiment_variant`, `platform`, `locale`, `currency`, `timestamp`.

| ID | Event | Trigger | Extra properties |
|---|---|---|---|
| AN-01 | `anywhere_option_shown` | Suggestion list with "Anywhere" is shown | – |
| AN-02 | `anywhere_selected` | User selects "Anywhere" | – |
| AN-03 | `anywhere_search_submitted` | Valid Anywhere search submitted | checkin, checkout, nights, adults, children, rooms |
| AN-04 | `destination_results_viewed` | Screen 2 rendered | total_destinations, partial, load_ms |
| AN-05 | `destination_filter_changed` | Any filter or sort change on Screen 2 | filter_name, value, results_count |
| AN-06 | `explore_stays_clicked` | Navigation from Screen 2 to Screen 3 | dest_id, position, avg_price_per_night, available_stays |
| AN-07 | `property_opened` | "See availability" clicked on Screen 3 | dest_id, property_id, position, total_price, src |
| AN-08 | `booking_completed` | Existing event | add src / entry_source |
| AN-09 | `booking_cancelled` | Existing event | add src / entry_source |
| AN-10 | `anywhere_error` | Error or empty state shown | type (error, empty_filters, empty_dates, sold_out) |

These events feed the metrics in the proposal: incremental bookings (AN-08 by variant), adoption rate (AN-03 users ÷ all searchers), discovery engagement (AN-06 ÷ AN-04), return frequency (distinct days with AN-03 per user in 30 days).

## 12. Experiment and rollout

| Item | Specification |
|---|---|
| Feature flag | `anywhere_search_mvp` (on/off, allocation %, market list, kill switch). |
| Design | A/B test, user-level randomisation, 50/50 treatment vs control after ramp-up. |
| Eligible users | Desktop and mobile web visitors in the experiment markets who view the homepage search box. |
| Ramp-up | 1% for 2 days (technical check) → 10% for 3 days → 50%. Each step needs no alerts on NFR-01 to NFR-04. |
| Duration | At least 4 full weeks, and until the pre-calculated sample size for the North Star is reached. |
| Primary metric | Completed (not cancelled) bookings per eligible user, treatment vs control. |
| Guardrails | Conversion of standard destination searches; cancellation rate; standard search latency. |
| Stop rules | Stop early if a guardrail drops significantly (as defined by the data team) or NFR-03 is triggered. |

## 13. Open questions

| ID | Question | Owner | Needed by |
|---|---|---|---|
| OQ-01 | Should "Anywhere" be pre-selected in the destination field for treatment users (as in the concept screen), or only offered as the first suggestion? Pre-selection may raise adoption but risks the standard-search guardrail. Proposal: test as a second treatment variant later. | Product | Sprint planning |
| OQ-02 | Mean vs median for destination price (BR-04). The median is less sensitive to luxury outliers but the label must then change from "avg.". | Product + Data | Design freeze |
| OQ-03 | How does Anywhere relate to the existing AI Trip Planner in the app (destination inspiration via chat)? Shared destination content? Cross-links? | Product leads | Before phase 2 |
| OQ-04 | Final list and number of candidate destinations per market (BR-01) and content readiness (AS-02). | Content | Sprint 1 |
| OQ-05 | Can the availability service handle the fan-out for ~350 destinations at 50% allocation, or do we need nightly pre-computation for popular date ranges? | Search engineering | Sprint planning |
| OQ-06 | Which markets run the experiment first? | Product + Data | Sprint planning |

## 14. Traceability

| User story | Requirements | Acceptance criteria | Metric |
|---|---|---|---|
| US-01 | FR-101–106 | AC-101–103 | Adoption rate |
| US-02 | FR-203, FR-204, FR-309, BR-04 | AC-201 | Discovery engagement |
| US-03 | FR-201, FR-310, BR-02 | AC-202, AC-302 | Conversion (family segment) |
| US-04 | FR-210–215, FR-307, BR-06 | AC-203, AC-204 | Discovery engagement |
| US-05 | FR-305, FR-306 | AC-301, AC-304 | Explore stays → property open rate |
| US-06 | FR-207, FR-303, FR-304 | AC-206 | Destinations explored per session |
| US-07 | FR-311 | AC-305 | Search-to-booking conversion |
| US-08 | FR-311, BR-08, AN-01–10 | AC-305 | Incremental bookings (North Star) |
