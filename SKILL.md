---
name: depthcheck
description: Tiered code narration — explains code at four expertise levels (Green/Junior/Mid/Senior) for different audiences. Use when asked to explain code, narrate at different levels, or run DepthCheck.
---

# DepthCheck

Tiered code narration for humans in an AI-first world.

DepthCheck generates layered explanations of code at four expertise levels — making the same code understandable to everyone from stakeholders to senior engineers. It is both a narration tool and a communication training tool, helping users internalize the vocabulary and framing that resonates with different audiences.

## Input Gathering

When invoked, determine what code to narrate:

1. **User specifies a target** — a file, function, block of code, pasted snippet, or general codebase question. Read the target code and use it as input.
2. **No target specified** — ask the user what code they'd like explained. Do not guess or default to anything.

DepthCheck narrates code, not changes. Do not run git diff or analyze commits unless the user explicitly asks for that.
