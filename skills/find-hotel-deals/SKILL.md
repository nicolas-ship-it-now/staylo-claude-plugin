---
name: find-hotel-deals
description: Find and compare hotels with Staylo when the user wants a place to stay — a city, dates, a budget, free cancellation, breakfast or a minimum rating. Uses the Staylo tools to show live net rates next to the public price, then hands off to the Staylo website to book.
---

# Find hotel deals with Staylo

Use this skill when the user is looking for a hotel or any place to stay: "a hotel in Rome next weekend", "somewhere refundable near the Eiffel Tower under €200", "a family room in Lisbon in July".

## 1. Get the essentials

You need a destination and dates before searching.

- **Destination**: a city, neighbourhood, landmark or hotel name. Pass it as the user said it.
- **Dates**: check-in and check-out as `YYYY-MM-DD`. Resolve relative dates ("next weekend", "tomorrow") from today's date. If the user gives a number of nights, compute the check-out.
- **Guests**: default to 2 adults and 1 room. Ask only if the user hinted at something else (children, a group, several rooms). Children need their ages.

Ask one short question if the destination or the dates are missing; otherwise search right away.

## 2. Pass every requirement as a parameter

The server filters on the rate it displays, so a requirement only counts if it is sent:

| The user says | Parameter |
|---|---|
| "refundable", "free cancellation", "flexible" | `freeCancellation: true` |
| "with breakfast", "half board", "all inclusive" | `mealPlan: "breakfast"`, `"half_board"`, `"full_board"`, `"all_inclusive"` |
| "under €150", "max 200 a night" | `maxPricePerNight: 150` |
| "well rated", "8 or more" | `minRating: 8` |
| "4 or 5 stars" | `stars: [4, 5]` |

Also send `language` (the language of the conversation) and `currency` (the user's currency if known, otherwise EUR), so the booking site opens the right way.

Use the same `freeCancellation` and `mealPlan` values when you call `get_hotel` for a hotel from the results.

## 3. Present the results

- The results appear as cards in the conversation. Add a short summary: the cheapest option, the best-rated one, and how much the user saves against the public price.
- The **public price** is the hotel's suggested retail rate; the **saving** is the difference with the Staylo price. Describe it that way, without naming other booking sites.
- Mention that a local city tax, where it applies, is paid at the hotel.
- If no hotel matches, say so plainly and suggest which requirement to relax (dates, budget, cancellation, meal plan, rating). Do not present hotels that break the user's requirements as if they matched.

## 4. Booking

Staylo never books or charges anything from the chat. To book, the user opens the link of a result (or one from `get_booking_link`) and completes the booking and payment on the Staylo website. Prices are live and are confirmed on that page.
