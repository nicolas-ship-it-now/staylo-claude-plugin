# Staylo for Claude

**Hotels at net rates, right in your conversation.** Ask Claude for a place to stay and get live hotel prices from Staylo, shown next to each hotel's public price so you see exactly how much you save. Filter by budget, free cancellation, breakfast or guest rating, then book in one click on the Staylo website.

## What's inside

- **Staylo connector** (remote MCP server at `https://mcp.staylo.fr`): three read-only tools.
  - `search_hotels` — available hotels for a destination and dates, with the Staylo price, the public price, the saving, rating, cancellation terms and a booking link, shown as an interactive carousel. Filters: adults, children's ages, rooms, stars, free cancellation, meal plan, maximum price per night, minimum rating, language, currency.
  - `get_hotel` — the rooms of one hotel with price, meal plan and cancellation terms.
  - `get_booking_link` — the booking link for a hotel, dates and guests.
- **`find-hotel-deals` skill**: helps Claude turn a request such as "a refundable hotel with breakfast in Rome under €180" into the right search, and present the results clearly.

## Try it

- "Find me a hotel in Lisbon from May 3 to 6 for two adults, under €150 a night."
- "Refundable hotels with breakfast in Rome next weekend, rated 8 or more."
- "Family room in Barcelona for 2 adults and kids aged 5 and 8, July 10 to 14."

## How it works

Prices are live rates from Staylo's supplier, Nuitee (LiteAPI), for the exact dates and guests requested, taxes included (a local city tax, where it applies, is paid at the hotel). The public price shown is the hotel's suggested retail rate supplied with each offer.

Nothing is booked or charged from the chat. Each result links to the Staylo booking website, where the user completes the booking and payment (processed by Nuitee).

## Data and privacy

The plugin runs no local code. Claude calls the remote server `https://mcp.staylo.fr`, which receives only the search parameters (destination, dates, guests, filters, language, currency), sends them to Nuitee to get availability and prices, and records anonymous usage statistics (no IP address, no identity). Opening a result goes through `https://mcp.staylo.fr/r`, which counts the click and redirects to the booking website. No account is needed. Full details: [privacy policy](https://mcp.staylo.fr/privacy).

## Support

Documentation: https://mcp.staylo.fr/docs · Contact: contact@staylo.fr

## License

MIT
