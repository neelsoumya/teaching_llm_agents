---
name: academic-manuscript-writer
description: Transform academic notes, outlines, drafts, or bullet points into a polished academic manuscript in LaTeX, Word (.docx), or Markdown. Use this skill whenever the user wants to turn rough notes, meeting notes, ideas, or partial drafts into a full academic paper, journal article, conference paper, thesis chapter, or literature review. Trigger this skill when the user says things like "turn my notes into a paper", "write this up properly", "polish my draft", "make this into a manuscript", "academic write-up", "journal-ready", or similar. The skill enforces strict hallucination prevention, no en dashes or em dashes, semiformal academic language, and mandatory reference verification.
version: 1.0
---

# Skill: Academic Manuscript Writer

## Purpose

Transform one or more inputs (notes, outlines, bullet points, rough drafts, meeting notes, reference fragments) into a polished, publication-ready academic manuscript in the user's chosen output format: LaTeX, Word (.docx), or Markdown.

## Output Formats

Ask the user which format they want if they have not specified:

- **LaTeX** — produces `manuscript.tex` + `references.bib` (compile-ready)
- **Word (.docx)** — produces a formatted Word document via the `docx` skill
- **Markdown** — produces a clean `manuscript.md` with inline citations

If the user does not specify, default to **Markdown** for simplicity and ask if they want another format.

---

## Hallucination Prevention (Critical)

This is the most important constraint. Follow it without exception.

### What you must never do

- Never invent a fact, statistic, result, or claim not present in the user's notes.
- Never fabricate a reference, author name, journal, volume, page number, DOI, or year.
- Never infer that a study "found X" unless the notes explicitly state it.
- Never fill a gap in the argument with a plausible-sounding but unverified claim.
- Never silently complete a partial reference by guessing the missing fields.

### What to do instead

- Use explicit placeholders for missing information. See the Placeholder section below.
- Flag gaps clearly in a `## Flags for Author Review` section at the end of the manuscript.
- If a reference appears in the notes but is incomplete, keep the partial entry and mark it `[VERIFY]` in the bibliography.
- If a claim needs a citation but none is in the notes, write `[CITATION NEEDED]` inline.

### Placeholder conventions

Use square-bracket placeholders consistently throughout:

| Placeholder | Use case |
|---|---|
| `[AUTHOR NAME]` | Missing author |
| `[YEAR]` | Missing publication year |
| `[JOURNAL NAME]` | Missing journal or venue |
| `[VOLUME/ISSUE/PAGES]` | Missing bibliographic detail |
| `[INSTITUTION]` | Missing affiliation |
| `[DOI]` | Missing DOI |
| `[CITATION NEEDED]` | Claim requires a reference not in the notes |
| `[CLARIFY: ...]` | Ambiguous passage that the author should resolve |
| `[DATA NEEDED]` | Claim requires data or results not in the notes |

---

## Reference Verification Protocol

References are the highest-risk area for hallucination. Follow this protocol strictly.

### Step 1: Collect all references from the notes

Extract every bibliographic mention, however partial. This includes:

- Full citations
- Author-year pairs (e.g., "Smith et al., 2019")
- Titles mentioned in passing
- URLs or DOIs

### Step 2: Classify each reference

For each reference, classify it as one of:

- **Complete** — all key fields present (authors, year, title, venue/journal, volume/pages or DOI). Mark as ready.
- **Partial** — some fields missing. Keep what is known; mark missing fields with the appropriate placeholder; flag with `[VERIFY]`.
- **Named only** — only an author-year pair or a title fragment. Create a stub entry; mark all fields `[UNKNOWN]`; flag with `[VERIFY]`.
- **Implied** — a factual claim clearly needs a citation but no reference is mentioned at all. Insert `[CITATION NEEDED]` inline; do not create a bibliography entry.

### Step 3: Never guess

Do not attempt to reconstruct a reference by memory or inference. If you are not certain a field is correct from the notes, use the appropriate placeholder.

### Step 4: Produce the bibliography

