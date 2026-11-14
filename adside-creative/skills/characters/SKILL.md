---
name: characters
description: Keep the same person, performer or mascot across Adside ads with a workspace character, or help someone create one. Use when an ad needs a recurring face, a brand mascot, a spokesperson or a performer, when someone asks to create or reuse a character, or when ads should show "the same person" or "our mascot".
---

# Use a character in ads

A character keeps one face, performer or mascot the same from one ad to the next. In Adside it is 1 to 8 reference images (best first; the first is the cover a talking performer speaks from), up to 400 characters of identity notes saying what must never change, and a stock voice. Characters belong to one workspace.

## Ask first

When an ad needs a recurring person or mascot, ask whether to use one of the workspace's characters before you write the prompt. The Adside tools can't list characters yet, so ask the person which one, or send them to the Characters page to look:

`https://app.adside.ai/org/<organizationId>/workspaces/<workspaceId>/characters` (`whoami` gives the `organizationId`). In the app it sits under Brain, then Characters.

## Use one in a drop

A character's images are ordinary images in the workspace's asset library, but the Adside tools can't tell which ones yet. Search `list_assets` for the character's name, or for the file names the person gives you from the asset library, and show them the matches. Pass only the images they confirm to the drop as asset references, cover first. Then say in the prompt which references are the character and what must not change ("the same woman in every creative: short red hair, round glasses, green jacket"). Ask the person for the character's identity notes from its page if you don't have them.

## Help create one

Creating a character happens in the app. On the Characters page, **New character** offers two ways:

- **Describe one**: Adside drafts the images from a description.
- **Use your images**: upload photos, or choose them from the asset library.

Then name it and pick its kind: **AI persona** (an invented person), **Mascot** (a non-human or stylized character) or **Real person**.

Help the person get a good one:

1. Several angles of the same character on a plain, light background, in even light and with no text: full body from the front, three-quarter, and a close-up of the face.
2. For the cover, a face looking straight at the camera with a visible mouth. A beak or a tiny mouth gap lip-syncs badly.
3. Identity notes that list what must never change: exact colours, outfit, a mark on the face. Not a personality description.
4. A voice, if the character will speak.

If the brand already has a mascot, use its existing artwork. Never redesign it.

## Real people

A **Real person** character needs consent confirmed in Adside by a person. The person depicted must be the one confirming, or an adult who gave written permission to use their likeness in ads. Adside refuses the confirmation from an agent, so never try to confirm it yourself. Never make a character that looks like a real person who hasn't agreed, including celebrities.

## In ads

A generated person is a character in a scene. It never speaks as a customer, reviewer or employee, and never claims to have used the product. When an ad with a realistic generated person goes live, the person should switch on the platform's AI label (see the `creative-drop` skill, "Before it goes live").

## With a terminal

In Claude Code or Codex, the Adside CLI does more with characters than the Adside tools here can:

- create one: `adside characters create --name Maya --kind ai_person --reference ./front.png --reference ./three-quarter.png --identity-notes "..." --voice-id <id>` (a `--reference` is a local file or an asset ID, best first)
- find them: `adside characters list` and `adside characters get --character maya`
- use one: `--character maya` on `adside media images generate` and `adside media avatars generate`, and `--voice @maya` on `adside media speech generate`. Video models take no character yet: make the first frame with `images generate --character maya`, then animate it with `videos generate --first-frame <assetId>`.

The CLI plugin's `adside-media` skill covers pricing and running those jobs.
