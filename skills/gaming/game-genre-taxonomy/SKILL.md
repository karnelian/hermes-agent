---
name: game-genre-taxonomy
description: "Use when classifying or correcting game genre labels by separating genre, player fantasy, setting, art tone, core loop, meta loop, platform, and service model; especially useful for Pokemon-like, creature-collection, monster-taming, MMO, RPG, fantasy, and live-service terminology."
version: 1.0.0
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [gaming, genre, taxonomy, positioning, terminology, game-design, research]
    related_skills: [game-research, game-concept-discovery, core-loop-designer, game-feature-prd]
---

# Game Genre Taxonomy

## Overview

Use this skill to describe games with precise, layered labels instead of mixing genre, setting, tone, business model, and platform into one vague phrase.

A common failure mode is calling a game something like "fantasy MMO" when the useful classification is actually "creature-collection MMO", "monster-taming RPG", or "Pokemon-like online RPG". "Fantasy" may describe the world, creature design, or art tone, but it usually does not explain what the player repeatedly does.

The goal is not to invent academic taxonomy. The goal is to produce labels that are accurate enough for product strategy, game design, market research, store positioning, article summaries, and build planning.

## When to Use

- The user asks "what genre is this game?", "what should we call this?", or "is this label accurate?"
- A game is described with vague labels such as fantasy, casual, RPG, MMO, open world, social, survival, cozy, roguelike, or Pokemon-like
- A market-research or article summary needs clean genre terminology
- A game concept needs a short pitch line, Steam/mobile category, competitor set, or reference-title framing
- The wording mixes setting, art style, player fantasy, mechanics, platform, and service model
- A label sounds familiar but does not explain the core loop

Do not use this skill alone for full game design, balance, UI flows, FTUE, or implementation planning. Hand off to the relevant design or build skill after the terminology is clean.

## Core Rule: Separate the Layers

Classify the game by layers. Do not let one layer pretend to be all the others.

| Layer | What it answers | Examples |
|---|---|---|
| Core genre / primary loop | What does the player repeatedly do? | creature collection, action RPG, farming sim, tactics, deckbuilder, extraction shooter |
| Sub-loop / combat model | How is the repeated play resolved? | turn-based battles, real-time action, auto-battler, match-3, grid tactics |
| Progression / meta loop | What grows over time? | party roster, base, gear, town, collection, account power, narrative branches |
| Setting / fiction | Where does it take place? | fantasy, sci-fi, modern, historical, post-apocalyptic, mythic |
| Art tone / vibe | How does it feel visually? | cozy, dark fantasy, anime, cute, grim, low-poly, painterly |
| Player fantasy | Who does the player become? | trainer, commander, survivor, shopkeeper, explorer, god, detective |
| Platform / interface | Where and how is it played? | mobile portrait, PC, console, VR, web, controller-first |
| Service model | How is it operated? | MMO, online co-op, live service, seasonal, premium, F2P, gacha |
| Commercial shorthand | What comparison helps users understand fast? | Pokemon-like, Soulslike, Vampire Survivors-like, Stardew-like |

A good final label usually combines two to four layers, not all of them.

## Classification Workflow

1. **Identify the player verb.** Ask what the player does every session: collect, tame, build, fight, explore, solve, survive, farm, trade, manage, decorate, optimize.
2. **Name the core loop before the setting.** If the setting can change without breaking the game, it is not the core genre.
3. **Separate combat/resolution.** "RPG" is often too broad; specify turn-based, action, tactics, auto-battler, deckbuilding, or simulation where useful.
4. **Separate service model.** MMO, live service, co-op, gacha, and seasonal are distribution/operation layers, not complete genres by themselves.
5. **Use comparison labels carefully.** "Pokemon-like" or "Soulslike" is useful shorthand, but convert it into mechanics when precision matters.
6. **Remove misleading labels.** If a label only describes theme or mood, demote it from genre to setting/tone.
7. **Produce a clean label stack.** Give a short public label, a precise design label, and a warning about labels to avoid.

## Output Pattern

When asked to classify a game, respond in this shape:

```text
Short label: <2-5 word audience-friendly label>
Precise label: <core loop + combat/resolution + progression/service layer>
Setting/tone: <fiction and vibe, not treated as the main genre>
Comparable shorthand: <optional reference title + why>
Avoid calling it: <misleading labels + reason>
```

Example:

```text
Short label: Creature-collection MMO
Precise label: Monster-taming RPG with online shared-world progression
Setting/tone: Bright fantasy creature world
Comparable shorthand: Pokemon-like, because collection, party growth, and creature battles are central
Avoid calling it: Fantasy MMO, because fantasy is a setting/tone and MMO is a service layer; neither names the collection/taming loop
```

## Pokemon-like / Temtem-like Games

For Pokemon, Temtem, and adjacent games, the primary classification should usually center on creature collection and monster taming, not fantasy.

Core elements:

- discovering creatures
- capturing, recruiting, hatching, or otherwise acquiring them
- building a roster or party
- training, evolving, breeding, fusing, or upgrading creatures
- battling through creature abilities and matchups
- exploring regions, routes, dungeons, gyms, arenas, or online zones
- trading, social comparison, PvP, or co-op where applicable

