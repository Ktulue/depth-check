# depthcheck

**Tiered code narration for humans in an AI-first world.**

depthcheck is a Claude Skill that generates layered explanations of code changes at four expertise levels — making the same work understandable to everyone from stakeholders to senior engineers.

> Built live on stream at [Twitch/Ktulue](https://twitch.tv/ktulue) during Software Saturdays 04.04.26.

---

## The Problem

AI coding tools are optimized to *produce* code faster. Almost none of them are optimized to help humans *understand* code better. The few that offer explanations do it one-size-fits-all — a single level of detail regardless of who's reading.

## What depthcheck Does

Given a code change (diff, commit, PR, or session summary), depthcheck generates four tiers of explanation:

| Level | Audience | Example |
|-------|----------|---------|
| **Green** | Stakeholders, PMs, non-technical | "We added a way for users to get notified when an item they want goes on sale." |
| **Junior** | Early-career devs, bootcamp grads | "Created a React component that subscribes to a product's price via a REST API and sends a toast notification when it drops below the user's target." |
| **Mid** | Working developers | "Implemented PriceWatchService with Redis pub/sub for real-time price events, a notification queue with retry logic, and user preference storage via PostgreSQL." |
| **Senior** | Architects, tech leads | "Decoupled price monitoring into an event-driven microservice with fan-out via SNS/SQS, enabling horizontal scaling independent of the product catalog. Chose eventual consistency over strong consistency to keep P99 latency under 200ms." |

Same work. Four audiences. Automatically generated.

## Why It Matters

depthcheck isn't just a narration tool — it's a communication framework. Engineers who can explain the same work to a PM, a junior dev, and an architect are rare and valuable. depthcheck teaches that skill by example, showing what audience-appropriate vocabulary looks like at each level.

## Use Cases

- **Developer Onboarding** — New hires understand a codebase at their own level
- **Engineering Communication** — Auto-generate stakeholder-appropriate summaries for sprint reviews, board updates, and client changelogs
- **Code Review & PRs** — Tiered PR summaries help reviewers at different seniority levels understand changes faster
- **Education & Bootcamps** — Level-appropriate explanations for students at different comprehension levels
- **Streaming & Content Creation** — Make coding content accessible to mixed-skill audiences
- **Compliance & Audit** — Document what code does for non-technical auditors in regulated industries

## Getting Started

### Prerequisites

- [Claude Code](https://claude.ai/code) CLI or any Claude environment that supports skills

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/ktulue/depthcheck.git
   ```

2. Add `SKILL.md` to your Claude environment as a skill.

3. Ask Claude to explain any code change:
   ```
   /depthcheck
   "Run depthcheck on this diff"
   "Give me a tiered summary of what we just built"
   "Explain this PR at all four levels"
   ```

### Invocation

depthcheck can be invoked as a slash command (`/depthcheck`) or by asking Claude directly. It accepts optional arguments:

| Argument | Description |
|----------|-------------|
| `--hierarchical` | Top-down narration (Green first, then deeper) |
| `--reverse` | Bottom-up narration (Senior first, then simpler) |
| `--only <tier>` | Generate only one tier (e.g., `--only green`) |
| *(no args)* | Generates all four tiers, Green through Senior |

## Roadmap

| Stage | Description | Status |
|-------|-------------|--------|
| 1. Claude Skill | `SKILL.md` — Claude reads it and follows narration rules | Complete |
| 2. MCP Server | Standalone TypeScript server for any MCP-compatible client | Planned |
| 3. GitHub Action | Auto-generates tiered PR summaries on every pull request | Planned |
| 4. API / SaaS | Hosted API with a dashboard for engineering teams | Future |

## Project Structure

```
depthcheck/
├── SKILL.md          # The Claude Skill definition (Stage 1)
├── CLAUDE.md         # Project instructions for Claude Code
├── README.md
├── LICENSE           # MIT License
├── AI_Coding_Landscape_depthcheck_Market_Map.md
└── docs/
    └── superpowers/  # Brainstorming specs and implementation plans
```

## Market Context

The AI coding tools market is projected to exceed $30B by 2032. Every major player (Cursor, Copilot, Devin, Sourcegraph) is focused on making AI produce code faster. Nobody is building the human-readable layer that helps different audiences understand the same work at their level. That's the gap. Full market analysis available in [`AI_Coding_Landscape_depthcheck_Market_Map.md`](./AI_Coding_Landscape_depthcheck_Market_Map.md).

## Contributing

Contributions are welcome. Please open an issue first to discuss what you'd like to change.

## License

This project is licensed under the [MIT License](./LICENSE).

---

## Support

☕ [Buy me a coffee on Ko-fi](http://ko-fi.com/ktulue)

Created by Ktulue | The Water Father 🌊
