---
name: tracked-link
description: Build a tracked link (a page address with UTM tags on the end) from a page address, a channel, a type of item and a campaign name. Use when the user asks for a tracked link, a UTM link, or a link for a post, email or advert.
---

# Tracked link

Build one tracked link, the same way as the Calendar tab of `plan/campaign-plan.xlsx`.

## Steps

1. Get four things: the page address, the channel, the type of item and the campaign name.
2. If any are missing, ask for each one with one short question. Never guess, and never invent a page address.
3. Turn the channel, type and campaign into tags: lower case, with a hyphen in place of each space.
   - Channel: `Email to dog owners` is `email-dog-owners`. `Email to vet practices` is `email-vet-practices`. `Facebook`, `Instagram` and `LinkedIn` are `facebook`, `instagram` and `linkedin`.
   - Type: one word for one item: `email`, `post`, `reel` or `story`.
   - Campaign: `A calmer Christmas` is always `a-calmer-christmas`, exactly as it is written in the Calendar links.
4. Build the link in this order:
   `<page address>?utm_source=<channel>&utm_medium=<type>&utm_campaign=<campaign>`
5. If the page address already has a `?`, join with `&` instead. Change nothing else in the address.

## Reply

Show the link on its own line. Then add three short lines:

- Channel: the channel tag
- Type: the type tag
- Campaign: the campaign tag