Prefer labels such as:

- creature-collection RPG
- monster-taming RPG
- creature-collection MMO
- monster-taming online RPG
- Pokemon-like RPG
- Pokemon-like online RPG
- collection-and-battle RPG
- creature-raising RPG

Use "fantasy" only as setting or tone:

- "fantasy creature-collection RPG"
- "bright fantasy monster-taming MMO"
- "anime fantasy creature battler"

Avoid making "fantasy" the main genre label unless the discussion is specifically about setting, art direction, fiction, lore, or theme.

## Label Corrections

### "Fantasy MMO"

Often too vague. It combines a setting/tone with a service model and omits the actual play.

Better replacements depend on the loop:

- creature collection + online world -> **creature-collection MMO**
- party creature battles + progression -> **monster-taming RPG**
- raids/classes/gear treadmill -> **theme-park MMORPG** or **tab-target MMORPG**
- player economy and territory -> **sandbox MMORPG**
- survival crafting in shared world -> **online survival-crafting RPG**

### "RPG"

Too broad by itself. Clarify the progression and resolution model.

- action RPG
- turn-based RPG
- tactical RPG
- creature-collection RPG
- party-based RPG
- narrative RPG
- idle RPG
- gacha RPG

### "MMO"

MMO describes concurrency and shared world/service shape. It does not identify the main loop.

Use it as a modifier:

- MMO creature collector
- MMORPG with class-and-raid progression
- MMO survival sandbox
- MMO social sim

### "Pokemon-like"

Useful audience shorthand, but not always precise. Translate it into concrete components:

- creature collection
- monster taming
- party-based creature battles
- type/matchup strategy
- exploration and regional progression
- trading, breeding, PvP, or completionist collection

If only one component exists, avoid overusing Pokemon-like.

### "Open world"

Open world is a world-structure label, not a complete genre. Pair it with the main loop:

- open-world survival crafting
- open-world action RPG
- open-world creature-collection RPG
- open-world driving sandbox

### "Cozy"

Cozy is tone/player emotion, not the mechanical genre. Pair it with activity:

- cozy farming sim
- cozy life sim
- cozy creature collector
- cozy shop-management game

## Good Label Stack Examples

| Bad / incomplete label | Better label | Why |
|---|---|---|
| Fantasy MMO | Creature-collection MMO | Names the collection/taming loop and keeps MMO as service form |
| Pokemon-like fantasy game | Fantasy monster-taming RPG | Makes the mechanic primary and fantasy secondary |
| Casual RPG | Mobile idle RPG with hero collection | Identifies platform, progression, and session pattern |
| Open-world game | Open-world survival-crafting game | Names what players do in the open world |
| Cozy fantasy | Cozy creature-raising life sim | Turns mood and setting into modifiers around the actual loop |
| Roguelike card game | Run-based deckbuilder roguelite | Clarifies run structure and deckbuilding core |
| Social MMO | MMO social-sandbox with player housing | Explains the social loop |

## Decision Heuristics

- If removing the setting leaves the game mostly intact, the setting is not the genre.
- If removing the service model leaves a playable single-player version, the service model is not the core genre.
- If a comparison title is needed for speed, also provide the underlying mechanics.
- If the label does not tell a designer what to prototype first, it is probably too vague.
- If the label does not tell a player what they will repeatedly do, it is probably marketing fluff.
- If two labels conflict, prioritize the one that describes repeated player action over the one that describes mood or fiction.

## Common Pitfalls

1. **Promoting setting into genre.** "Fantasy", "sci-fi", and "post-apocalyptic" are usually settings or tones. They become primary only when the task is specifically about fiction, lore, or art direction.
2. **Treating MMO as the whole genre.** MMO explains scale and operation, not the core loop. Always pair it with what players do.
3. **Using reference-title labels without translation.** "Pokemon-like" is useful, but explain whether it means collection, taming, type matchups, party battles, trading, or all of them.
4. **Overloading one pitch sentence.** A label stack should be precise, but not exhaustive. Put secondary layers in a follow-up sentence.
5. **Confusing player fantasy with genre.** "Become a monster trainer" is player fantasy; "monster-taming RPG" is genre/loop.
6. **Letting store categories dictate design taxonomy.** Store tags are useful for discoverability, but they may be too broad for product or design decisions.
7. **Ignoring local language nuance.** In Korean, "판타지" is often used broadly, but for design/research clarity it should usually be treated as 세계관/톤 rather than 장르.

## Verification Checklist

- [ ] The core repeated player action is named
- [ ] Setting and art tone are separated from genre
- [ ] Platform and service model are modifiers, not the whole label
- [ ] Comparison labels are translated into mechanics
- [ ] Misleading labels are explicitly corrected
- [ ] The final short label is understandable to a player
- [ ] The precise label is useful to a designer, researcher, or producer
- [ ] For Pokemon/Temtem-like games, creature collection or monster taming is foregrounded over fantasy
