# GitHub Copilot Workspace Instructions

## Project purpose

This repository is a teaching course for LLM Agents: practical labs, sample code, and guided exercises for building and evaluating agent architectures with modern LLM toolkits. It is mainly markdown, learning materials, and minimal sample code.

## Key files
- `README.md` — course overview and module roadmap
- `materials/` — course content (agents, tools, resources, quizzes, installation)
- `materials/claude.md` — model/skill-specific notes and exercise steps
- `materials/agents.md` — agent examples and sample code snippets

## What to do here
- Keep educational materials clear, concise, and reproducible for students.
- Prefer linking to authoritative external docs when possible ("Link, don’t embed").
- Keep code snippets runnable and match the environment in the course setup.
- Avoid adding non-teaching infrastructure or large binary assets.

## Development commands
- No build pipeline is defined in this course repository.
- Documentation edit flow: modify markdown, run local preview via any Markdown renderer.

## Agent-specific guidance
- If asked to create agents for exercises, base on course themes: open-source LLM SDKs, tool-assisted planning, retrieval augmentation, safety / guardrails.
- Avoid deviations into unrelated full-stack app scaffolding unless explicitly requested by an instructor.

## Conventions
- Use plain Markdown headings and code fences, minimal custom styling.
- Keep exercises in `materials/` and link from `README.md`.
- Add new core topic files in `materials/` and update the `README.md` table of contents.

## Troubleshooting
- If a user asks how to run code, direct them to course installation docs (e.g., `materials/installation.md`) and mention required Python / Node dependencies.

## Agent customization suggestions
- In this repo, refer to agent tasks as teaching exercises (e.g., "create a prompt tuning exercise for retrieval-augmented generation").
- For any new agent guidance, add to `materials/agents.md` and `materials/claude.md` for consistency.
