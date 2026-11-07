# Premature mortality: data of a scoping review

Data and codebook for the scoping review

> *Premature mortality: one term, many standards. A scoping review of its conceptualisations.*

The review maps how premature mortality is conceptualised in 674 peer-reviewed articles. It does so along four dimensions in two pairs:

- **identification**: which deaths came too early, or that some did (the *identification form*), and against what standard (the *identification standard*);
- **extent**: how the extent of premature death in a population is built (the *extent form*), and against what standard (the *extent standard*).

It also records two descriptors of each article: its **discipline** and its **ethical framing**, meaning the normative principle the article names, if any.

The protocol was published in advance and is cited in the article's Methods. The search, the screening and the selection of the 954 articles read in full are described there and in the article's Methods.

Everything here is a copy of the review's working files. The article PDFs are not included, because they are copyrighted (see *What is not included*).


## Layout

```
README.md                  this file
codebook/                  the Elicit prompts and the framework
data/
  elicit/                  the raw Elicit exports, combined in one workbook
  coded/                   the coded data and the derived files
```

Article ids have the form `s1art###` or `s2art###`. They match the identifiers in Supplementary Material S7 of the article.

The two reviewers are identified as **R1** and **R2**:

- **R1** coded 189 of the first 200 articles on the protocol's dimensions.
- **R2** screened and coded every article and confirmed every derived code. Wherever the files record who decided, R2 is named, in the `reviewer` columns, the `confirmed` stamps (e.g. `R2 2026-09-22`) and the notes.

Some notes record that a decision was drafted by an AI assistant (Claude) under R2's delegation; each such decision is marked as such.


## The codebook — `codebook/`

| File | Contents |
|---|---|
| `elicit_prompts.md` | The instructions given to Elicit for each of the eleven extraction columns, verbatim, as last used. |
| `FRAMEWORK.md` | The framework: the dimensions, the levels of each, the standards, the coding rules and a dated log of coding rulings. It is authoritative on definitions. |

Supplementary Material S5 of the article gives each column's question and terms in short.


## Data

### `data/elicit/elicit_exports_all.xlsx` — raw extraction

The 19 Elicit exports, one per sample (block) of articles, combined in one sheet: 934 rows, one per article and export. The first column, `sample`, names the export a row comes from (`sample12` … `sample78`); the other columns are those of the exports, one per codebook question (S0, S1, A1, A2, B1, B2, D1, E1, E2, F1, F2) with Elicit's supporting quotes, tables and reasoning for each. Each answer has the form `ANSWER | "quoted sentence" (Section)`. Two exports each lack two of the supporting-quote and supporting-table columns, and one has `Summary` columns the others lack; those cells are empty. Otherwise every cell is as downloaded. The exports do not distinguish a cell produced by the model from one a human replaced; the coded data below are the exports after screening decisions and corrections were applied.

### `data/coded/` — the coded data


| File | Contents |
|---|---|
| `coded_all.csv` | One row per included article and sample (676 rows, 674 articles; two articles were drawn twice). It holds the extracted and corrected answer to every column: `s1_term` (discipline), `a1_term` (identification form), `a2_term`, `b1_code`, `b2_term`, `d1_term`/`d1_code`, `e1_given`/`e1_code` (principle named), `e2_*`, `f1_*` and `f2_term`. It combines the processed exports of all samples, with the screening decisions and corrections applied, and the codes of the articles coded by reading the PDF; it was never edited by hand. |
| `quotes_all.csv` | The supporting quotation for every answer. |
| `identification_standard_all.csv` | The identification standard of each article (`id_standard`), with the rule that derived it. |
| `extent_level_all.csv` | Every extent form at which an article reports a figure (`level`), with its quantification. |
| `extent_standard_all.csv` | The extent standard of each extent form an article reports. |
| `principles_all.csv` | The ethical framing descriptor: the group of the principle an article names (`principle_group`). |
| `article_flags.csv` | Per-article flags reported in the Results: a second identification rule, a preventable second rule, a criterion recovered from the measurement, the source of a cause list, and the source or reason given for a fixed age. |
| `cause_list_sources.csv` | For the 26 cause-list articles, where the list comes from, with the evidence (coded value, or the PDF page and quotation). |
| `included_articles.csv` | The table of Supplementary Material S7: each article's reference (authors, year, title, venue and DOI, checked against the PDF and Crossref), codes and descriptors, labelled as in the article. |
| `prisma_counts.csv`, `exclusion_grounds_all.csv`, `excluded_articles.csv`, `decisions_all.csv` | The flow of articles and the grounds for exclusion. |
| `discipline_by_dimension.csv` | Counts by discipline on all four dimensions. |


## Names in the data and in the article

The data keep the internal values used during coding. The article uses these names:

| In the data | In the article |
|---|---|
| `a1_term` | identification form |
| `id_standard` | identification standard |
| `level` (extent) | extent form |
| `extent_standard` | extent standard |
| `recomputed schedule` | life-table statistic |
| `schedule contrast` | life-table contrast |
| `distributional` (extent) | dispersion |
| `own counterfactual` | the population's own mortality under other conditions |
| `fixed value` | fixed external value |
| `own statistic` | the population's own statistic |
| `other population` (standard) | another actual population |
| `prototype`, `prototype_family` | not used in the article (an earlier device, dropped; see S3) |

`included_articles.csv` already uses the article's names.


## What is not included

- **The 939 article PDFs:** they are copyrighted. The articles are identified in S7 of the article and in `included_articles.csv`, with DOIs where available.
- **The search results and the Rayyan screening of titles and abstracts:** these are described in the protocol.
- **The R code** that processed the exports and derived the variables, and the working notes and drafts used during the review.


## Licence

The data and the codebook are licensed under the Creative Commons Attribution 4.0 International licence (CC BY 4.0); the full text is in `LICENSE`.
