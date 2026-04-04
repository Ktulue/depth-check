# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

DepthCheck is a Claude Skill that generates layered explanations of code changes at four expertise levels (Green/Junior/Mid/Senior). It makes the same work understandable to audiences ranging from non-technical stakeholders to senior architects.

**Current stage:** Stage 1 — Claude Skill (`SKILL.md`), implemented.

### Roadmap stages

1. **Claude Skill** — `SKILL.md` that Claude reads and follows narration rules (complete)
2. **MCP Server** — Standalone TypeScript server for any MCP-compatible client
3. **GitHub Action** — Auto-generates tiered PR summaries on every pull request
4. **API / SaaS** — Hosted API with a dashboard for engineering teams

## The Four Tiers

| Level | Audience | What it conveys |
|-------|----------|-----------------|
| 🟢 Green | Stakeholders, PMs, non-technical | Plain-language "what it does and why it matters" |
| 🔵 Junior | Early-career devs | Components, APIs, and patterns used |
| 🟡 Mid | Working developers | Services, infrastructure, data flow, and trade-offs |
| 🔴 Senior | Architects, tech leads | System design decisions, scaling implications, consistency models |

## Project Conventions

- Licensed under GPLv3.
- Built live on stream ([Twitch/Ktulue](https://twitch.tv/ktulue)) during Software Saturdays.
- Market analysis lives in `AI_Coding_Landscape_DepthCheck_Market_Map.md`.
- No proprietary code or employer/client architecture may be referenced — personal/public repos only.
