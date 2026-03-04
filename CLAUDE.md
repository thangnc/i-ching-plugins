# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Claude Code plugin monorepo** (not a traditional software project) hosting Vietnamese I Ching divination (Lục Hào Bát Quái) plugins. It has no build step, no tests, and no runtime — it is a collection of Markdown-based instruction files consumed by the Claude plugin system. Plugins live under `plugins/<plugin-name>/`; the marketplace listing is at `.claude-plugin/marketplace.json`.

## Plugin Structure

```
.claude-plugin/
  marketplace.json                  # Marketplace listing (repo-level)
plugins/
  luc-hao/
    .claude-plugin/
      plugin.json                   # Plugin metadata and entry points
    commands/
      gieo-que.md                   # Slash command: /gieo-que (concise prompt + output format)
      luan-giai.md                  # Slash command: /luan-giai (concise prompt + output format)
    skills/
      gieo-que/
        SKILL.md                        # Auto-trigger recognizer
        references/bang-tra-cuu.md      # Lookup tables (Nạp Giáp, Nạp Chi, 64 hexagrams, Nạp Âm, etc.)
      luan-giai/
        SKILL.md                        # Auto-trigger recognizer
        references/quy-tac-luan-giai.md # Interpretation rules (Dụng Thần, Vượng Suy, special cases, etc.)
```

## Plugin Architecture

Three-tier design:

1. **`plugins/luc-hao/skills/*/SKILL.md`** — Natural-language trigger recognizers. Auto-activate on keywords ("gieo quẻ", "luận giải"...). Lightweight — delegate execution to commands and reference files.
2. **`plugins/luc-hao/commands/*.md`** — Concise prompts with `$ARGUMENTS` and fixed output format. Instruct Claude to answer directly without explaining theory.
3. **`plugins/luc-hao/skills/*/references/*.md`** — Static lookup tables and rule sets. Referenced via `${CLAUDE_PLUGIN_ROOT}/skills/.../references/...` inside SKILL.md.

| | Skills | Commands | References |
|---|---|---|---|
| **Role** | Trigger recognizer | Concise execution prompt | Data tables & rules |
| **Activation** | Natural language | `/gieo-que`, `/luan-giai` | Loaded by skills/commands |

**Usage flows:**
```
/gieo-que + info  →  /luan-giai          # Explicit command flow
"Gieo quẻ cho tôi..."  →  "Giải quẻ"    # Natural language (skills auto-trigger)
/luan-giai + manual hexagram data        # Interpret an existing hexagram
```

## File Formats

**Skill front matter:**
```yaml
---
name: skill-name
description: Trigger description with keywords that activate this skill.
---
```

**Command format** — concise prompt using `$ARGUMENTS`, direct output instructions, fixed emoji-prefixed sections.

## Domain Knowledge

This plugin implements traditional Vietnamese I Ching divination:

- **gieo-que** (Cast hexagram): Collects user info (name, birthdate, sex, question), calculates the Four Pillars (Tứ Trụ), derives Upper/Lower trigrams using Mai Hoa numerology, assigns Nạp Giáp, Lục Thân (Six Relatives), Thế/Ứng positions, and Lục Thần (Six Spirits).
- **luan-giai** (Interpret hexagram): Takes a cast hexagram and interprets it by identifying Dụng Thần (useful god), analyzing Nguyệt kiến/Nhật thần influence, evaluating moving lines, Thế-Ứng relationship, and concluding with fortune, timing, and advice.

The two skills are designed to chain: `gieo-que` casts a hexagram, then offers to invoke `luan-giai` for interpretation.

## Installation

Copy the plugin directory into `.claude/plugins/` or install via the Claude marketplace.

## What to Edit

When modifying this plugin:
- **Lookup tables** (Nạp Giáp, Nạp Chi, 64 hexagrams, Nạp Âm, etc.) → `plugins/luc-hao/skills/gieo-que/references/bang-tra-cuu.md`
- **Interpretation rules** (Dụng Thần, Vượng Suy, special cases, priority order) → `plugins/luc-hao/skills/luan-giai/references/quy-tac-luan-giai.md`
- **Output format or prompt behavior** → `plugins/luc-hao/commands/gieo-que.md` or `plugins/luc-hao/commands/luan-giai.md`
- **Natural language trigger keywords** → `description` front matter in `plugins/luc-hao/skills/*/SKILL.md`
- **Plugin metadata, versioning** → `plugins/luc-hao/.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json` (keep in sync)
- **All content is in Vietnamese** — maintain Vietnamese language and Hán-Việt terminology conventions throughout