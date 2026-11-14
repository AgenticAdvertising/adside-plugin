---
name: creative-formats
description: Resize Adside creatives for other placements, such as a 9:16 version for Stories and Reels, 4:5 for feeds, square, landscape or link ads, or check which sizes a Meta ad set still needs. Use when someone asks for other sizes or aspect ratios of creatives in an Adside drop, or whether creatives are ready for an ad set.
---

# Adapt creatives to every placement

Each Adside creative can come in seven sizes:

| Size | Pixels | Typical placement |
| --- | --- | --- |
| `story` | 1080×1920 (9:16) | Stories, Reels, TikTok |
| `portrait` | 1080×1350 (4:5) | Feeds |
| `square` | 1080×1080 (1:1) | Feeds, carousels |
| `landscape` | 1440×1080 (4:3) | Some feed and display slots |
| `wide` | 1920×1080 (16:9) | YouTube, in-stream video |
| `twitter` | 1600×900 | X |
| `link` | 1910×1000 | Link and right-column ads |

`creatives_get` lists the sizes each creative already has in its `media`.

## Make the missing sizes

Call `creatives_edit` with:

- a new `requestId`
- the targets: `targetCreativeNumbers`, `targetCreativeIds` or `allCreatives: true`
- `formatAdaptation: { "requiredFormats": ["story", "portrait"] }` with the sizes needed
- an `instruction` such as "Adapt these to the new sizes and keep the design, copy and product shot the same."

Then follow the run as the `creative-drop` skill describes (`creatives_runs_by_request_id`, then `creatives_status`) and show the new sizes with `creatives_get`.

In `story`, Adside keeps text clear of the platform's buttons and captions (the top 14%, the bottom 35% and 6% at each side), so a 9:16 version can be laid out differently from the square one. That is expected.

**Make 9:16 its own picture.** When the ads will run in Stories, Reels or TikTok, ask for `story` in the first drop rather than adapting a square later, and say in the instruction that the 9:16 version fills the full height, never a square with bands above and below. The safe zones only keep text off the app's buttons; the picture still runs to every edge. A frame where one flat colour covers more than about a fifth of it was laid out for another size: ask for it again.

Check every new size as step 8 of the `creative-drop` skill describes.

## Check a Meta ad set

`creatives_meta_prepare` takes the `dropId`, a Meta `adsetId` and the `creativeIds`, and says which sizes that ad set's placements still need for each static creative. It only reads: it never makes a size and never publishes anything. Use it before the person launches, then make what is missing as above.

To find the ad set ID, `launch_catalog_campaigns` lists the workspace's active and paused Meta campaigns, and `launch_catalog_ad_sets` with a `campaignId` lists that campaign's ad sets.