- LaTeX: produce a `.bib` file; use consistent keys such as `smith2019robustness`.
- Word/Markdown: produce a formatted References section at the end.
- Consolidate duplicate references into one canonical entry.
- Ensure every in-text citation key matches a bibliography entry.

### Step 5: Add a verification note

At the end of the manuscript (in a clearly marked section not for publication), list every reference marked `[VERIFY]` and every `[CITATION NEEDED]`, so the author knows exactly what to check before submission.

---

## Punctuation Rules (Non-Negotiable)

- **No en dashes (--) anywhere in the manuscript.** Replace with a comma, a colon, a semicolon, or rephrase the sentence.
- **No em dashes either.** Replace with a comma, parentheses, or a colon.
- Use a hyphen only for compound adjectives (e.g., "well-established").
- Use serial commas (Oxford commas) throughout.
- Use only standard quotation marks appropriate to the output format.

---

## Language and Tone

The manuscript should be written in **semiformal academic English**:

- Clear, precise, and direct.
- Professional but not stiff or jargon-heavy.
- Full sentences; no bullet points in the body text (unless the user's discipline uses them, e.g., certain CS papers).
- Active voice preferred where it does not read as informal.
- Passive voice acceptable for methods sections.
- Consistent terminology throughout: once you choose a term for a concept, use it everywhere.
- Avoid: hedges stacked on hedges, verbose throat-clearing, vague nouns ("this study explores the interesting phenomenon of...").
- Avoid: hype, overclaiming, unsupported superlatives.

---

## Default Manuscript Structure

Use this structure unless the user specifies otherwise or the discipline clearly calls for a different format:

1. Title
2. Abstract (150 to 250 words)
3. Introduction
4. Background / Related Work / Literature Review
5. Methods / Methodology
6. Results / Findings
7. Discussion
8. Conclusion
9. Acknowledgements (placeholder if not provided)
10. References
11. Appendices (if needed)

Adapt the structure to the discipline:

- **Sciences / medicine**: IMRaD (Introduction, Methods, Results, Discussion) is standard.
- **Humanities**: May omit Methods; expand Discussion and close reading sections.
- **Computer science**: May have a System Design or Implementation section.
- **Social sciences**: Often combines Results and Discussion.

If unsure of the discipline, infer from the notes and state your assumption.

---

## Workflow

Follow these steps in order.

### 1. Read and parse all inputs

Read every file or passage provided. Identify:

- The core argument or thesis
- The research question(s) or objective(s)
- Key claims and findings
- Methods described
- References and citations
- Gaps, ambiguities, and contradictions

### 2. Clarify before writing (if needed)

If the notes are too incomplete to produce a coherent manuscript, ask the user for the minimum necessary information before proceeding. Do not pad a thin manuscript with invented content.

### 3. Draft the manuscript

Write the full manuscript following the structure and language rules above. Synthesise the notes into coherent prose. Do not simply reorder the user's bullet points.

### 4. Handle references

Apply the Reference Verification Protocol above.

### 5. Apply the quality checklist

Before delivering, verify every item in the Quality Checklist below.

### 6. Produce the output

Deliver the manuscript in the requested format. If LaTeX is requested, also read the `docx` skill if the user later wants a Word version (both can coexist). If `.docx` is requested, consult the `docx` skill at `/mnt/skills/public/docx/SKILL.md` before producing the file.

---

## Quality Checklist

Before finalising the manuscript, verify every item:

**Content**
- [ ] The central argument is clear and consistently maintained.
- [ ] Every factual claim is either supported by a note-provided reference or marked `[CITATION NEEDED]`.
- [ ] No claim, result, or statistic has been invented.
- [ ] Gaps and ambiguities are flagged, not silently papered over.
- [ ] Terminology is consistent throughout.

**References**
- [ ] Every in-text citation has a corresponding bibliography entry.
- [ ] Every bibliography entry uses the correct field placeholders for missing data.
- [ ] All `[VERIFY]` references are listed in the author review flags section.
- [ ] No reference has been fabricated or reconstructed by inference.

**Language and style**
- [ ] No en dashes anywhere.
- [ ] No em dashes anywhere.
- [ ] Oxford commas used throughout.
- [ ] No bullet points in body prose (unless discipline-appropriate).
- [ ] Tone is semiformal and consistent.
- [ ] No hype, overclaiming, or vague padding.

**Format**
- [ ] Structure follows the agreed or default manuscript format.
- [ ] Abstract is within the word limit (or flagged if a limit was not specified).
- [ ] LaTeX compiles cleanly (if applicable).
- [ ] Word document uses proper heading styles (if applicable).

---

## Format-Specific Rules

### LaTeX

- Use `\documentclass{article}` unless the user specifies a journal class.
- Use `natbib` with `\bibliographystyle{plainnat}` as the default citation style.
- Use `\cite{}` and `\citep{}` / `\citet{}` appropriately.
- Use semantic structure: `\section{}`, `\subsection{}`, `\paragraph{}`.
- Keep the document compile-ready. Do not include broken environments.
- If equations, tables, or figures are needed, include them only when supported by the notes.
- Produce a separate `.bib` file with all references.
- Mark incomplete BibTeX entries with a comment: `% [VERIFY] Missing fields`.

### Word (.docx)

- Read `/mnt/skills/public/docx/SKILL.md` before producing the file.
- Use Heading 1 for main sections, Heading 2 for subsections.
- Use the Normal style for body text.
- Format the References section using a hanging indent.
- Do not use text boxes or floating elements unless necessary.

### Markdown

- Use ATX-style headings (`##`, `###`).
- Use inline citations in author-year format: `(Smith et al., 2019)`.
- Produce a full References section at the end in a consistent format (APA by default, or as the user specifies).
- Use standard ASCII characters only; no special Unicode dashes.

---

## Author Review Flags Section

At the end of every manuscript, append a section titled:

```
## FLAGS FOR AUTHOR REVIEW (remove before submission)
```

This section must list:

1. Every placeholder inserted and its location (section and approximate context).
2. Every reference marked `[VERIFY]` with the partial information available.
3. Every `[CITATION NEEDED]` with the claim that needs supporting.
4. Every `[CLARIFY]` note with the ambiguity identified.
5. Any structural or content assumptions made during drafting.

This section should be written in plain language and is not part of the manuscript proper.

---

## Handling Incomplete or Contradictory Notes

When notes are incomplete:

- Infer the manuscript structure from context and state your inference.
- Use placeholders rather than guessing.
- Keep placeholders conservative: flag more rather than less.
- Prefer a shorter, accurate manuscript over a longer, padded one.

When notes are contradictory:

- Flag the contradiction in the author review section.
- Choose the more conservative or defensible version for the draft text.
- Mark the passage with `[CLARIFY: notes contain conflicting information here]`.

---

## Style Preferences Summary

Write in a tone that is:

- Precise and evidence-based
- Professionally confident but not arrogant
- Clear and direct without being blunt
- Academically credible without being needlessly dense

Avoid:

- En dashes and em dashes (always)
- Hype and superlatives without evidence
- Passive constructions used to obscure the subject
- Redundant phrasing and throat-clearing
- Jargon used without definition on first use
- Bullet points in continuous prose sections
- Fabricated or inferred facts

---

## Example Placeholder Usage

**In body text:**

> The intervention was shown to reduce symptom severity by approximately 30% `[CITATION NEEDED]`, a finding consistent with earlier work on cognitive reappraisal `(Smith et al., [YEAR])`.

**In a BibTeX entry:**

```bibtex
@article{smith2019reappraisal,
  author    = {Smith, Jane and Doe, John},
  title     = {Cognitive Reappraisal in Clinical Populations},
  journal   = {[JOURNAL NAME]},
  year      = {2019},
  volume    = {[VOLUME]},
  pages     = {[PAGES]},
  doi       = {[DOI]}
  % [VERIFY] Missing journal, volume, pages, and DOI
}
```

**In the author review flags:**

> **Reference [VERIFY]**: smith2019reappraisal. Known: authors (Smith and Doe), year (2019), approximate title. Missing: journal name, volume, pages, DOI. Appears in the Discussion section, paragraph 2.
