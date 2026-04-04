# DepthCheck v1 — Claude Skill Design Spec

**Date:** 2026-04-04
**Stage:** 1 — Claude Skill (`SKILL.md`)
**Status:** Approved

---

## Overview

DepthCheck is a Claude Skill that generates layered explanations of code at four expertise levels. It serves as both a narration tool and a communication training tool — helping users internalize the vocabulary and framing that resonates with different audiences.

## Invocation

- **Command:** `/depthcheck`
- **Trigger:** Explicit invocation only. The skill never auto-suggests or runs proactively.
- **Natural language discovery:** Claude's skill matching uses the `description` field in frontmatter, so phrases like "explain this at different levels" will surface the skill without extra configuration.

## Input Gathering

When invoked, Claude determines what code to narrate:

1. **User specifies a target** — a file, function, block of code, pasted snippet, or general codebase question. Claude uses that as input.
2. **No target specified** — Claude asks the user what they'd like explained.

No git diff logic, no commit analysis. DepthCheck narrates code, not changes. Diff-based narration is a future enhancement.

## Significance Assessment

Before generating narration, Claude assesses the scope of the code to calibrate depth:

- **Small** (a single function, a config value, a few lines) — each tier gets a single concise sentence.
- **Medium** (a file, a component, a class) — Green/Junior get a short paragraph. Mid/Senior get a paragraph with bullet points for technical details.
- **Large** (multiple files, a subsystem, a full codebase overview) — full treatment at every tier with structured detail at Mid/Senior.

Claude makes this judgment naturally from code size and complexity. No rigid word counts — guidance to match narration depth to what's being explained.

## Tier Definitions

All four tiers are always output, in order. Each tier is a genuinely different perspective, not a summary of another tier.

### 🟢 Green — Stakeholders, PMs, Non-Technical

- Plain language, no jargon
- Focuses on *what the code does and why it matters* to the product/business
- A non-technical person should understand every word
- Tone: clear, confident, conversational

### 🔵 Junior — Early-Career Devs, Bootcamp Grads

- Names the technologies, patterns, and components involved
- Explains *what the code does and how the pieces connect*
- Assumes basic programming knowledge but not deep domain expertise
- Tone: approachable, educational

### 🟡 Mid — Working Developers

- Describes implementation details, data flow, and design patterns
- Explains *how it works and why it was built this way*
- Can include bullet points for files, services, and key decisions
- Tone: peer-to-peer, practical

### 🔴 Senior — Architects & Tech Leads

- Focuses on system design, trade-offs, scaling implications, and architectural decisions
- Explains *what trade-offs were made and what the alternatives were*
- Can include bullet points for architectural concerns, performance, and maintainability
- Tone: strategic, concise, opinionated

## Output Format

Every invocation produces this structure:

```
## DepthCheck

🟢 **Green** — Stakeholders
[plain language paragraph]

🔵 **Junior** — Early-Career Devs
[approachable paragraph with tech names]

🟡 **Mid** — Working Developers
[implementation-focused paragraph]
- key detail bullets when warranted

🔴 **Senior** — Architects & Tech Leads
[strategic paragraph on trade-offs and design]
- architectural detail bullets when warranted
```

### Format Rules

- Always starts with `## DepthCheck` header
- All four tiers appear in order: Green → Junior → Mid → Senior
- Each tier has its emoji, bold label, and audience tag
- Bullet points only appear at Mid/Senior, and only when the code's complexity warrants it
- No tier references another tier's content — each stands alone
- Optimized for terminal rendering — no HTML, no collapsible blocks, clean markdown only

## Skill File Structure

Single `SKILL.md` with named sections:

1. **Frontmatter** — name, description
2. **Input Gathering** — how to determine what code to narrate
3. **Significance Assessment** — how to calibrate narration depth
4. **Tier Definitions** — voice, focus, and audience for each level
5. **Output Format** — the template and formatting rules

Sections may be split into separate files in the future if any section outgrows its space. Not expected for v1.

## Future Enhancements (Out of Scope for v1)

- Diff-based narration (uncommitted changes, last commit, commit ranges)
- PR narration via `gh` CLI
- Single-tier invocation flag (e.g., `/depthcheck green`)
- Auto-suggest after significant code changes
- MCP server (Stage 2)
- GitHub Action (Stage 3)
