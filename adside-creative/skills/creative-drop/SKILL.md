---
name: creative-drop
description: Make new ad creatives with Adside, or change ones Adside made. Use when someone asks for ads, ad creatives, statics, animations or short videos for Meta, TikTok, LinkedIn or another platform, wants more variations or new concepts, or wants to edit, keep, discard or undo creatives in an Adside drop.
---

# Make ad creatives with Adside

Adside's creative agent makes finished ads in the workspace's brand. You give it a prompt and references; it returns a **drop**: a set of numbered creatives, each a static, an animation or a video, rendered in the placement sizes it needs. You start the work, follow it, show the results, and pass on what the person wants changed.

Every tool below is one of the Adside tools. If they are missing, ask the person to connect Adside and sign in with their Adside account, then try again.

## 1. Pick the workspace

A workspace is one brand. Call `list_workspaces`. With one workspace, use it. With several, ask which brand the ads are for. Pass the same `workspaceId` to every call after that.

## 2. Check the brand is ready

Call `brands_creative_kit_preparation`. Adside builds a creative kit (logo, colors, fonts, product shots) from the brand's website. If it is not ready, a drop still starts but waits for it, so tell the person it will take longer.

## 3. Pick a direction

If the person gave no direction ("make some ads"), offer the creative styles first, as the `creative-styles` skill describes, or write a brief with the `creative-brief` skill. If the ad needs a recurring person or mascot, ask whether to use one of the workspace's characters (the `characters` skill).

## 4. Ask for references

References make better ads, so ask for them before every drop. Start without any only when the person says to.

Don't ask an open "any references?". Look first, then offer three or four real picks, each with one line on why:

| Where to look | What it gives | Tool |
| --- | --- | --- |
| The workspace's best ads | What already converts for this brand | `get_top_creatives`, then `get_creative_details` |
| Competitors' long-running ads | Angles the market keeps paying for | `list_competitors`, then `get_competitor_ads` with `activeOnly: true` and `sortBy: oldest` |
| The inspiration feed | Organic videos trending in the niche | `get_inspiration_feed` |
| Boards | Ads the team already saved | `list_boards`, `get_board` |
| The asset library | Product shots, logos, past renders, a character's images | `list_assets` with a `search` |

A drop takes up to 20 references, each an image or video in the workspace's asset library: `{ "type": "asset", "assetId": "..." }`. Bring each pick into the library first:

