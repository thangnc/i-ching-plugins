# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Claude Code plugin** (not a traditional software project) providing Vietnamese I Ching divination (Lục Hào Bát Quái) capabilities. It has no build step, no tests, and no runtime — it is a collection of Markdown-based instruction files consumed by the Claude plugin system.

## Plugin Structure

```
.claude-plugin/
  plugin.json       # Plugin metadata and entry points
  marketplace.json  # Marketplace listing info
commands/
  gieo-que.md       # Slash command: /gieo-que
  luan-giai.md      # Slash command: /luan-giai
skills/
  gieo-que/SKILL.md   # Auto-trigger skill for casting hexagrams
  luan-giai/SKILL.md  # Auto-trigger skill for interpreting hexagrams
```

## Plugin Architecture

The plugin has two entry-point types:

- **`commands/`** — Detailed instruction sets invoked explicitly via `/gieo-que` and `/luan-giai` slash commands. These hold the full divination logic.
- **`skills/`** — Lightweight natural-language recognizers that auto-trigger on contextual keywords. Skills detect intent from conversational input and then execute the detailed logic in `commands/`.

| | Commands | Skills |
|---|---|---|
| **Activation** | User types `/gieo-que` or `/luan-giai` | Claude detects natural language ("gieo quẻ cho tôi") |
| **Role** | Full detailed instructions | Trigger recognizer → delegates to commands |

**Usage flows:**
```
/gieo-que + info  →  /luan-giai          # Explicit command flow
"Gieo quẻ cho tôi..."  →  "Giải quẻ"    # Natural language (skills auto-trigger)
/luan-giai + manual hexagram data        # Interpret an existing hexagram
```

## Skill Front Matter Format

```yaml
---
name: skill-name
description: >
  Trigger description including keywords that activate this skill.
---
```

## Command Format

```yaml
---
description: Short description
---

# Title

1. Step one
2. Step two
...
```

## Domain Knowledge

This plugin implements traditional Vietnamese I Ching divination:

- **gieo-que** (Cast hexagram): Collects user info (name, birthdate, sex, question), calculates the Four Pillars (Tứ Trụ), derives Upper/Lower trigrams using Mai Hoa numerology, assigns Nạp Giáp, Lục Thân (Six Relatives), Thế/Ứng positions, and Lục Thần (Six Spirits).
- **luan-giai** (Interpret hexagram): Takes a cast hexagram and interprets it by identifying Dụng Thần (useful god), analyzing Nguyệt kiến/Nhật thần influence, evaluating moving lines, Thế-Ứng relationship, and concluding with fortune, timing, and advice.

The two skills are designed to chain: `gieo-que` casts a hexagram, then offers to invoke `luan-giai` for interpretation.

## Installation

Copy the plugin directory into `.claude/plugins/` or install via the Claude marketplace.

## What to Edit

When modifying this plugin:
- **Divination logic or tables** → edit `commands/gieo-que.md` or `commands/luan-giai.md` (detailed logic lives here)
- **Natural language trigger keywords** → edit the `description` front matter in `skills/gieo-que/SKILL.md` or `skills/luan-giai/SKILL.md`
- **Plugin metadata, versioning, keywords** → edit `.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json` (keep them in sync)
- **All content is in Vietnamese** — maintain Vietnamese language and Hán-Việt terminology conventions throughout