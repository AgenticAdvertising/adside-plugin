---
name: creative-brief
description: Write a creative brief for an Adside workspace from the brand's own results, its competitors' ads and its brand kit. Use when someone asks for ad ideas, concepts, angles or hooks, asks what ads to make next, or gives a thin request such as "make some ads" before a creative drop.
---

# Write a creative brief

A good brief starts from evidence: what already sells for this brand, what competitors keep running, and what the brand kit allows. Gather only what the request needs, then write the brief and offer to make the creatives with the `creative-drop` skill.

Use the workspace the person chose (`list_workspaces` if you don't know it), and pass the same `workspaceId` to every call.

## Gather

Pick the sources that fit; you rarely need all of them.

- **The brand**: `get_workspace_brand_details` for the brand kit, tone and products; `list_products` for the catalog.
- **What works for them**: `get_top_creatives` with the platform (`source`) and a period such as `last_30_days`. Rank by `conversion` with `sortSubMetric: costPer` and `sortOrder: asc` for the cheapest results, or by `spend` for what the budget backs. Open the best two or three with `get_creative_details` for the transcript and analysis. `list_messaging_themes` groups their ads by message.
- **Competitors**: `list_competitors`, then `get_competitor_ads` with `activeOnly: true` and `sortBy: oldest` to find ads that have run a long time, which usually means they work. Each answer says when the ads were last read; say that date when you cite them, and never call an old ad "currently running".
- **Trends**: `get_inspiration_feed` for the most-viewed organic TikTok videos in the brand's niche, good for hooks.
- **What the team saved**: `list_boards` and `get_board` for ads the team already liked.
- **What the team knows**: `search_brain` for the audience, offers, past learnings and rules such as claims they may not make.

If the workspace has no ad data yet, say so and build the brief from the brand and competitors.

If the person has no direction in mind, also offer the creative styles (the `creative-styles` skill): each is a tested way to make an ad, and the chosen one shapes the angles.

## Write

Keep it under 250 words, in this order:

1. **Goal**: what the ads should get (sales, sign-ups, installs) and on which platform and placement.
2. **Audience**: who they are and what they want, in one or two lines.
3. **Offer and call to action.**
4. **Angles**: three to five, each with a hook, the proof behind it and why you picked it (name the ad or data it comes from).
5. **Kind and sizes**: static, animation or video, and the placements.
6. **Must and must not**: required elements, claims with their source, words or images to avoid.
7. **References**: three or four picks for the drop, each with what to take from it ("the hook structure", "the end card's colour"), and the IDs you need to bring it in: an asset's `assetId`, or a competitor ad's `trackedCompanyId`, `channel` and `adArchiveId`. Offer them to the person as real picks with one line on why; don't ask an open "any references?". The `creative-drop` skill says how to turn each one into a reference.

## Check it makes sense

Before you offer to make the creatives, read each angle as the buyer would. Check that the situation really happens to them, that each line makes sense on its own, and that the proof answers that exact situation. A brief can pass every format rule and still describe an ad nobody understands.

## Rules

- Every number, review or quote in the brief needs a source the person gave or Adside holds. If there is none, leave it out or mark it as something to confirm.
- Use competitors' ads to learn structure and hooks, never to copy their words or visuals.
- Write for the brand's own team: plain words, no jargon, no filler.
- A generated person in an angle is a character in a scene, never a customer, reviewer or employee.
