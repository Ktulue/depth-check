---
name: depthcheck
description: Tiered code narration — explains code at four expertise levels (Green/Junior/Mid/Senior) for different audiences. Use when asked to explain code, narrate at different levels, or run DepthCheck.
user-invokable: true
args:
  - name: target
    description: The code to explain — a file path, function name, pasted snippet, or general description (optional, will ask if not provided)
    required: false
---

# DepthCheck

Tiered code narration for humans in an AI-first world.

DepthCheck generates layered explanations of code at four expertise levels — making the same code understandable to everyone from stakeholders to senior engineers. It is both a narration tool and a communication training tool, helping users internalize the vocabulary and framing that resonates with different audiences.

## Input Gathering

When invoked, determine what code to narrate:

1. **User specifies a target** — a file, function, block of code, pasted snippet, or general codebase question. Read the target code and use it as input.
2. **No target specified** — ask the user what code they'd like explained. Do not guess or default to anything.

DepthCheck narrates code, not changes. Do not run git diff or analyze commits unless the user explicitly asks for that.

## Significance Assessment

Before generating narration, assess the scope of the code to calibrate narration depth:

- **Small** (a single function, a config value, a few lines) — each tier gets a single concise sentence.
- **Medium** (a file, a component, a class) — Green and Junior get a short paragraph. Mid and Senior get a paragraph with bullet points for technical details.
- **Large** (multiple files, a subsystem, a full codebase overview) — full treatment at every tier. Mid and Senior include structured bullet points for files, patterns, trade-offs, and architectural concerns.

Match narration depth to what is being explained. No rigid word counts. A trivial piece of code should not receive an architectural essay. A complex subsystem should not be reduced to a sentence.

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

## Output Format

Every invocation produces this structure:

````
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
````

### Format Rules

- Always start output with the `## DepthCheck` header.
- Always output all four tiers in this exact order: Green, Junior, Mid, Senior.
- Each tier line uses the emoji, bold label, and audience tag exactly as shown above.
- Bullet points only appear at Mid and Senior tiers, and only when the code's complexity warrants them.
- No tier may reference another tier's content. Each tier stands completely alone.
- Use clean markdown only. No HTML tags, no collapsible blocks, no `<details>` elements. Output must render cleanly in a terminal.
