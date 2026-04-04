# DepthCheck SKILL.md Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create the `SKILL.md` file that defines the DepthCheck Claude Skill — tiered code narration at four expertise levels.

**Architecture:** Single markdown file with YAML frontmatter and five named sections. The skill instructs Claude how to gather input, assess significance, and produce four-tier narration output optimized for terminal rendering.

**Tech Stack:** Markdown, YAML frontmatter (Claude Skills format)

**Spec:** `docs/superpowers/specs/2026-04-04-depthcheck-skill-design.md`

---

### Task 1: Create SKILL.md with Frontmatter

**Files:**
- Create: `SKILL.md`

- [ ] **Step 1: Create SKILL.md with frontmatter and skill purpose**

```markdown
---
name: depthcheck
description: Tiered code narration — explains code at four expertise levels (Green/Junior/Mid/Senior) for different audiences. Use when asked to explain code, narrate at different levels, or run DepthCheck.
---

# DepthCheck

Tiered code narration for humans in an AI-first world.

DepthCheck generates layered explanations of code at four expertise levels — making the same code understandable to everyone from stakeholders to senior engineers. It is both a narration tool and a communication training tool, helping users internalize the vocabulary and framing that resonates with different audiences.
```

- [ ] **Step 2: Commit**

```bash
git add SKILL.md
git commit -m "feat: create SKILL.md with frontmatter and purpose"
```

---

### Task 2: Add Input Gathering Section

**Files:**
- Modify: `SKILL.md`

- [ ] **Step 1: Add input gathering section after the purpose paragraph**

Append to `SKILL.md`:

```markdown
## Input Gathering

When invoked, determine what code to narrate:

1. **User specifies a target** — a file, function, block of code, pasted snippet, or general codebase question. Read the target code and use it as input.
2. **No target specified** — ask the user what code they'd like explained. Do not guess or default to anything.

DepthCheck narrates code, not changes. Do not run git diff or analyze commits unless the user explicitly asks for that.
```

- [ ] **Step 2: Commit**

```bash
git add SKILL.md
git commit -m "feat: add input gathering section to SKILL.md"
```

---

### Task 3: Add Significance Assessment Section

**Files:**
- Modify: `SKILL.md`

- [ ] **Step 1: Add significance assessment section after input gathering**

Append to `SKILL.md`:

```markdown
## Significance Assessment

Before generating narration, assess the scope of the code to calibrate narration depth:

- **Small** (a single function, a config value, a few lines) — each tier gets a single concise sentence.
- **Medium** (a file, a component, a class) — Green and Junior get a short paragraph. Mid and Senior get a paragraph with bullet points for technical details.
- **Large** (multiple files, a subsystem, a full codebase overview) — full treatment at every tier. Mid and Senior include structured bullet points for files, patterns, trade-offs, and architectural concerns.

Match narration depth to what is being explained. No rigid word counts. A trivial piece of code should not receive an architectural essay. A complex subsystem should not be reduced to a sentence.
```

- [ ] **Step 2: Commit**

```bash
git add SKILL.md
git commit -m "feat: add significance assessment section to SKILL.md"
```

---

### Task 4: Add Tier Definitions Section

**Files:**
- Modify: `SKILL.md`

- [ ] **Step 1: Add all four tier definitions after significance assessment**

Append to `SKILL.md`:

```markdown
## Tier Definitions

Always output all four tiers, in order. Each tier is a genuinely different perspective written for a different reader — not a shorter or longer summary of the same explanation. Use vocabulary and framing natural to each audience.

### 🟢 Green — Stakeholders, PMs, Non-Technical

- Plain language, zero jargon. If a non-technical person would need to look up a word, rephrase it.
- Focus on *what the code does and why it matters* to the product or business.
- Tone: clear, confident, conversational.
- Example framing: "This is the part of the system that handles..." / "This lets users..."

### 🔵 Junior — Early-Career Devs, Bootcamp Grads

- Name the technologies, patterns, and components involved.
- Explain *what the code does and how the pieces connect*.
- Assume basic programming knowledge (variables, functions, classes) but not deep domain expertise.
- Tone: approachable, educational. Treat the reader as capable but new.
- Example framing: "This is a React component that..." / "This function takes X and returns Y by..."

### 🟡 Mid — Working Developers

- Describe implementation details, data flow, and design patterns.
- Explain *how it works and why it was built this way*.
- Include bullet points for files, services, and key decisions when the code's complexity warrants it.
- Tone: peer-to-peer, practical. No hand-holding, no over-explaining.
- Example framing: "Uses the repository pattern to..." / "Event-driven via pub/sub so that..."

### 🔴 Senior — Architects & Tech Leads

- Focus on system design, trade-offs, scaling implications, and architectural decisions.
- Explain *what trade-offs were made and what the alternatives were*.
- Include bullet points for architectural concerns, performance characteristics, and maintainability when warranted.
- Tone: strategic, concise, opinionated. Assume deep technical expertise.
- Example framing: "Chose eventual consistency over strong consistency to..." / "This decouples X from Y, enabling..."
```

- [ ] **Step 2: Commit**

```bash
git add SKILL.md
git commit -m "feat: add four tier definitions to SKILL.md"
```

---

### Task 5: Add Output Format Section

**Files:**
- Modify: `SKILL.md`

- [ ] **Step 1: Add output format and rules after tier definitions**

Append to `SKILL.md`:

```markdown
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

- Always start output with the `## DepthCheck` header.
- Always output all four tiers in this exact order: Green, Junior, Mid, Senior.
- Each tier line uses the emoji, bold label, and audience tag exactly as shown above.
- Bullet points only appear at Mid and Senior tiers, and only when the code's complexity warrants them.
- No tier may reference another tier's content. Each tier stands completely alone.
- Use clean markdown only. No HTML tags, no collapsible blocks, no `<details>` elements. Output must render cleanly in a terminal.
```

Note: The inner code fence uses triple backticks. To nest it inside the SKILL.md, use a different fence delimiter (four backticks) for the outer block, or indent the inner block. The implementer should ensure the markdown renders correctly — the template example should appear as a literal code block in the skill file.

- [ ] **Step 2: Verify the complete SKILL.md renders correctly**

Read the full `SKILL.md` from top to bottom. Check:
- Frontmatter parses correctly (name, description)
- All five sections are present in order
- The output format template appears as a code block, not rendered markdown
- No broken markdown syntax

- [ ] **Step 3: Commit**

```bash
git add SKILL.md
git commit -m "feat: add output format section, completing SKILL.md v1"
```

---

### Task 6: Update CLAUDE.md

**Files:**
- Modify: `CLAUDE.md`

- [ ] **Step 1: Update CLAUDE.md to reflect that Stage 1 is complete**

Change the "Current stage" line from:

```
**Current stage:** Stage 1 — Claude Skill (`SKILL.md`), not yet implemented.
```

To:

```
**Current stage:** Stage 1 — Claude Skill (`SKILL.md`), implemented.
```

- [ ] **Step 2: Commit**

```bash
git add CLAUDE.md
git commit -m "maint: update CLAUDE.md to reflect SKILL.md completion"
```
