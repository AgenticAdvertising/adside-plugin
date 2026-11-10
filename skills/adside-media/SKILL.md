---
name: adside-media
description: "Generate ad images, video clips, voice-overs, sound effects, music, talking avatars and lip-synced clips with Adside's media models through the adside command line: pick a model, price the request, get the person's OK, make one paid output per request ID, wait for it and save it. Charged to the organization's media credit."
---

<!-- @generated from packages/adside-cli/src/plugin-skills and api-documentation/api-reference/cli-catalog.json by `pnpm docs:generate`. Edit the template, not this file. -->

# Adside media

Every output costs money, charged to the organization's media credit when the job is created. Check the setup in the `adside` skill first: `adside` installed, logged in, and the workspace known.

## Commands

- `adside media`: recommend
- `adside media avatars`: cancel, estimate, generate, get, models
- `adside media images`: cancel, estimate, generate, get, models
- `adside media jobs`: list
- `adside media lipsync`: cancel, estimate, generate, get, models
- `adside media music`: cancel, estimate, generate, get, models
- `adside media sounds`: cancel, estimate, generate, get, models
- `adside media speech`: cancel, estimate, generate, get, models
- `adside media videos`: cancel, estimate, generate, get, models
- `adside media voices`: list
- `adside characters`: create, delete, get, list, update
- `adside credits`: balance, ledger

Read a command's `--help` before using it: the flags differ by type and model. `recommend`, `models`, `estimate`, `get`, `voices list`, `jobs list` and `credits balance` never charge.

## Before anything is paid

1. Run `adside media recommend --task '<what it is for, the placement, the length, cheap or best>'`. It returns up to three models, best first, each with `why`, ready-to-use `parameters`, its `priceUsd` and a `promptGuide`. Add what you know as flags, which win over the task: `--type video`, `--aspect-ratio 9:16`, `--duration 6`, `--max-price-usd 2`, `--priority cost`.
2. Write the prompt the way the model's `promptGuide` says. Never use a model ID from memory: take it from `recommend` or `models`.
3. Run `estimate` with the same flags you will generate with, and tell the person the price.
4. Generate only once the person agrees. A request that already sets a budget ("three 6-second clips, up to $5 in all") covers the jobs inside it.

Always pass both of these to `generate`:

- `--request-id <task>:<name>:v1`. Running the same command again returns the same job and never pays twice, so a retry after a timeout is safe. A new take needs a new ID (`…:v2`).
- `--max-price-usd <price>`. Adside refuses a job that would cost more, before charging.

Make a still first and iterate on it, since a still costs cents; then animate it with `adside media videos generate --first-frame <assetId>`. Make one take before any variant, then send variants as separate jobs, each with its own ID.

## Waiting

A clip takes minutes. `--wait` holds the command until the job ends, up to `--wait-timeout` (15 minutes by default). Your shell may stop a command sooner (Claude Code's limit is 10 minutes), so pass `--wait-timeout 9m`, or run the command in the background.

The exit code says how it ended: 0 completed, 1 bad input or an HTTP error, 2 failed, cancelled or expired, 3 still running at the timeout. On 3, keep waiting with the command it prints, `adside media videos get --job-id <id> --wait` (or the job's own type), which never pays again.

`--out <file>` saves the finished output to a new file on this computer; it never overwrites one. The job's `outputs[0]` also has its `assetId`, which the workspace's asset library keeps.

## When a job fails

- `MODERATION_REJECTED`: rephrase the prompt; never send it again unchanged.
- `INPUT_REJECTED`: tell the person the reason, and change the input.
- `UNCERTAIN_SUBMISSION`: report it, and submit nothing else for that output: the provider may have made it.
- `TIMEOUT` or `PROVIDER_ERROR`: one new take, with a new request ID.
- HTTP 400: `details` names the supported values; fix the request.
- HTTP 402: the organization's credit is too low. Stop and say so; `adside credits balance` shows it.
- HTTP 429: wait for `Retry-After`, then run the same command again.

Cancelling a job the provider has already accepted still costs. A job that never reached the provider is given back and shows `chargedUsd` 0.

## Audio and performers

- **Speech** is priced by every character of the text, spaces and audio tags included. Pick a voice from `adside media voices list`. **Music** is billed per started minute and is instrumental unless `--instrumental false`.
- `adside media avatars generate` makes the person in a still say a line; `adside media lipsync generate` makes the speaker in a clip say a new one. Both take local files, asset IDs or, for a still, an https URL.
- `adside characters list` shows the workspace's recurring people and mascots. `--character <handle>` uses one in an image or an avatar.

## Rules for what you make

- **Never a testimonial or an endorsement.** A generated voice or person never speaks as a customer, real or invented, and never says a real person used or recommends the product (FTC 16 CFR 465). A generated narrator may describe the product.
- **A performer is a character**: an invented one, or a workspace character a person added with the depicted person's consent. Never any other real person or a lookalike. Never create a real-person character or confirm consent yourself: the person does it in Adside, under Characters.
- **Say it is AI** whenever people outside the organization will see or hear the output.
