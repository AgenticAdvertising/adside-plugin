---
name: ad-copy
description: Write or vary ad copy (primary text, headline, description and call to action) for Adside creatives, and save it with them. Use when someone asks for ad copy, captions, headlines, text variations or a call to action for creatives in an Adside drop or for ad images they have.
---

# Write ad copy for creatives

Copy is the text around a creative in the ad: primary text above it, a headline and a description below it, and a call-to-action button. Adside writes it from the creative's images and the brand kit.

## Write it

- **From the images**: `creative_tools_copy_generate` with the creative's image URLs (`imageUrls`; for a drop, take them from `creatives_get`). Pass `field` to write only one field, and `currentCopy` to keep the fields the person already likes.
- **Variations**: `creative_tools_copy_variations` with the `imageUrls`, the `field`, a `seed` (the current text) and a `count` of 1 to 3. Pass the variations you already have in `existingVariations` so new ones take a different angle.

Show each option with its length. Most placements cut the text after about 125 characters of primary text, 40 of headline and 25 of description, so put the point first.

## Save it

When the person picks the copy for a creative in a drop, save it with `creatives_copy`:

- `dropId` and `creativeId`
- `baseCreativeRevisionId`: the creative's `currentCreativeRevisionId` from `creatives_get`
- `copy` with all four fields: `primaryText` (up to 1,024 characters), `headline` (up to 255), `description` (up to 255) and `callToAction`, one of Meta's buttons such as `SHOP_NOW`, `LEARN_MORE`, `SIGN_UP`, `BOOK_NOW`, `GET_OFFER`, `DOWNLOAD` or `CONTACT_US`

Copy belongs to one version of the creative. If the creative changed since you read it, the save is refused: read it again with `creatives_get` and check the copy still fits. If the creative is edited after you save, save the copy again for the new version.

## Rules

- No claim, number or review without a source the person gave or Adside holds.
- No em dashes, no lists of three, and no stock phrases such as "unlock", "elevate", "seamless" or "game-changing". They read as machine-written, and Adside's creative agent is not allowed them on the ads either.
- Match the brand's tone from its brand kit, and the language of the market the ad runs in.
