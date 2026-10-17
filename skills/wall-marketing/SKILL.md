---
name: wall-marketing
description: Use the Wall Marketing MCP server to earn commission as an ambassador (find, claim and submit venues for an advertising screen), to book adverts on e-paper screens inside bars, cafés, hostels and gyms, or to manage a venue's screens and earnings. Use when the user wants to earn money signing up venues, advertise in a city, or asks about their Wall Marketing screen.
---

# Wall Marketing

The `wall-marketing` MCP server (`https://www.wall.marketing/mcp`) acts in the role the user chose when signing in: advertiser, venue (tools `host.*`) or outreach team (tools `ambassador.*`). A sandbox connection has every tool on made-up data. If a tool you need is missing, the user signed in with another role; tell them to reconnect and choose it.

## Earning as an ambassador (outreach team)

1. `ambassador.account.me` first: it gives the commission per venue that goes live, how many venues may be claimed at once and for how long, and the balances.
2. `ambassador.account.set_location` with the area the user works in, then `ambassador.venues.suggestions` for scored venues without a screen. Show the best few with rating, distance and score.
3. `ambassador.venues.claim` before the user approaches a venue, so nobody else on the team does. Use `ambassador.venues.release` if they decide not to.
4. The user talks to the owner or manager. You never contact venues yourself.
5. When the owner agrees in principle, `ambassador.venues.submit` with the contact's name, role and phone or email. Wall Marketing sends them the hosting agreement.
6. `ambassador.venues.list` shows where each venue is; the commission is confirmed when the venue's screen goes live. `ambassador.earnings.wallet` and `ambassador.earnings.request_payout` handle payouts (identity verification and payout details are set once on the outreach dashboard).

A venue the user knows but that isn't suggested can be added with `ambassador.venues.add` (name and street address); it is vetted on Google the same way.

## Booking adverts (advertiser)

1. `advertiser.account.limits` before booking: spending limits, approval rules, whether a card is saved.
2. `advertiser.venues.search`, then `advertiser.bookings.quote`. Dates are YYYY-MM-DD and `end_date` is exclusive. Never invent venue IDs.
3. Tell the user the total price and get their go-ahead before `advertiser.bookings.create`.
4. `advertiser.artwork.upload` converts the image to the six-colour e-paper screen; show the preview.
5. Follow the booking's `next_step` (pay with `advertiser.bookings.pay`, or send the user the payment link). `advertiser.bookings.report` gives proof of display.

Venues take no part in booking: a paid booking is scheduled at once.

## Venues hosting screens

`host.venue.overview` shows the screens, adverts and earnings; `host.screens.report_advert` objects to an advert; `host.screens.set_wifi` stages new WiFi; `host.earnings.withdraw` pays out the venue's share.
