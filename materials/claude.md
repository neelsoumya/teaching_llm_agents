# Claude tools

- [Course webpage](https://learn.deeplearning.ai/courses/agent-skills-with-anthropic/lesson/bv2ekh/why-use-skills---part-i)

- Claude.ai/Claude Desktop, the Claude API, Claude Code, and the Claude Agent SDK

- [https://agentskills.io/home#adoption](https://agentskills.io/home#adoption)

- [material](https://github.com/https-deeplearning-ai/sc-agent-skills-files/tree/main)

## Skills

- [Lecture deeplearning.ai on skills](https://learn.deeplearning.ai/courses/agent-skills-with-anthropic/lesson/bv2ekh/why-use-skills---part-i)

- 📝 `SKILLS.md` File which should have the skills. This will have all the instructions to perform the tasks.

- `name` and `description` are required (YAML format)

- `references` folder should have file which is referenced in .md format

- put all these in another folder 📁 (named with the same name as the skill), zip it

- ⬆️📎 Upload this zipped file to _Claude_ > `capabilities` > `Skills`

- _Concept_ 🧩🚀 Skills are an open standard and are supported in `Claude`, `Gemini`, etc.

- [OpenAI SKILLS](https://developers.openai.com/cookbook/examples/skills_in_api)

- You want to keep system prompts slim. Put stable procedures in skills; keep system prompts for global behavior.

-  🧩🚀 Multiple agents or teams share the same _house style._ Skills are a nice `org standard library` pattern.

- Also good for reproducibility

- You want a reusable, independently versionable set of behaviours

- Consider pinning the model and skill version together for reproducible behavior across deployments.

- If the system prompt repeats the entire procedure, people will: Bypass skills and Stuff logic into tool schemas. And you lose the whole point (reusability + versioning + conditional invocation) of skills. Keep the system prompt content separate.

- Your workflow is highly conditional, or branches like a complex flow chart. Example: If X → do this; else if Y → do that; plus validation + retries.

- Skills are less ideal if it is a one-off task

- 🧩🚀  Skills are less ideal if you need live data side effects (that would be a `tool call`)

- [VibeSafe: reproducible prompts](https://github.com/lawrennd/vibesafe)

- Folder Structure for a Skill

A **skill** is just a folder bundle. A typical skill folder may contain:

```text
my-skill/
├── SKILL.md              # Required: main instruction file
├── scripts/              # Optional: code files
│   ├── example.py
│   └── example.js
├── helpers/              # Optional: helper modules and dependencies
│   └── requirements.txt
├── assets/               # Optional: images, data files, templates
│   ├── sample_input.json
│   └── template.md
└── README.md             # Optional: human-readable overview
```

- An example `SKILLS.md` file is here

```bash
---
name: academic-grant-writer
description: Transform Markdown notes (ideas, outlines, meeting notes) into a polished academic grant proposal in LaTeX with a corresponding BibTeX file.
version: 1.0
---

# Skill: Academic Grant Writing from Notes

## Purpose

Transform one or more Markdown inputs containing ideas, outlines, meeting notes, rough drafts, and reference fragments into a polished academic grant proposal written in LaTeX, with a matching BibTeX file.

## Input Format

The input directory may contain any of the following Markdown files:

- `ideas.md`
- `outline.md`
- `meeting-notes.md`
- `references.md`
- `draft.md`
- other `.md` files containing relevant project material

These files may be incomplete, repetitive, messy, or contradictory. Your job is to synthesize them into a coherent grant application.

## Output Format

Produce:

- `grant.tex` — the main LaTeX document
- `references.bib` — BibTeX entries for all cited sources
- optionally:
  - `sections/` for modular LaTeX files such as `sections/abstract.tex`, `sections/methods.tex`
  - `appendix.tex` if needed

The main output should be a clean, compile-ready LaTeX manuscript.

## Core Task

Use the Markdown notes to draft a grant proposal with the following qualities:

- clear research vision
- strong motivation and significance
- feasible work plan
- well-structured methodology
- explicit expected outcomes and impact
- academically polished language
- consistent terminology throughout

## Preferred Grant Structure

Unless the user specifies otherwise, use this structure:

1. Title  
2. Abstract  
3. Background and Motivation  
4. Research Questions / Aims  
5. Methodology / Work Packages  
6. Expected Contributions / Impact  
7. Timeline  
8. Risks and Mitigation  
9. References  

If the notes suggest a different funding format, adapt accordingly.

## Writing Rules

- Preserve the user’s intent and domain-specific terminology.
- Turn fragments into full academic prose.
- Do not invent claims, results, or citations.
- Flag uncertainty where the notes are ambiguous.
- Prefer precise, formal, grant-style language.
- Remove redundancy and combine repeated ideas.
- Keep the proposal internally consistent.
- Make the narrative persuasive but not overstated.

## Citation Rules

- Any factual claim that depends on external literature should be supported by a BibTeX entry.
- If a reference is mentioned in the notes but incomplete, do one of:
  - infer the likely citation only if highly confident, or
  - mark it clearly as `TODO` in the BibTeX file.
- Never fabricate publication details.
- Ensure every in-text citation key used in `grant.tex` exists in `references.bib`.

## LaTeX Rules

- Use standard, minimal LaTeX packages unless the grant format requires otherwise.
- Keep the document compile-ready.
- Prefer semantic structure:
  - `\section{}`
  - `\subsection{}`
  - `\paragraph{}`
- Use `\cite{}` for references.
- Avoid overcomplicated macros unless useful.
- If equations, tables, or figures are needed, include them only when supported by the notes.

## BibTeX Rules

- Extract all explicit references from the notes.
- Consolidate duplicate citations into one canonical entry.
- Use consistent BibTeX keys, for example:
  - `smith2022robustness`
  - `doe2021multiagent`
- If a citation is known only partially, keep the entry marked clearly for later completion.

## Workflow

1. Read all Markdown inputs.  
2. Identify:
   - project goal  
   - research problem  
   - contributions  
   - methods  
   - required references  
   - missing information  
3. Draft a concise but compelling grant narrative.  
4. Convert all bibliographic mentions into BibTeX entries.  
5. Write the final LaTeX and BibTeX outputs.  
6. Check consistency:
   - names  
   - acronyms  
   - citations  
   - section ordering  
   - terminology  
7. Ensure the output compiles cleanly.

## Style Guidance

Write in a tone that is:

- professional  
- precise  
- credible  
- concise  
- academically persuasive  

Avoid:

- hype  
- vague language  
- unsupported promises  
- repetitive phrasing  
- overlong sentences  

## Handling Incomplete Notes

When the notes are incomplete:

- infer structure from context  
- keep placeholders for unknown details  
- make assumptions explicit only when necessary  
- prefer conservative, defensible wording over guesswork  

Examples of acceptable placeholders:

- `[FUNDING SCHEME]`  
- `[PROJECT DURATION]`  
- `[NAME OF HOST INSTITUTION]`  
- `[REFERENCE NEEDED]`  

## Quality Checklist

Before finishing, verify:

- the proposal has a clear argument  
- the research questions are explicit  
- the work plan is feasible  
- citations match bibliography entries  
- the LaTeX is syntactically valid  
- no important note content was omitted  
- no unsupported claims were added  

## Output Expectations

The final deliverable should feel like a real grant draft, not a summary of notes.

When possible, prefer:

- full sentences over bullet lists  
- narrative synthesis over raw extraction  
- coherent sections over fragmented notes  
```


## Why use skills and how they work

- [Video by Anthropic](https://learn.deeplearning.ai/courses/agent-skills-with-anthropic/lesson/eg4sac/why-use-skills---part-ii)