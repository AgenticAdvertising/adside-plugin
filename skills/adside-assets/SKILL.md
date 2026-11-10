---
name: adside-assets
description: "Find, upload, import, tag, download and archive the images and videos in an Adside workspace's asset library with the adside command line, including files from this computer. Use when the person wants to put creatives into Adside, get them out, or organize them."
---

<!-- @generated from packages/adside-cli/src/plugin-skills and api-documentation/api-reference/cli-catalog.json by `pnpm docs:generate`. Edit the template, not this file. -->

# Adside assets

The asset library holds a workspace's images and videos: uploads, generated media and imported creatives. Check the setup in the `adside` skill first: `adside` installed, logged in, and the workspace known.

## Commands

- `adside assets archive`: Archive an asset.
- `adside assets batch`: Look up assets in this workspace by ID.
- `adside assets delete`: Remove an asset and queue storage cleanup.
- `adside assets download`: Download an asset to a new local file.
- `adside assets get`: Get an asset and its download URL.
- `adside assets import-url`: Import a public image or video URL into the asset library.
- `adside assets list`: List the workspace's assets, with filters and cursor pagination.
- `adside assets status`: Check asset processing and upload readiness.
- `adside assets transcription`: Request or read a video transcription.
- `adside assets update`: Update asset metadata.
- `adside assets upload`: Upload a local media file and publish it in the asset library.
- `adside assets tags list`: List the workspace's most-used asset tags.
- `adside assets tags update`: Add or remove asset tags.
- `adside assets uploads complete`: Publish an uploaded asset (safe to repeat).
- `adside assets uploads create`: Reserve a media upload and return a single-file upload ticket.

Read a command's `--help` before using it.

## Working with files

- **Find**: `adside assets list --limit 20`, newest first. Filter with `--search`, `--tags '["approved"]'` or `--media-type '["image"]'`, and continue with the returned `nextCursor` through `--cursor`. `adside assets get --asset-id <id>` reads one.
- **Upload from this computer**: `adside assets upload --file ./creative.png`. It reserves the upload, sends the bytes and publishes the asset in one command. Keep the asset ID it returns. If the bytes were sent but the last step failed, run the command it prints instead of uploading again.
- **Import from the web**: `adside assets import-url --url <https-url>`.
- **Download to this computer**: `adside assets download --asset-id <id> --out ./creative.png`. Choose a new file name: it never overwrites one.
- **Tag**: `adside assets tags update --asset-id <id> --add '["approved"]' --remove '["draft"]'`.

Keep IDs as strings. A failed command exits with a nonzero code: never treat its message as an asset.

## Changes need the person's OK

Commands make their change on the first call. Uploading or tagging what the person asked for needs no second question. Before `adside assets delete` or `adside assets archive`, name the assets, and wait for a yes: a deleted asset cannot be brought back.
