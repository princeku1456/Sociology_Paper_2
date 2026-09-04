# Transcript → One LaTeX Chapter (for the local class-notes template)

> **How to use:** fill PART 0, paste one lecture's transcript(s) at the bottom, send.
> You get back **one chapter file** and nothing else — no preamble, no `\documentclass`,
> no title page, no compile step. Save the output as `chapters/NN-slug.tex` in your local
> template folder and add one `\include{chapters/NN-slug}` line to `main.tex`. See that
> template's `README.md` if you don't have it yet.
>
> This is the lightweight companion to the full master prompt — same content rules
> (zero information loss, ledger-based extraction, source-bound), but it assumes the
> visual design (`preamble.tex`) already exists and is fixed, so it never re-generates
> or re-verifies styling. That's what makes it cheap to run per lecture.

---

## PART 0 — RUN PARAMETERS

| Parameter | Value |
|---|---|
| `CHAPTER_TITLE` | e.g. Sociology as a Discipline |
| `CHAPTER_LABEL` | short slug for `\label{ch:...}`, e.g. `sociology-discipline` |
| `TRANSCRIPT_COUNT` | e.g. 2 |
| `LANGUAGE_OF_OUTPUT` | English (default) / Hindi |

If `CHAPTER_TITLE` is blank, infer it from the transcript and state your inference in the delivery note — don't invent a topic the transcript doesn't support.

---

## PART 1 — OUTPUT CONTRACT

1. Output is **one LaTeX fragment**, starting with `\chapter{CHAPTER_TITLE}` and ending after the Chapter Glossary. Nothing before it, nothing after it.
2. **Never include:** `\documentclass`, any `\usepackage`, colour/environment definitions, `\begin{document}`/`\end{document}`, a title page, `\tableofcontents`. All of that already exists once in the template's `preamble.tex` and `main.tex` — repeating it here is exactly the wasted work this prompt exists to avoid.
3. Use **only** the environments already defined in the template's `preamble.tex`: `KeyConcept`, `DataFact`, `TheoristView`, `CriticalAnalysis`, `CaseStudy`, `ComparisonBox`, `DebateBox`, `IndianContext`, `PYQLink`, `QuickRevision`, plus the standard `itemize`/`enumerate`/`tabularx`/`\paragraph{Label.}`. Do not invent a new box type — if content doesn't fit the eleven categories, use plain prose or a bullet instead.
4. Structure levels are fixed by the template: `\chapter` (this whole file, used once) → `\section` (sub-topics) → `\subsection` (sub-sub-topics). Do not use `\subsubsection` — the template only styles down to `\subsection`.
5. Show the full fragment as one fenced code block. No partial output, no "continue similarly" placeholders.
6. No brand names, channel names, teacher names, or platform references anywhere, including comments.
7. You are not expected to compile this. If you have sandbox tools available and the user has also given you `preamble.tex`, a quick local compile is a nice sanity check but is optional — don't spend time standing up a full document skeleton just to verify one chapter.

---

## PART 2 — TRANSCRIPT INTAKE & CLEANING

**Always keep:** every fact, figure, statistic, percentage, rank, year, date; every name — person, thinker, sociologist, committee, commission, report, act, scheme, treaty, organisation, court case, article/section number; every definition, cause, consequence, advantage, limitation, criticism; every example, analogy, anecdote, case study; every mnemonic or memory hook; every answer-writing instruction; every exam-relevance remark or PYQ reference; every student doubt and its answer; every sociological perspective or theoretical viewpoint.

**Always drop:** greetings, attendance/audio checks, class logistics, batch/app promotion, subscribe/like requests, filler and repetition (keep only the corrected version of a self-correction), off-topic chit-chat. Dropping noise is not an exception to zero-information-loss — zero loss applies to substance, and noise carries none.

**ASR errors:** fix silently when unambiguous from context (restore official spellings of thinker names, sociological terms, acts, schemes, articles, committees, organisations, place names). Never substitute what you believe is factually correct for what the teacher actually said — reproduce the teacher's stated figure even if you think it's wrong. If a term is unsafe to reconstruct, write your best reading + `[as stated in lecture]` and flag it in the delivery note.

**Translation:** entirely in `LANGUAGE_OF_OUTPUT`, formal register. Preserve untranslated: act names, scheme names, article/section numbers, committee names, report titles, organisation names, legal maxims, sociological terms of art (e.g. Gemeinschaft, Gesellschaft, anomie), and any Hindi term the teacher explicitly glosses. Keep Indian numbering alongside a readable form: `\rupee 1.5 lakh crore`. Preserve emphasis force. Translate analogies faithfully — don't substitute your own.

**Uncertainty:** never guess to fill a gap. Write what is recoverable, flag the gap in the delivery note.

**Multiple transcripts for one chapter:** process in order. If they're clearly continuous parts of one lecture, merge them and continue the `\section` sequence without restarting; otherwise give each its own `\section`. Never delete a later repetition — if the teacher adds nuance on a repeat, keep the fuller version.

---

## PART 3 — EXTRACTION PROTOCOL

**Pass 1 — Ledger (internal, not in the output):** read the transcript(s) start to finish; list every extractable item in order, tagged `DEF` `FACT` `NAME` `CAUSE` `EFFECT` `EX` `CMP` `CRIT` `SOL` `EXAM` `TERM` `THEORY` `DEBATE` `INDIA`. One line per item, no compression.