- **A tracked competitor's ad** (from `get_competitor_ads`, or a board item that has a `trackedCompanyId`, a `channel` and an `adArchiveId`): `creative_sets_references_import` with `ads` (up to 5), each `{ "trackedCompanyId": "...", "source": "<channel>", "adArchiveId": "..." }` exactly as the tool returned them, and `availableSlots`, the number of the 20 references still free. It copies the ad's images and videos into the library and returns one `assetId` for each.
- **Anything else** (the brand's own ad, a trending or saved inspiration video, a board item without those three IDs, a file the person links): `upload_asset_from_url` when you have a direct image or video link. Without one, describe it in the prompt.

Say in the prompt what to take from each reference ("the hook structure of the competitor ad", "the colour of the end card in asset 2"). The agent copies unlabelled references loosely. A competitor's ad is a reference for the angle or the format, never something to copy.

## 5. Write the prompt

The prompt is the brief. It should say:

- what the ads sell, to whom, and on which platform and placement
- the angle or angles to try, and any offer or call to action
- the kind (static, animation or video) and the sizes, when the person cares
- what must appear or must not, and any claim with its source
- what to take from each reference

If the request is thin ("make some ads"), use the `creative-brief` skill first, or ask one round of short questions. Do not invent numbers, reviews or quotes: the agent will put them on the ad.

**Check it makes sense before you pay.** Write the premise and every line the ad will say in plain words. Check that the situation really happens to the buyer, that each line makes sense on its own, and that the proof answers that exact situation. For a new concept, show the person those words before you start the drop. The agent's checks test format, not sense.

Two more rules for the prompt:

- A generated person is a character in a scene. It never speaks as a customer, reviewer or employee, and never claims experience or research ("I asked 100 people").
- Don't ask for "AI-generated" text on the ad itself unless the person asks for it. Disclosure goes on the platform's AI label at launch (see "Before it goes live").

## 6. Start the drop

A drop runs on the organization's Adside credits. Start one only when the person asked for creatives. If you are suggesting it, say how many you would make and wait for a yes. `credits_balance` shows the balance.

Call `creatives_create` with:

- `requestId`: a new, readable ID such as `summer-sale-statics-v1`. The same `requestId` never makes a second drop.
- `prompt`: the brief.
- `creativeCount`: only when the person named a number (1 to 30). Leave it out and Adside uses the number in the prompt, or 5.
- `references`: as above.

If the call times out or fails without an answer, never send it again with a new ID. Call `creatives_by_request_id` with the same `requestId` to get the receipt.

## 7. Follow it

The receipt has a `dropId`. Its `runId` can be empty until the work is scheduled; call `creatives_by_request_id` again until it is set, then `creatives_status` with `dropId` and `runId`.

Give the person the drop's link right away, so they can watch it in Adside: `https://app.adside.ai/org/<organizationId>/workspaces/<workspaceId>/creatives/<dropId>`. `whoami` gives the `organizationId`.

A drop takes several minutes. Check the status now and then, not in a tight loop; if the conversation would sit waiting, give the link and tell the person to ask you to check it.

| Status | What to tell the person |
| --- | --- |
| `QUEUED`, `RUNNING` | Still working; `progress` says the phase and how many are done |
| `NEEDS_CONFIRMATION` | Adside needs them to confirm something in the drop; send the link |
| `DELIVERED` | All done |
| `PARTIAL` | Some are done; `result.failures` gives each failure's reason |
| `FAILED`, `CANCELLED` | It stopped; say why if `result` says |

## 8. Show and check the results

Call `creatives_get` with the `dropId`. Each creative has a `number`, a `title`, a `note`, its `kind` and `media` (one URL per size). Show each creative by number and title, with one image where the app can display it, and one line on its idea. Refer to creatives by their number, as the drop page does.

Then look for what the agent's checks miss, and fix it with an edit before anyone keeps the creative:

- **Invented text**: read every word on generated screens, signs and packaging. Generated screens show made-up words, sometimes for only a few frames of a video.
- **Real brands on props**: zoom in on laptops, phones and cups. A real Apple logo has appeared on a generated laptop.
- **9:16 as its own picture**: the story size should fill the full height, not be a square with bands. A frame where one flat colour covers more than about a fifth of it was laid out for another size.
- **Each line on its speaker**: a caption over the listener's face confuses viewers.
- **Videos**: you can't watch them frame by frame here, so ask the person to check the first second (something should already move), the last frames (a talking shot can end mid-blink) and the sound level.

## 9. Change, add, keep

- **Edit**: `creatives_edit` with a new `requestId`, an `instruction`, and the targets: `targetCreativeNumbers` (the numbers the person sees), `targetCreativeIds`, or `allCreatives: true`. Add `references` when the change needs one. To change sizes, see the `creative-formats` skill.
- **More creatives**: `creatives_add` with a new `requestId`, an `instruction` and a `creativeCount`.
- Edits and additions are new runs on the same drop. Follow them with `creatives_runs_by_request_id` (the `dropId` and the `requestId`), then `creatives_status`.
- A drop works on one request at a time. If it is busy, wait and send the same request again with the same `requestId`; it never runs twice.
- **Keep or discard**: `creatives_review` with `kept`, `discarded` or `unreviewed`, only for the creatives the person chose. Kept creatives are the ones offered when a campaign is built.
- **Undo**: each creative in `creatives_get` lists its `revisions`. `creatives_revisions_get` shows one of them, and `creatives_revert` restores it (pass the current revision as `expectedCreativeRevisionId`) without touching the other creatives.
- **Stop**: `creatives_cancel` with the `dropId` and `runId`. Creatives already finished stay.
- **Find an earlier drop**: `creatives_list`, with a `query` to search.

## Before it goes live

This plugin never launches ads or changes campaigns. When the person wants creatives live, tell them it happens from Adside's launch flow, which asks for their confirmation before anything reaches the ad platform.

If a creative shows a realistic generated person or voice, remind them to switch on the platform's AI label when they launch it: TikTok requires one for realistic AI content, and Meta may add its own "AI info" label. For ads shown in New York or the EU, or a performer who could pass for a real customer, suggest they check with their lawyer whether an on-screen label is needed too.

## With a terminal

In Claude Code or Codex, the Adside CLI plugin (`claude plugin install adside --marketplace AgenticAdvertising/adside-plugin`) does what a drop can't: single images, video clips, voice-overs and music with `adside media`, characters, and the full creative styles. Its `adside-media` skill prices every job before paying for it. On the web or a phone (claude.ai, ChatGPT), stay with drops.
