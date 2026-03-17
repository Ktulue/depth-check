# depth-check

**Tiered code narration for humans in an AI-first world.**

depth-check is a Claude Skill that generates layered explanations of code changes at four expertise levels — making the same work understandable to everyone from stakeholders to senior engineers.

> 🎥 **Built live on stream** — Follow the entire build process on [Twitch/Ktulue](https://twitch.tv/ktulue) during Software Saturdays.  
> 🧪 **First Claude Skill** — This is my first custom skill for Claude, built from scratch and documented start to finish.

---

## The Problem

AI coding tools are optimized to *produce* code faster. Almost none of them are optimized to help humans *understand* code better. The few that offer explanations do it one-size-fits-all — a single level of detail regardless of who's reading.

## What depth-check Does

Given a code change (diff, commit, PR, or session summary), depth-check generates four tiers of explanation:

| Level | Audience | Example |
|-------|----------|---------|
| 🟢 **Green** | Stakeholders, PMs, non-technical | "We added a way for users to get notified when an item they want goes on sale." |
| 🔵 **Junior** | Early-career devs, bootcamp grads | "Created a React component that subscribes to a product's price via a REST API and sends a toast notification when it drops below the user's target." |
| 🟡 **Mid** | Working developers | "Implemented PriceWatchService with Redis pub/sub for real-time price events, a notification queue with retry logic, and user preference storage via PostgreSQL." |
| 🔴 **Senior** | Architects, tech leads | "Decoupled price monitoring into an event-driven microservice with fan-out via SNS/SQS, enabling horizontal scaling independent of the product catalog. Chose eventual consistency over strong consistency to keep P99 latency under 200ms." |

Same work. Four audiences. Automatically generated.

## Use Cases

- **Developer Onboarding** — New hires understand a codebase at their own level
- **Engineering Communication** — Auto-generate stakeholder-appropriate summaries of technical work for sprint reviews, board updates, and client changelogs
- **Code Review & PRs** — Tiered PR summaries help reviewers at different seniority levels understand changes faster
- **Education & Bootcamps** — Level-appropriate explanations for students at different comprehension levels
- **Streaming & Content Creation** — Make coding content accessible to mixed-skill audiences
- **Compliance & Audit** — Document what code does for non-technical auditors in regulated industries

## Roadmap

| Stage | Description | Status |
|-------|-------------|--------|
| 1. Claude Skill | `SKILL.md` — Claude reads it and follows narration rules | 🚧 In Progress |
| 2. MCP Server | Standalone TypeScript server for any MCP-compatible client | ⬜ Planned |
| 3. GitHub Action | Auto-generates tiered PR summaries on every pull request | ⬜ Planned |
| 4. API / SaaS | Hosted API with a dashboard for engineering teams | ⬜ Future |

## Stream Schedule

This project is being built live on [Twitch/Ktulue](https://twitch.tv/ktulue) as part of Software Saturdays:

1. **Architecture & Design** — Market research walkthrough, SKILL.md structure, tier design
2. **Build the Skill** — Implement with Claude Code, test against personal/public repos, iterate live
3. **MCP Server** — Convert to a standalone TypeScript MCP server, publish to npm
4. **GitHub Action** — PR integration, publish to GitHub Marketplace

## Project Structure

```
depth-check/
├── SKILL.md          # The Claude Skill definition
├── README.md
├── LICENSE
├── references/       # Supporting docs, tier examples, prompt patterns
└── (future)
    ├── mcp-server/   # TypeScript MCP server (Stage 2)
    └── action/       # GitHub Action (Stage 3)
```

## Usage (Stage 1 — Claude Skill)

Once the `SKILL.md` is complete, add the skill to your Claude environment and ask Claude to explain any code change:

> "Run depth-check on this diff"  
> "Give me a tiered summary of what we just built"  
> "Explain this PR at all four levels"

## Market Context

The AI coding tools market is projected to exceed $30B by 2032. Every major player (Cursor, Copilot, Devin, Sourcegraph) is focused on making AI produce code faster. Nobody is building the human-readable layer that helps different audiences understand the same work at their level. That's the gap. Full market analysis available in [`AI_Coding_Landscape_depth-check_Market_Map.md`](./AI_Coding_Landscape_depth-check_Market_Map.md).

## License

This project is licensed under the [GNU General Public License v3.0](./LICENSE).

## Support

☕ [Buy me a coffee on Ko-fi](https://ko-fi.com/ktulue)

## Author

**Ktulue** — [Twitch](https://twitch.tv/ktulue) · [GitHub](https://github.com/ktulue)

---

*Built with Claude. Streamed live. Explained for everyone.*
