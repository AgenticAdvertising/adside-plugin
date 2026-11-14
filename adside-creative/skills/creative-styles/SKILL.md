---
name: creative-styles
description: Offer Adside's creative styles, tested ways to make an ad (product demo, talking performer, micro-drama, mascot, comedy), as directions for new ads, and apply the chosen one to a creative drop. Use when someone asks for ads without a clear direction or format, asks for ad ideas, styles, formats or inspiration, or names a style such as UGC, micro-drama, mascot or a product demo.
---

# Offer the creative styles

A creative style is a tested way to make an ad: a method, and in the full version, agent skills that make it end to end. When someone asks for ads without a direction, offer the styles before you write a prompt, with one line each, and let them pick one or two.

The Adside tools can't list the styles yet. These are the five in Adside's catalog when this plugin was released; with a terminal, `adside creative-styles list` shows the live catalog.

| Style | The ad | Fits |
| --- | --- | --- |
| Product hero demo | The product does the customer's job on screen, under way within 3 seconds | Software and products with a visible result |
| UGC performer | A performer talks to camera about one moment of the buyer's day; the product's real screens prove it | TikTok and Reels |
| Micro-drama | A 10–15 s three-act story whose twist the product causes | Brands with a relatable everyday situation |
| Mascot | One recurring character whose single absurd trait is the product's value | Brands that want a recognisable face across many ads |
| Writers' room | Funny ads where the laugh is the product's value | Crowded feeds, brands that can take a joke |

## Apply a style to a drop

A drop doesn't run the style's own tools, so it follows the method rather than reproducing the style exactly. Write the method into the drop's prompt, along with the references and the brief (the `creative-drop` skill).

**Product hero demo.** The ad is a demonstration, not a description: input, action, outcome, payoff, in one continuous take, under way from the first frame and the outcome held to the last. Software: the real screens, the request typed, the click, the result circled and named in the site's own words. Consumer goods: the site's real product photos as the start, with hands using the product. Default: two statics frozen at the moment the result appears and one 7–8 s video that works on mute.

**UGC performer.** One performer talks to camera about one specific moment of the buyer's day (a time, a place, one detail), with a hook in the first two seconds: a callout, a confession or a pattern break. The product's real screens prove the line. Default: a 14–20 s video (hook, the product's screens with the performer's voice over them, their reaction, end card) and two statics: the performer with the hook as a caption, and a native format such as a notes-app list. The performer is a character in a dramatized moment, never a customer or reviewer. The installed style also writes "AI-generated performer" on screen; in a drop, leave that line off unless the person asks, and remind them of the platform's AI label at launch.

**Micro-drama.** Act 1 is a situation a stranger recognises in a second. Act 2 breaks the viewer's prediction (a reversal, a fake-out, a double meaning), and the product is the cause. Act 3 lands a reaction and a callback, then an end card. Dialogue reads as captions on each speaker's own shot, so it works on mute. Default: one 10–15 s video and two statics of the key frame with the twist as the headline. Use a character (the `characters` skill) so the people stay the same across shots.

**Mascot.** One character carries every ad. It has exactly one absurd physical trait that is the product's value in physical form (eight arms for a cleaning service, a clock for a face for a time-saver), a persona turned up to 11 that reacts to the buyer's pain, a signature line and a signature sound. Default: two statics (two pains, the same character, a speech bubble and real product proof) and a 10–13 s video that opens on the trait mid-reaction and ends on a product end card. Use the brand's existing mascot as a character if it has one; never redesign it.

**Writers' room.** Do the room here, with the person, before the drop. Pitch twenty premises across six devices (exaggeration, reversal, double meaning, a broken pattern, understatement, callback), punch up the best eight, and keep only the jokes where the product's value is the punchline, every claim is true, and someone who never saw the brief gets both the joke and the product. Send the winners to the drop. Default: two statics, each a one-second visual gag with a short headline in the buyers' words, and a 10–14 s sketch: the setup inside 3 seconds, a held beat, the turn on a hard cut, the real product on the end card.

## With a terminal

The full styles run in Claude Code or Codex, with the Adside CLI and the CLI plugin. They make their own images, video, voices and talking performers with `adside media`, check every frame, and deliver the finished ads to the asset library.

1. `adside creative-styles get --slug micro-drama` says what the style makes and what it needs.
2. `adside creative-styles install --slug micro-drama` in a fresh project folder (`--agent codex` for Codex, `--into <folder>` for another skills folder). It brings the `adside-studio` toolkit the styles run on.
3. Ask the agent for ads "in the micro-drama style".

What to know before a run:

- The machine needs Node 22 or later, Python 3.9 or later and ffmpeg; the toolkit's setup installs a headless Chromium. That rules out claude.ai and ChatGPT on the web.
- Media is charged to the organization's media credit as each job starts: about $1.50–2.60 per run for most styles, under $0.10 for a software product demo.
- Talking performers (UGC performer, mascot, writers' room) need CLI 0.4.0 or later, and one performance can take 15–27 minutes.
- In zsh, write request IDs as `${R}:name`, never `$R:name`: `:c` and `:s` are zsh modifiers and silently change the ID.
