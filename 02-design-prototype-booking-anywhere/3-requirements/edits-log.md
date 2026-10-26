# FRD: AI first draft vs. my edits

**AI tool used:** Claude (Anthropic)
**Prompt:** [paste or summarise the prompt]

**See every change line by line:** [commit diff](ADD-COMMIT-LINK)

## What I changed and why

| # | What the AI draft had | What I changed | Why |
|---|---|---|---|
| 1 | Destination overview with a written description ("Sunny beaches, a historic old town…"), assuming a content team would write it (BR-07, AS-02) | Summary built only from existing data: what guests mention in reviews, most booked areas, guest rating, plus rule-based tags (BR-07, BR-08, section 8.4) | Booking.com has no written content about cities today. Writing it for ~350 destinations in every language is a hidden cost bigger than the UI, and AI-written text risks invented claims |
| 2 | A new "Neighbourhood" filter on Screen 3 (FR-307) | Screen 3 uses Booking.com's standard filter panel, unchanged | A custom panel costs more to build and test, users expect the filters they know, and it would add a second change to the experiment |
| 3 | A "Popular nearby" line in the destination overview | Removed | Not needed to decide on a destination; one less data dependency |
| 4 | A "Mild weather" theme tag | Removed (replaced by "Family-friendly", based on family rooms) | Booking.com has no weather data of its own; every tag must come from existing data |
| 5 | A "What are you in the mood for?" theme filter in the prototype | Removed; theme tags are for display only | Booking.com has no theme filters today. A new filter is extra scope the MVP doesn't need to test the core hypothesis |
| 6 | Screen 3 concept with "Why it fits your trip" and "Similar for your dates" blocks | Removed from the MVP, moved to the future-vision moodboard | Keep the MVP focused on the core hypothesis; both are closer to personalisation, which was cut |

## What I learned

- [e.g. AI is fast at structure and coverage but invents system details. I marked those as assumptions (section 3)]
- [ ]
