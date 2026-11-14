# Adside Creative

Make on-brand ad creatives from a conversation with Claude. Adside Creative pairs the Adside connector with six skills that teach Claude how your team makes ads in Adside: start from what already works and from your references, pick a tested style, keep your characters the same, make the creatives, fit them to every placement and write the copy.

## What it does

- **Creative brief** (`creative-brief`): builds a brief from your best-performing ads, the messages behind them, the ads your competitors keep running, trending organic videos in your niche and your brand kit.
- **Creative drops** (`creative-drop`): offers three or four references from your best ads, competitors' ads, trending videos, boards and assets, checks the idea makes sense before paying, asks Adside's creative agent for a set of finished statics, animations or videos in your brand, follows the work, checks each creative, and passes on edits, additions, keeps, discards and undos.
- **Creative styles** (`creative-styles`): offers Adside's tested ways to make an ad (product demo, talking performer, micro-drama, mascot, comedy) when you have no direction, and writes the chosen method into the drop.
- **Characters** (`characters`): keeps the same person, performer or mascot across ads by passing a workspace character's images as references, and helps you create one on Adside's Characters page.
- **Placement sizes** (`creative-formats`): makes the 9:16, 4:5, square, landscape, 16:9, X and link-ad versions, composes 9:16 as its own full-height picture, and checks which sizes a Meta ad set still needs.
- **Ad copy** (`ad-copy`): writes and varies primary text, headlines, descriptions and calls to action from the creative itself, and saves the chosen copy with it.

Ask in plain words, for example "Make five static ads for our summer sale on Instagram Stories", "What should our next ads say, based on what's working?", "Make a micro-drama ad with Maya" or "Give me a 4:5 version of creatives 2 and 3".

## Install

On claude.ai and in Cowork, add Adside Creative from Claude's plugin directory. In Claude Code:

```bash
claude plugin install adside-creative --marketplace AgenticAdvertising/adside-plugin
```

## What you need

- An Adside account with a workspace for your brand. Creative drops run on your organization's Adside credits.
- The Adside connector. After you add the plugin, connect it from the plugin's Connectors tab and sign in with your Adside account. In Claude Code, the connector signs in through your browser the first time it is used.

## AI disclosure

Creative drops put no "AI-generated" text on the ads unless you ask for it. When an ad with a realistic generated person or voice goes live, switch on the ad platform's own AI label: TikTok requires one for realistic AI content. Generated people appear only as characters in a scene, never as customers or reviewers, and a character of a real person needs that person's consent, confirmed in Adside by a person.

## With a terminal

On claude.ai and in Cowork, the plugin makes creatives through drops. In Claude Code or Codex, add the Adside CLI plugin for single images, video clips, voice-overs and music, characters from the command line, and the full creative styles:

```bash
claude plugin install adside --marketplace AgenticAdvertising/adside-plugin
```

## What it connects to and sends

The plugin contains only instructions (Markdown) and one connector entry. It runs no code on your computer and installs no packages.

- It connects to one server, Adside's MCP server at `https://api.adside.ai/mcp`, with the Adside account you sign in with. Claude sees your workspaces, brand kit, asset library, ad results, tracked competitors and creative drops there, as your role in Adside allows.
- What you ask for, including your prompts, the references you choose and the copy you approve, is sent to Adside to make and store the creatives. Adside's [privacy policy](https://www.adside.ai/privacy) covers how it is handled.
- Creatives stay in your Adside workspace. The plugin never launches ads or changes your campaigns on Meta, Google, LinkedIn, TikTok or any other platform.

## Support

Write to support@adside.ai, or see [docs.adside.ai](https://docs.adside.ai/mcp/connect).