**Pass 2 — Write the chapter:** convert every ledger line into content, in ledger order. No line may vanish.

**Pass 3 — Coverage audit (before delivery):** confirm every ledger item appears in the fragment. Report ledger count vs. placed count in the delivery note.

**Chunking rule:** for long transcripts, complete the ledger for chunk *n* before reading chunk *n+1*. Never skim ahead — thinning the back half of a lecture is the most common failure of this task.

---

## PART 4 — CONTENT RULES (non-negotiable)

1. **Zero information loss** — every ledger item appears; no collapsing distinct points, no dropping examples for feeling repetitive.
2. **Strictly source-bound** — transcript(s) only, no outside facts even if correct; flag missing context in the delivery note, not the chapter.
3. **Lecture structure preserved** — teacher's sequence and groupings exactly, no "cleaner" reorganisation.
4. **Depth over labelling** — define every key term; write full reasoning chains, not just conclusions; keep all parts of multi-part arguments; show both sides of comparisons explicitly.
5. **Bullet discipline** — one idea per `\item`; an item past ~3 lines usually hides two items; nested lists carry elaboration only, never orphaned.
6. **Escaping** — `\&` `\%` `\$` `\#` `\_` `\{` `\}`, `\textasciitilde{}` `\textasciicircum{}` `\textbackslash{}`, `\rupee` for ₹, `--`/`---` for en/em dash, `` ``quoted'' `` for quotes, `\textdegree{}` for °. **`40\%`, never `40%`** — an unescaped `%` silently comments out the rest of the line. Re-read your own output for bare `%` and `&` before delivering.

---

## PART 5 — CHAPTER STRUCTURE

```latex
\chapter{CHAPTER_TITLE}
\label{ch:CHAPTER_LABEL}

\section{First sub-topic, in lecture order}
\subsection{First sub-sub-topic, if the material needs a third level}
  ... body paragraphs, bullets, note boxes, tables ...
  ... end the \section with a QuickRevision note ...

\section{Second sub-topic}
  ...

\section*{Chapter Glossary}
\addcontentsline{toc}{section}{Chapter Glossary}
  ... two-column tabularx of every TERM from the ledger, alphabetical ...
```

- Every `\section` ends with a `QuickRevision` note before the next `\section` starts — mandatory, same as the full master prompt.
- `\paragraph{Label.}` (run-in, bold italic) is for a single named provision or thinker's specific contribution worth calling out by name (e.g. "Durkheim on Suicide.", "Section 3(p)."), not a heading level of its own.
- If the lecture gave answer-writing guidance (dimensions, keywords, intro/conclusion lines, diagram suggestions), add a `\section*{Answer-Writing Pointers}` (same `\addcontentsline` treatment as Glossary) before the Chapter Glossary. Omit it entirely if the lecture had none — don't manufacture one.
- No `\clearpage`, no `\sectiondivider` needed inside a chapter — `\chapter` already forces a fresh page in the template, and a divider between `\section`s within one chapter usually just adds clutter. Only reach for `\sectiondivider` if a chapter has a genuinely large tonal break mid-way (rare).

---

## PART 6 — CONTENT-TO-ELEMENT MAPPING

| When the teacher… | Use |
|---|---|
| Defines a term or explains a core sociological idea | `KeyConcept` |
| States a number, statistic, rank, date, index position, census data | `DataFact` |
| Presents a thinker's perspective — Durkheim, Weber, Marx, Merton, etc. | `TheoristView` |
| Names one specific thinker's contribution worth setting off | `\paragraph{Label.}` run-in, then normal text |
| Draws a fine distinction, flags exam importance, or offers a critical evaluation | `CriticalAnalysis` |
| Gives a real-world example, case study, ethnographic instance, or analogy | `CaseStudy` |
| Compares 2+ items on 1–2 attributes (e.g. functionalism vs conflict theory) | `ComparisonBox` |
| Compares 2+ items on 3+ attributes | Plain `tabularx` comparison table (booktabs rules, `Y` columns, no colour fill — matches the template) |
| Presents opposing sociological perspectives or a contested debate | `DebateBox` |
| Discusses India-specific sociological phenomena (caste, tribe, village, kinship, etc.) | `IndianContext` |
| Mentions a past-year question or exam framing | `PYQLink` |
| Ends a `\section` | `QuickRevision` (mandatory) |
| Explains a process, chain, or sequence of stages | `enumerate`, one stage per `\item` |
| Gives challenges then solutions | two `\subsection`s: "Challenges" and "Way Forward" |
| Says "write this down" / gives a keyword | `\textbf{keyword}` inline **and** add it to the Chapter Glossary |

**Density:** target 20–25% of the chapter as boxed notes — most content stays plain prose and bullets. Never place two note boxes back to back with no text between them; never wrap a whole `\section` in a single box. A note holding one fact reads as plain prose inside the box, not a forced one-item bullet list.

---

## PART 7 — DELIVERY NOTE

Alongside the fragment, a short report — no preamble, no restating this prompt:

- Sections and subsections in this chapter
- Ledger items extracted vs. placed
- Note-box counts by type; comparison table count
- Uncertain items — or "none"
- Anything the teacher referenced but did not explain
- Confirmation that the fragment contains no `\documentclass`, `\usepackage`, or preamble content — only chapter body

---

## TRANSCRIPT(S)

Paste the transcript(s) for this one chapter below, labelled Transcript 1, Transcript 2, … if more than one:

```
[PASTE TRANSCRIPT(S) HERE]
```
