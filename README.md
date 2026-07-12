# Skoltech Bilingual PhD Dissertation LaTeX Template (Russian / English)

A LaTeX template for a **Skoltech** PhD dissertation and its synopsis
(автореферат). The Skoltech organization data (name, city, dissertation-council
address) is pre-filled; you only need to add your personal data. The template
**defaults to English mode**.

It has a single **language switch**:

* **Russian mode** — the whole document is in Russian (GOST Р 7.0.11-2011).
* **English mode** — the mandatory Russian title page and abstract come first,
  and the rest of the dissertation is in English (Skoltech-style).

*Двуязычный шаблон кандидатской диссертации: один переключатель задаёт язык всей
работы — либо полностью русский, либо английский с обязательными русскими
титульным листом и аннотацией в начале.*

## Features
* Encoding: UTF-8. Standard: GOST Р 7.0.11-2011.
* Engines: pdfTeX, XeTeX, LuaTeX. Bibliography: BibTeX or BibLaTeX/Biber.
* One switch (`thesislang`) drives language, fonts, hyphenation, decimal marker,
  section names, front-matter order and appendix numbering.

## The language switch

Open **`common/setup.tex`** and set the counter near the top:

```latex
\setcounter{thesislang}{1}  % 1 = English dissertation (Russian title + abstract first) -- DEFAULT
                            % 0 = Russian dissertation (everything in Russian)
```

That is the only change needed to switch languages.

## Quick start
1. Set `\setcounter{thesislang}{...}` in `common/setup.tex` (0 or 1).
2. Fill in your data in **`common/data.tex`** (the Skoltech organization, city and
   council address are already filled — replace the red `\fixme{…}` personal
   fields):
   * the main `\thesis…` / `\supervisor…` fields hold the **main-language** values
     (English in mode 1, Russian in mode 0);
   * for an **English** thesis, also fill the **`\thesis…Rus`** block (author,
     title, specialty, degree, supervisor) — these feed the mandatory Russian
     title page and abstract.
3. Put your Russian and English abstracts in `Dissertation/abstract_rus.tex` and
   `Dissertation/abstract.tex`, and your acknowledgements in
   `Dissertation/acknowledgements.tex`.
4. Write chapters: edit `Dissertation/part1.tex`, copy it to `part2.tex`, … and
   uncomment the matching `\include` lines in `dissertation.tex`.
5. Put your references in `biblio/external.bib` and your own publications in
   `biblio/author.bib` (shipped with a few example entries).

Placeholders are wrapped in `\fixme{…}` and printed in red so they are easy to
find. Remove them as you fill the template in.

## Building

```sh
latexmk -pdf dissertation.tex     # pdfLaTeX (default)
latexmk -xelatex dissertation.tex # XeTeX
latexmk -lualatex dissertation.tex# LuaTeX
latexmk -pdf synopsis.tex         # synopsis / автореферат (Russian)
```

All four dissertation combinations (pdfLaTeX/XeLaTeX × Russian/English) are known
to compile on TeX Live 2025.

## Structure
* `dissertation.tex` — main file of the dissertation.
* `common/` — shared setup: `setup.tex` (the switch and options), `data.tex`
  (all metadata), `packages.tex`, `fonts.tex`, `styles.tex`, `newnames.tex`,
  `renames.tex`, `characteristic.tex` (the "general characteristics" of the work).
* `Dissertation/` — front matter (`title_rus.tex`, `title.tex`, `abstract_rus.tex`,
  `abstract.tex`, `acknowledgements.tex`), `introduction.tex`, example chapter
  `part1.tex`, `conclusion.tex`, `dictionary.tex`, `appendix.tex`, `setup.tex`.
* `biblio/` — bibliography databases and style.
* `synopsis.tex` + `Synopsis/` — the автореферат.
* `presentation.tex` + `Presentation/` — a beamer defence presentation.

## Notes
* The **synopsis (автореферат)** is, by Russian regulation, a Russian-language
  document; build it in Russian mode (`thesislang=0`). It is not required for an
  English/Skoltech dissertation.
* In English mode the appendices are numbered A, B, C…; in Russian mode — А, Б, В…
* Put your organization logo at `images/logo.pdf` (vector PDF); delete the file
  if you do not want a logo.

## Attribution & license
This template is based on
[**Russian-Phd-LaTeX-Dissertation-Template**](https://github.com/AndreyAkinshin/Russian-Phd-LaTeX-Dissertation-Template)
by Andrey Akinshin and contributors, via the Skoltech-oriented
`Sk-Phd-LaTeX-Dissertation-Template` fork. The bilingual (Russian/English) switch
and the templatization (content removed, front matter generalized) were added on
top. Distributed under the same **Creative Commons Attribution 4.0** license — see
[`LICENSE`](LICENSE).
