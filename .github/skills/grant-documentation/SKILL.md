---
name: grant-documentation
description: "Create grant proposal text in LaTeX with bibliography support, plus meeting notes and outlines in Markdown and plain text."
---

# Grant Documentation Skill

## Use when

- you need a grant proposal or funding request written in LaTeX
- you want a matching `.bib` bibliography file for citations
- you want structured meeting notes, agendas, and outlines in `.md` and `.txt`

## What this skill produces

- one or more LaTeX source files (`.latex`) for the grant narrative, budget, and supporting material
- a `.bib` file containing bibliographic references
- meeting notes and action-item summaries in Markdown (`.md`)
- plain-text outlines and notes in `.txt`

## Workflow

1. Collect the grant context:
   - funding agency or sponsor
   - proposal title and project name
   - project summary, goals, impact, methodology, and schedule
   - budget highlights and team roles
   - deadlines, submission format, and audience
2. Generate the LaTeX grant document:
   - structure sections clearly (e.g. summary, background, aims, approach, budget, timeline)
   - use LaTeX formatting conventions, labels, and section commands
   - provide a concise bibliography section and export matching `.bib` entries
3. Produce notes and outlines:
   - create meeting notes with date, participants, decisions, and action items
   - create an agenda or outline in Markdown and a plain-text version
   - include headers, bullet lists, and clear next steps
4. Offer file suggestions:
   - grant proposal file names (e.g. `proposal.latex`, `proposal.bib`)
   - meeting notes file names (e.g. `meeting-notes.md`, `meeting-outline.txt`)

## Quality criteria

- LaTeX content should compile cleanly and use standard document structure
- `.bib` entries should be valid BibTeX records
- Markdown notes should use headings and lists for readability
- Plain-text outlines should remain readable and easy to edit

## Example prompts

- "Generate a grant proposal in LaTeX for an education research project, including a `.bib` file and meeting notes in Markdown and text."
- "Create a project outline, LaTeX grant narrative, and supporting `.bib` file for an NSF-style application."
- "Write meeting notes, agenda, and grant proposal content with separate `.md` and `.txt` outputs."


## Writing Rules

- Preserve the user’s intent and domain-specific terminology.
- Turn fragments into full academic prose.
- Do not invent claims, results, or citations.
- Flag uncertainty where the notes are ambiguous.
- Prefer precise, formal, grant-style language.
- Remove redundancy and combine repeated ideas.
- Double-Check and verify references and ensure thay they exist
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
- Use `\cite{}` for references and `natbib` package.
- Avoid overcomplicated macros unless useful.
- If equations, tables, or figures are needed, include them only when supported by the notes.

## BibTeX Rules

- Extract all explicit references from the notes.
- Consolidate duplicate citations into one canonical entry.
- Use consistent BibTeX keys, for example:
  - `smith2022robustness`
  - `doe2021multiagent`
- If a citation is known only partially, keep the entry marked clearly for later completion.

## Preferred Grant Structure

Unless the user specifies otherwise, use this structure:

1. Title  
2. Abstract  
3. Background and Motivation  
4. Research Questions / Aims  
5. Methodology / Work Packages  
6. Expected Contributions / Impact  
7. Ethics and responsible research innovation (RRI) - this section will contain additional questions to collect information about specific ethical considerations relating to research involving animals, human participants and genetically modified organisms, project partners and facility access requests. 
8. Timeline  
9. Risks and Mitigation  
10. References  

If the notes suggest a different funding format, adapt accordingly.

## Writing Rules

- Preserve the user’s intent and domain-specific terminology.
- Turn fragments into full academic prose.
- Do not invent claims, results, or citations.
- Flag uncertainty where the notes are ambiguous.
- Prefer precise, formal, grant-style language.
- Remove redundancy and combine repeated ideas.
- Double-Check and verify references and ensure thay they exist
- Keep the proposal internally consistent.
- Make the narrative persuasive but not overstated.

## Citation Rules

- Any factual claim that depends on external literature should be supported by a BibTeX entry.
- If a reference is mentioned in the notes but incomplete, do one of:
  - infer the likely citation only if highly confident, or
  - mark it clearly as `TODO` in the BibTeX file.
- Never fabricate publication details.
- Ensure every in-text citation key used in `grant.tex` exists in `references.bib`.

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
- endashes


## Output Expectations

The final deliverable should feel like a real grant draft, not a summary of notes.

I prefer the following:

- full sentences over bullet lists  
- narrative synthesis over raw extraction  
- coherent sections over fragmented notes  
- no endashes
