# Booking.com feature proposal: "Anywhere", date-led destination discovery

Let travellers start with **when** and **who**, and help them discover **where**, so Booking.com captures people who know their dates but have not chosen a destination.

**Contents:** [1 Business overview](#1-business-overview) · [2 Vision](#2-vision) · [3 Competitive landscape](#3-competitive-landscape) · [4 User interviews](#4-user-interviews) · [5 Personas](#5-user-personas) · [6 Problem statement](#6-problem-statement) · [7 User journey](#7-user-journey-three-screens) · [8 MVP scope](#8-mvp-scope) · [9 Success metrics](#9-success-metrics) · [10 Budget cut](#10-budget-cut-scenario)

---

## 1. Business overview

Booking.com's core experience is built around travellers choosing a destination, travel dates and the number of guests before they browse properties.

The proposed feature, **"Anywhere"**, lets travellers enter only their dates and group size and then discover destinations that fit. The longer-term ambition is to evolve from a destination-based booking platform into a place-discovery and trip-inspiration platform.

| Area | Project context (hypothetical) |
|---|---|
| Core business | Accommodation search and bookings |
| Primary users | Travellers planning trips, including those who are flexible about the destination |
| Existing journey | Destination > dates > guests > accommodation results |
| Opportunity | **Capture travellers who know when they want to travel, but not where** |
| Budget | To be determined; investment must be justified by evidence |
| Timeline | MVP experiment before committing to the broader vision |

**What Booking.com has today**
- A destination-first accommodation search.
- Search inputs for destination, travel dates and number of guests.
- Property listings, filters, property pages and a booking flow.
- A large accommodation marketplace (about 4.4 million properties in 220+ countries and territories) that can support discovery across destinations.

## 2. Vision

Help travellers discover destinations they might never have considered, even when they have no specific place in mind.

**Short term:** the user selects "Anywhere", enters dates and number of travellers, and explores destinations where suitable accommodation is available.

**Why now:** in Expedia Group research, 59% of travellers had no specific destination in mind, or were weighing several options, when they started planning [Expedia Group & Luth Research, *The Path to Purchase*, 2023]. Today, Booking.com's search does not serve that moment.

## 3. Competitive landscape

*Illustrative: the comparison describes broad product positioning, not a verified feature audit.*

| Player | What they offer | Gap / opportunity for Booking.com |
|---|---|---|
| Google Travel | Travel search and destination exploration | Connect inspiration directly to Booking.com's accommodation inventory and booking flow |
| Airbnb | Accommodation discovery, including distinctive stays and destination inspiration | Explore destinations across a much broader accommodation marketplace (hotels and homes) |
| Pinterest | Visual inspiration and saved collections | Turn inspiration into bookable accommodation instead of leaving users to organise the booking themselves |
| Booking.com today | Destination-led accommodation search | Serve travellers who are flexible about where they go |

## 4. User interviews

*The four interviews below are fictional examples created to illustrate potential user needs.*

| Interviewee | What they said | Key insight |
|---|---|---|
| Yuliya, 29, working professional, flexible weekends | "I know I want to go somewhere for three nights in October, but I have no idea where. I usually open Google Maps, browse places, check prices on different sites, and eventually give up because it takes too long." | Dates are fixed; the effort of comparing places makes her give up: lost demand. |
| Tomáš, 34, travels with his partner | "We don't care that much about the destination. We want somewhere affordable, with nice restaurants and maybe a pool. If Booking.com showed us places that fit our dates and budget, we'd definitely explore them." | Chooses by budget and vibe (food, pool), not by place name. |
| Maya, 26, solo traveller, blogger | "I like discovering places that look nice on pictures and I can work on my video blog there. Pretty pictures are enough for me." | Visuals drive exploration, but may not lead to a booking. |
| Lucie, 38, parent of two | "We often have school holidays booked before we've decided where to go. I want to see which places have accommodation for four people within our budget. I don't want to search twenty destinations one by one." | Needs availability for a specific group size across many destinations at once. |

**Patterns across the interviews**
- **Dates come first.** Three of four interviewees know when they travel before they know where.
- **Budget is a hard filter.** Yuliya, Tomáš and Lucie all frame the choice around price.
- **Repeating searches is the main pain.** Comparing destinations one by one leads to fatigue and drop-off.

## 5. User personas

The interviews point to three primary personas, the core target of the MVP, and one secondary persona we need to watch so that browsing is not mistaken for success.

### Yuliya · PRIMARY · The budget and dates explorer
*29, working professional, travels on flexible long weekends*

| | |
|---|---|
| Trigger | A free long weekend appears in her calendar; dates are fixed, the place is not. |
| Goals | Get away for 2–3 nights without spending an evening on research · Stay within a clear budget · Feel confident the place is worth it |
| Pain points | Jumps between Google Maps and several booking sites · Has to check prices destination by destination · Planning fatigue > she abandons the trip |
| Today's workaround | Maps + price comparison across tabs; often ends with no booking at all. |
| What she needs from Anywhere | Dates + budget > a short list of destinations with real availability and a total price she can trust. |
| MVP features that serve her | Anywhere option, fixed dates, price visibility (per night and total), budget filter, direct booking |
| Expected usage | 3–4 short trips a year; several sessions per trip in the 1–3 weeks before booking. |
| Success for her | Goes from "I have a free weekend" to a confirmed booking in one session. |

### Tomáš · PRIMARY · The flexible couple
*34, travels with his partner, values atmosphere over a specific place*

| | |
|---|---|
| Trigger | He and his partner agree on dates for a holiday and a rough budget. |
| Goals | Affordable stay with a pool · A destination with good food and a pleasant vibe · Something they both agree on quickly |
| Pain points | Search starts with "where?", which they have not decided · Hard to compare destinations by the things they care about (food, pool) |
| Today's workaround | Browses friends' recommendations and searches a few familiar cities one by one. |
| What he needs from Anywhere | Destinations matched to dates and budget, plus a quick sense of what each place is like. |
| MVP features that serve him | Anywhere option, price visibility, destination tags (e.g. Great food), "Swimming pool" filter, destination overview |
| Expected usage | 1–2 holidays and a few weekend breaks a year; returns 2–3 times while the couple decides. |
| Success for him | Shortlists 2–3 destinations, shares them with his partner and books one. |

### Lucie · PRIMARY · The flexible family
*38, parent of two, dates fixed by school holidays*

| | |
|---|---|
| Trigger | School holiday dates are announced; dates and budget are fixed, destination is open. |
| Goals | Accommodation that really fits 4 people (2 adults + 2 children) · Stay within the family budget · Book early, before family-friendly options sell out |
| Pain points | Searching 20 destinations one by one · Peak-season availability disappears fast |
| Today's workaround | Repeats the same search across many destinations and keeps notes. |
| What she needs from Anywhere | Only destinations with available family-sized accommodation for her exact dates, with the total price. |
| MVP features that serve her | Number of travellers and rooms, real availability across destinations, total price for the stay, property type filter (apartments, holiday homes) |
| Expected usage | 2–3 trips a year, but intense planning: 4+ sessions in the weeks before each school holiday. |
| Success for her | Finds a suitable family stay without running separate searches, and books before peak sell-out. |

### Maya · SECONDARY · The visual wanderer (watch-out persona)
*26, solo traveller, video blogger*

| | |
|---|---|
| Trigger | Looking for content-worthy, photogenic places to visit and film. |
| Goals | Discover beautiful, less obvious places · Find a stay where she can also work (WiFi) |
| Pain points | Inspiration lives on social media, separate from booking |
| Why she matters | She shows that strong imagery drives exploration. |
| MVP features that serve her | Destination photos and overview, "Free WiFi" facility filter |
| Expected usage | Frequent browsing visits, few bookings. |
| How we treat her | Not a primary target for the MVP. We track her behaviour so that high engagement without bookings is not mistaken for success. |

## 6. Problem statement

Travellers who know when they want to travel but are flexible about where are underserved by Booking.com's destination-first search: they must pick a destination before they can explore options. As a result, some potential customers abandon their search, or never discover destinations that fit their dates, group size and budget.

Helping these travellers move from uncertainty to a bookable destination could unlock incremental bookings and lay the foundation for Booking.com's longer-term ambition to become a place-discovery platform.

## 7. User journey: three screens

The MVP adds one entry point and one new results type, then hands the user over to the existing booking flow.

1. **Home: choose "Anywhere".** The user leaves the destination as "Anywhere", enters dates and guests, and taps Search.
2. **Results: destinations that fit.** A ranked list of destinations with availability for those dates and guests, each showing price per night, total price and the number of available stays.
3. **Explore stays: one destination in detail.** After "Explore stays", the user sees an overview of the destination and the available properties there, then continues to the existing property page and checkout.

### Screen 1: Home with "Anywhere"
![Screen 1](images/screen-1-home-anywhere.jpg)
*"Anywhere" is selected in the destination field; dates and guests are the only required inputs.*

### Screen 2: Destination results
![Screen 2](images/screen-2-destination-results.jpg)
*Destinations with availability for Oct 17–24, 2 adults; each card leads to "Explore stays".*

### Screen 3: Explore stays (destination detail)
**Purpose:** the moment of decision. The user has picked a destination they may not know, so this screen must answer two questions fast: "Is this place right for me?" and "What can I actually book here?" It then hands the user to the existing booking flow without friction.

**Entry point:** "Explore stays" or the "X stays available" link on a destination card in Screen 2. All search inputs (dates, guests, rooms) and filters chosen on Screen 2 are carried over.

![Screen 3](images/screen-3-explore-stays.jpg)
*Concept: Valencia, Oct 17–24, 2 adults, "Free cancellation" filter on. Numbers match the elements in the table below.*

| # | Element | What it does | Why (persona / hypothesis) |
|---|---|---|---|
| 1 | Search bar with "via Anywhere" tag | Shows the chosen destination while remembering the user came from Anywhere. Changing dates or guests updates this page. | Keeps context; lets us attribute bookings to the feature. |
| 2 | Breadcrumb | Home > Explore anywhere > Results > Valencia. | Clear way back; users compare several destinations. |
| 3 | Destination overview | Hero photo, 2–3 sentence description, a quick neighbourhood guide and theme tags (Beaches, Culture, Great food). | Helps users judge an unfamiliar place (Tomáš, Maya) |
| 4 | "Back to all destinations" | Returns to Screen 2 with scroll position and filters preserved. | Comparing destinations should not mean starting again. |
| 5 | Filters | Budget and filters from Screen 2 are kept; a destination-specific "Neighbourhood" filter is added; mini-map opens the map view. | Essential filters only. |
| 6 | Property cards | Photo, name, area and distance, review score, room that fits the group, free cancellation, total price for the whole stay, "See availability". | Leads to the existing property page and checkout. The total price matters most to Lucie and Yuliya. |

## 8. MVP scope

**Product principle:** validate whether date-led destination discovery generates incremental bookings before building a broader inspiration platform.

### Must-haves
1. **"Anywhere" search option.** The core of the feature: it tests whether people want to discover places without choosing a destination first.
2. **Travel date selection.** Dates are the starting point; results must reflect when travellers can go.
3. **Number of travellers and rooms.** Suggestions must suit the group (essential for families like Lucie's).
4. **Available accommodation across destinations.** Discovery must lead to real, bookable options, not an inspirational list with nothing available.
5. **Price visibility.** Per-night and total prices let users judge whether a destination is affordable.
6. **Basic destination information.** Location and a short overview help users assess places they have not considered before.
7. **Essential filters.** A small set (budget, property type, a few popular facilities) supports preference-based exploration without a complex recommendation engine.
8. **Direct booking flow.** Users go from a discovered destination to property details and checkout; without this the feature cannot prove commercial value.
9. **Experimentation and analytics.** Track adoption, return visits, discovery, conversion and cancellations against existing search before scaling.

### Explicit cuts
- **Saved collections and folders:** part of the long-term vision, but not needed to discover and book a destination.
- **Personalised recommendations:** first validate whether users value destinations ranked by dates, guests, budget and availability.
- **Transport and total trip cost:** the MVP covers accommodation only; no flights or local transport.

## 9. Success metrics

| Level | Metric | Definition | Why |
|---|---|---|---|
| ⭐ North Star | Incremental completed bookings | Completed (not cancelled) bookings per eligible search session in the test group minus the control group. | Shows value beyond existing search. |
| Supporting | Search-to-booking conversion | % of Anywhere sessions that end in a completed booking. | Shows discovery turns into bookings. |
| Supporting | Destination discovery engagement | % of Anywhere sessions where the user opens "Explore stays" or a property. | Shows the results are relevant. |
| Adoption | Feature reach | See 9.1 | How many users use the feature? |
| Retention | Return frequency | See 9.2 | How often each user comes back. |

### 9.1 How many users use the feature (adoption)
- **Adoption rate** = unique users who run at least one Anywhere search / unique users who run any accommodation search (same period, test group).
- **Weekly and monthly active Anywhere users (WAU / MAU):** the absolute number of unique users who use Anywhere.
- **Share of searches** = Anywhere searches / all searches. Shows how central the feature becomes.
- **Segment split:** adoption by device, by solo/couple/family group size (proxy for personas), and new vs. returning Booking.com customers.

*Illustrative funnel for the experiment (assumptions to validate, not Booking.com data):*

| Funnel step | Assumed rate | Users (per 1,000,000 searchers in test group, 4 weeks) |
|---|---|---|
| Searchers who see the Anywhere option | 100% | 1,000,000 |
| Select Anywhere and search (adoption) | 6% | 60,000 |
| Open "Explore stays" for a destination (Screen 3) | 45% | 27,000 |
| Open a property page | 60% | 16,200 |
| Complete a booking | 3% of Anywhere users | 1,800 |

**Why 6%?** About 59% of travellers start planning undecided (Expedia Group), but most people who reach Booking.com have already chosen a place, so only a small share of searchers is expected to need Anywhere. The experiment will replace these assumptions with real numbers.

### 9.2 How many times a person comes back (return frequency)
Travel is a low-frequency purchase, so "coming back" is measured on two time scales:

| Metric | Definition | Illustrative target |
|---|---|---|
| Sessions per user (planning cycle) | Average number of separate days a user uses Anywhere within 30 days of their first use. | ≥ 2.0 |
| 7-day return rate | % of Anywhere users who use it again within 7 days of first use. | ≥ 30% |
| Return distribution | Share of users who used Anywhere 1 time, 2–3 times, 4+ times in 30 days. | Growing "2–3" group |
| Repeat use for the next trip | % of Anywhere bookers who start their next search with Anywhere within 6 months. | ≥ 20% (measured after MVP) |

## 10. Budget cut scenario

**Scenario:** the board halves the budget, but the Series A timeline stays the same.

- **Cut:** flexible-date search within Anywhere. Users must choose fixed check-in and check-out dates; Anywhere searches across destinations for those exact dates.
- **Simplify:** use a straightforward destination ranking (availability, price, popularity) rather than building a recommendation engine.
- **Protect:** the Anywhere entry point, date and traveller inputs, real availability, the existing booking flow and reliable experiment tracking (including adoption and return metrics). Removing these would undermine the core hypothesis or make its impact impossible to measure.

**What I would tell the leadership team:**

> "We can cut the breadth of the experience, but not our ability to learn. We give up the richer discovery platform in the short term to find out whether date-led search produces incremental, quality bookings. If the evidence is positive, we have a credible case for further investment. If it isn't, we avoid spending the remaining budget on features that haven't proved their value."
