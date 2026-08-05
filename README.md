# Class Notes — Local LaTeX Template

A one-time template you compile locally with `pdflatex`. Every new lecture becomes
one chapter file; you never regenerate the whole book from scratch.

## Folder contents

```
main.tex               — the book: title page, table of contents, \include list
preamble.tex            — all styling (fonts, colours, note boxes, tables, header/footer)
chapters/
  01-tkdl-patents-act.tex   — sample chapter, already wired into main.tex
chapter-prompt.md        — the short prompt: paste a transcript in, get a chapter file out
README.md                — this file
```

## One-time local setup

You need a TeX distribution: [TeX Live](https://tug.org/texlive/) (Windows/Linux) or
[MacTeX](https://tug.org/mactex/) (Mac). Any recent install has every package this
template uses (`tcolorbox`, `titlesec`, `tocloft`, `fancyhdr`, `tabularx`, `charter` —
all standard).

```bash
cd class-notes-template
pdflatex main.tex
pdflatex main.tex        # run twice — the second pass fixes the TOC page numbers
```

`main.pdf` is your book.

## Adding a new chapter (the normal workflow)

1. Open a chat with the **chapter prompt** (`chapter-prompt.md`) and paste your transcript
   at the bottom of it, same as before.
2. You get back **one chapter file** — starting at `\chapter{...}`, nothing else. No
   preamble, no packages, no title page. Save it as `chapters/02-your-topic.tex`
   (increment the number).
3. In `main.tex`, add one line where you want it to appear in the book:
   ```latex
   \include{chapters/02-your-topic}
   ```
4. Recompile locally (`pdflatex main.tex`, twice).

That's the whole loop. The assistant only ever produces the chapter body — a few hundred
lines instead of a full ~250-line preamble plus a sandboxed compile-and-render cycle every
single time, which is what made earlier runs slow.

## Editing the design once, for every chapter

Everything visual — colours, note-box style, table style, fonts, header/footer — lives in
`preamble.tex` alone. Change it once there and every chapter (old and new) picks it up on
the next compile. You should never need to touch a chapter file to change how it looks.

Two things worth knowing in `preamble.tex`:
- `\HeaderLeftText` near the bottom — the static left-hand running header text (currently
  "UPSC GS Paper 3 • Science & Technology"). Edit the string there if you start a book for
  a different paper.
- The `note` environment and its eight aliases (`KeyConcept`, `DataFact`, `GovtPolicy`,
  `CriticalPoint`, `ExampleBox`, `ComparisonBox`, `PYQLink`, `QuickRevision`) — these are
  what the chapter prompt's output uses. Don't rename them without also updating
  `chapter-prompt.md`, or new chapters will reference environments that don't exist.

## Editing the book-level details in `main.tex`

Near the top of `main.tex`:
```latex
\newcommand{\BookExamEyebrow}{CIVIL SERVICES EXAMINATION}
\newcommand{\BookExamLine}{UPSC \textbullet\ GENERAL STUDIES PAPER 3}
\newcommand{\BookTitle}{Science \& Technology}
\newcommand{\BookSubtitle}{Class Notes}
\newcommand{\BookDate}{2026}
```
Edit these for the title page. One book = one subject/paper; start a fresh copy of the
whole template folder for a different paper.

## Faster iteration while drafting: `\includeonly`

If you're only working on one chapter and don't want to wait for the whole book to
recompile, uncomment and edit this line near the top of `main.tex`:
```latex
\includeonly{chapters/02-your-topic}
```
Only that chapter's content is inserted (everything else is skipped, leaving gaps), which
compiles much faster. **Comment it back out** — or list every chapter — before your final
full compile, or you'll ship a PDF with chapters missing.

## Chapter numbering vs. file numbering

The `NN-` prefix on a chapter filename (`01-`, `02-`, …) is just for your own sorting in
the folder — LaTeX numbers chapters by the order of the `\include` lines in `main.tex`,
not by filename. If you reorder chapters, reorder the `\include` lines; renaming the files
is optional tidiness.
