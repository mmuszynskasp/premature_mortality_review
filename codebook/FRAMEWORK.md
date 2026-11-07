# FRAMEWORK.md — the conceptual framework, as decided
# Status: authoritative for framework questions. Where CLAUDE.md, the codebook,
# scripts or the draft disagree with this file, this file wins and the others
# need updating. Decisions marked OPEN are not yet made; do not treat a
# recommendation as a decision.
# Last revised: 2026-09-20, from the working session of 19-20 Sept.

## 1. Vocabulary

- **Dimensions** and **levels**. Never "coordinates", "positions", or
  "prototypes" in the manuscript or the codebook.
- Premature *death* is individual-level; premature *mortality* is
  population-level. Never interchangeable.
- The concept ladder: conceptualisation > definition > operationalisation.
  "Measurement" suggests the bottom rung and is not used as a dimension name.

## 2. The four dimensions, two pairs

| Pair | Dimension | Fixes |
|---|---|---|
| Identification | **identification kind** | which deaths count as premature (the form of the rule) |
| Identification | **identification standard** | what fills the rule in, and where it comes from |
| Extent | **extent level** | how age at death enters the population quantity |
| Extent | **extent standard** | what that quantity is reckoned against |

The pair names are **extent** / **extent standard** — not "measurement"
(operationalisation overtone), not "aggregation" (Sen's word, kept only in the
sentence crediting Sen 1976). The split generalises Sen in two respects, stated
in the manuscript: aggregate identification leaves no individual shortfalls to
aggregate, and the extent is itself reckoned against a standard, where poverty's
line belongs to identification alone.

Kind and standard are distinct: "deaths before an age" is a kind; "65, from
Medicare eligibility" is its standard. The old coding carries both in one
column; the split is a pending codebook change.

## 3. Identification kinds

As in the agreed table (tab:a1def): all deaths; fixed age; avoidable causes;
amenable causes; preventable causes; intervention; counterfactual scenario;
other population; distributional statistic; model component; and the
conjunction kinds (other population × fixed age; amenable × other population;
avoidable × other population).

Notes that go beyond the table:
- **DISTRIBUTIONAL STATISTIC is a known conflation**: it is a fixed-age kind
  whose *standard* is the population's own distribution. After the
  kind/standard split it dissolves into FIXED AGE + own-mortality standard.
  Keep the code until the split; record the dissolution when it happens.
- **Deaths of despair is not a level** (n = 2 in the corpus, coded
  inconsistently). Structurally a cause list; what differs is the ground of the
  list (social diagnosis, not avoidability). Handle as a sentence in the
  cause-list discussion: a third ground for cause lists that the vocabulary
  does not mark.
- **Exposure counterfactuals** (tobacco-, alcohol-, PM2.5-attributable deaths)
  are COUNTERFACTUAL SCENARIO, not a new kind. What is distinctive sits in the
  standard (§5).
- The "no headcount as aggregation" clause in the all-deaths row is an extent
  fact and comes out of the identification definition; dimensions are defined
  independently so entailments stay testable.
- **Preventable-alone is an empty cell** in the corpus (occurs only inside
  "avoidable"). Report as a finding: the OECD/Eurostat instrument separates
  preventable from treatable; the literature does not.

## 4. Extent levels — six, settled

Individuation test: **how does the age at which death occurred enter the
population quantity?** (Not "what does each death contribute" — that phrasing
presupposes individual identification.)

**Level names** (R2, 2026-11-06): in everything written for the manuscript,
level 1 is the **life-table statistic** and level 7 the **life-table contrast**.
The data and code keep the internal values `recomputed schedule` and
`schedule contrast`; the scripts that write displayed tables relabel them
(as `distributional` is shown as "dispersion").

1. **Life-table statistic** (internal: recomputed schedule) — through the hazard, non-additively; nothing is
   summed over deaths (cause-deleted life expectancy; competing risks absorbed;
   reports realisable rather than gross years)
2. **Count** — not at all; every death enters equally
3. **Years** — linearly, as years remaining against the benchmark
4. **Weighted years** — non-linearly: discounting, age weighting. This is where
   the badness-of-death debate lives; never fold into 3
5. **Money** — through a valuation function (magnitude-sensitivity depends on
   the method; code the method)
6. **Distributional** — through distance from a central tendency of the
   age-at-death distribution (variance, Gini, disparity measures other than e†)
7. **Life-table contrast** (internal: schedule contrast; added 2026-09-20) — through the hazard, as with
   level 1, but the reported quantity is the *difference or ratio between two
   schedules*: a cause-deleted gain, a life-expectancy gap between groups or
   periods, a decomposition contribution, a scenario difference. Nothing is
   summed over deaths and the figure has no reading as a duration — nobody
   lives 0.16 years — so the contrast is constitutive of the quantity rather
   than a standard it is reckoned against.
   **Five varieties, one level.** They differ by what the *other* schedule is,
   which is the extent standard, not by how age enters: **cause-deleted gains**
   (own schedule with a cause removed; jie14, guimarares25), **gaps** (another
   population; crump13, heslop15, leider20, jackman19, wuchung18,
   manouchehrinia14, kiiskinen98, wilkie24, stringhini17), **decompositions**
   (own schedule at another time, or the other sex; aburto21, orpana19,
   martelin, hiam17),
   **scenario differences** (own schedule under an intervention; holm14,
   lipan18) and **attributable reductions** (own schedule at a
   counterfactual exposure; cerquiera, bjornelv21, richmond08, qi, yang20,
   helleberg2012). Counts in the corpus: 2, 9, 4, 2, 6 (hiam17 and
   stringhini17 added in recheck_46; adair18 excluded as a commentary in
   recheck_47, 2026-09-22). Keep them as varieties
   in the write-up, never as levels; they are the cleanest demonstration that
   one extent can carry every standard form.

**Deriving the extent level** (R2, 2026-09-21; `code/21_extent_level.R`):
- An article is recorded at **every** level its reported figures use, not only
  the headline one: "probability; years total; life expectancy" gives count,
  years and life-table statistic. The Results report how many articles use each
  level and how many use more than one.
- A ratio of rates (relative risk, rate ratio, SMR) is the **count** level with
  the ratio recorded as its quantification; the comparison is the extent
  standard.
- The articles whose figure could not be determined are rechecked from the
  Elicit exports and then the PDFs, as the identification standard was.
- An **odds ratio** is also the count level, but recorded with its own
  quantification, "odds ratio", since it is a ratio of odds rather than of
  rates (R2, 2026-09-22). Confirmed level for all 687 articles in
  `data/coded/extent_level_all.csv`.

What the old d1 coding mixed in, and where it goes instead:
- **Quantifications** (raw / rate / proportion / probability / risk) scale a
  level; they are not levels. Keep as a separate recorded property.
- **Comparisons** (ratio of summaries, difference of summaries, rank) belong to
  the **extent standard** *where the quantity survives without them*. A count
  of deaths is the same count whether or not it is divided by another
  population's; the comparison is then a choice of standard. Where the quantity
  exists only as a contrast, as in level 7, the comparison is the extent
  itself. Qualified 2026-09-20 on R2's ruling that a cause-deleted life
  expectancy, and ratios or differences of life expectancies, are a different
  extent from a life expectancy.
- **Two tests separate levels 1, 6 and 7.** Shift every age at death up by one
  year: a life expectancy rises by a year (level 1, location-sensitive),
  variance and Gini do not move (level 6, location-invariant). Then ask whether
  the figure goes to zero when the two schedules coincide: if it does, it is
  level 7. e† stays at level 3 because it sums remaining life expectancy over
  deaths, so something is summed per death despite the name.
- e† is level 3 (years) with the population's-own-schedule standard; GBD YLL is
  level 3 (or 4 where weighted) with a frontier standard. The pair is the
  canonical illustration that the extent standard is the whole distance between
  a burden measure and an inequality measure.

CLOSED 2026-09-20: level 1 survives. It was open whether it decomposes into
level 6 with a counterfactually modified own-mortality standard; the
shift-by-one-year test settles it without reading the articles, since a life
expectancy is location-sensitive and a dispersion measure is not. What the
life-expectancy articles decide instead is the level 1 versus level 7 split,
which needs reading because `d1` records LIFE EXPECTANCY for a level, a gap and
a cause-deleted gain alike. 58 articles in the corpus mention life expectancy
in D1.

Recode plan for d1: ~403/735 mechanical; 239 years articles need the 3-vs-4
split (check the f2 weighting column first — only 23 mention weighting in
d1_code); ~29 need reading for the 1-vs-6 boundary; ~65 unresolved are mostly
the NOT STATED residue and resolve with the recheck.

## 5. Standards — both pairs

The four original forms are below; the decisions of 2026-09-21 that follow
extend them to ten levels on the identification side, and the extent side
mirrors them (tables/extent_standard.tex) except that it has "none" (a raw
tally) and no "none needed".

1. fixed external value, no population behind it
2. a statistic of the population's own mortality
3. best-attainable frontier, observed or constructed, that no population lives
4. another actual population, chosen as comparator

Additional decisions:
- On the extent side, **"none" is a real value** (a raw tally reported against
  nothing), distinct from "cannot determine".
- A frontier can be specified **in mortality terms or in exposure terms**
  (GBD TMREL: zero smoking). Same form, but the exposure version imports a
  causal model (the relative risks) into the standard — a commitment a
  mortality-schedule frontier does not carry. State in the framework text; the
  justification question should name it.
- Counts have standards too (excess deaths vs a comparator or baseline); the
  dimension is not confined to years-based measures.
- **Fifth form, identification side** (R2, 2026-09-21): the study population's
  own mortality under other conditions — at another time, as projected, without
  an event, or without an intervention (the reference scenario of an
  intervention study). Historical baselines and expected mortality belong here,
  not under form 2.
- **Frontier or other population** (R2, 2026-09-21, rule (a)): a comparator
  population is a frontier only where the article selects it explicitly for
  performance — vargas (s1art168): 23 high-income countries scoring over 90 on
  the Universal Health Coverage index. Otherwise it is another actual
  population, including the best-off group in a social gradient (least deprived
  quintile, highest education group) and comparators chosen for proximity or
  data, as allel22 (s2art013): Iran's neighbours with data in the WHO database.
- **Identification standard vs extent standard** (R2, 2026-09-21). The
  identification standard decides which deaths, or how many, count as premature;
  the extent standard is what the population quantity is reckoned against. So:
  under ALL DEATHS nothing fills the identification rule in ("none needed") and
  the life table that counts years lost is the extent standard; for cause lists
  the identification standard is the list and its age cap (a fixed value), and
  "zero deaths from the listed causes" is a count reported against nothing,
  extent standard "none"; for attributed conditions it is the named condition.
  Where a comparison decides how many deaths count (vargas, allel22, SMRs
  against national rates) it serves both pairs. Derived by
  `code/18_identification_standard_form.R`; the extracted B1 column mixes the
  two pairs and must not be read as the identification standard directly.
- **Levels of the identification standard** (R2, 2026-09-21), ten: none
  needed; fixed value; own statistic; own mortality under other conditions;
  other population; frontier; exposure at zero; exposure at its theoretical
  minimum; exposure at a reference category; continuous (below). The three exposure levels are not
  varieties of the frontier: a frontier is a whole mortality schedule, each
  exposure level changes one exposure and imports a causal model. This
  supersedes the line above that files zero exposure (TMREL) under the frontier
  for the identification side.
- **Coding rules for the exposure levels** (R2, 2026-09-21): an attributable
  fraction for a binary exposure (obesity, social isolation, smoking) is
  exposure at zero; "theoretical minimum" covers any minimum-risk
  counterfactual — plausible or feasible minimum, the lowest-risk intake — not
  only a named TMREL. Where an article does two things at once, the standard is
  the one that decides how many deaths count (a decomposition's comparison, a
  study's main counterfactual). Confirmed for all 691 articles in
  `data/coded/identification_standard_all.csv`, derived by
  `code/18_identification_standard_form.R`.
- **Extent standard, two rules** (R2, 2026-09-22; `code/23_extent_standard.R`):
  a life-table contrast against the same population with a cause removed
  (cause-eliminated life expectancy) is reckoned against the population's own
  mortality under other conditions, not against exposure at zero; and a plain
  life expectancy or median age at death, reported as it stands, is reckoned
  against nothing ("none"), not against the population's own statistic.
- **Tenth level, continuous** (R2, 2026-09-21): a contrast per unit of a
  continuous exposure, naming no exposure level. The kind stays COUNTERFACTUAL
  SCENARIO (the population's own mortality with the exposure changed); the
  level pairs with the continuous extent level. Steell19, eisenga19,
  zhuzhang24.

## 6. Entailment (P1), qualified

An extent in life-years requires a benchmark age per death. Individual
identification supplies it; aggregate identification supplies it **only where
the aggregate is resolved by age** (GBD attribution within age-sex cells).
Manuscript wording: "some combinations are unavailable rather than merely
unused." Do not state the absolute version.

A second entailment, added 2026-09-20 with the schedule-contrast level. In a
decomposition the same comparison appears twice: it is the identification
standard, because the comparison is what makes the deaths count as premature
(the rule adopted on orpana19), and it is the extent, because the reported
figure exists only as a difference between schedules. This is not
double-coding. The identification pair answers which deaths count and against
what; the extent pair answers how the quantity is built. The manuscript should
say so where the decomposition articles are discussed, since a reader meeting
the same schedule in two columns will otherwise read it as an error.

## 7. What the typology claims — two kinds, kept apart

- **Entailed (strong, negative)**: what the measure cannot register. A count is
  indifferent between a death at 20 and at 64; an own-mortality standard cannot
  record that the whole population died early; a frontier standard cannot
  record that a population has done well enough. Properties of the measure;
  intentions do not remove them.
- **Open (weak)**: the positive view that would justify the choice. Levels
  underdetermine justifications (Krieger: two grounds for the same 65).
  Reported as the question the user should be able to answer.
- Police "commit*" in the draft: strong reading earns the word, everything else
  is "question"/"justification".
- **The two pairs answer to different literatures**: identification standard →
  distributive justice (sufficientarian, capabilitarian, luck-egalitarian);
  extent level → axiology of death (deprivationism, time-relative interests).
  There is no such thing as *the* background theory of a measure; it needs two.
  This is an addition to Sørheim et al. 2024, not an aside.

## 8. Corpus rules (beyond the codebook)

- **Screening test**: TREATS-AS-EARLY vs ONLY-DIFFERENCE. A between-group
  contrast used as the measure is in; a hazard ratio reported as a study result
  is out (S0 v2.5: cohort with mortality as dependent variable → out).
- **Eligibility (separability test)**: constitutive vs scope. A restriction
  that is itself the criterion (neonatal deaths analysed as such) → out; a
  standard specified independently of the restriction (national life table on
  adolescents; national norms on a patient cohort) → in. A flat all-ages rule
  would exclude SDG 3.4. The two tests give **separate exclusion reasons** and
  separate PRISMA lines.
- **No identification rule, no article** (R2, 2026-09-21). An article whose
  identification kind is NOT STATED or CANNOT DETERMINE picks out no premature
  deaths and does not operationalise the concept; it is excluded under the
  existing ground "not operationalised" and does not appear as a level of the
  identification dimension. "Cannot determine" remains a permitted answer on
  every other dimension. Applied in recheck_43 to s2art559 roscoe22, s2art305
  ji23 and s1art158 sorheim24; the last stays cited in the manuscript as
  literature.
- **Population level is a corpus descriptor**, not a fifth dimension.
- New recheck columns: `a1_source` (STATED / INHERITED / NONE — inherited has a
  rule), `has_own_procedure`, `term_location`, `null_point` (free text; note
  when the quantity is insensitive to the exposure the article is about —
  Tannous case, candidate Discussion example).
- **GBD inheritance (decided 2026-09-20, on s2art204gbd25; covers every GBD
  round)**: an article whose premature-mortality measure is given by GBD
  inherits all of GBD's dimensions — identification ALL DEATHS, extent years of
  life lost, standard the frontier life table, so B2 is ASPIRATIONAL even where
  the article names no table. YLL inside DALYs passes the screening test. The
  cause the article studies, and any decomposition of that burden by risk
  factor, is the research question, not a second operationalisation: the
  article stays on one row and A2 stays SINGLE. "Own procedure" takes a third
  value, EXTRACTED, for articles that take ready-made estimates without
  computing them.
- **Risk-attributable figures (decided 2026-09-20)**: the null point decides.
  If the headline quantity would be zero at the counterfactual exposure level,
  the exposure identifies and the kind is COUNTERFACTUAL SCENARIO, with the
  standard specified in exposure terms. If the quantity is unchanged when the
  exposure is absent — the headline is a cause burden and the risk
  decomposition a side table — the kind is ALL DEATHS.
- **A file holding a whole journal issue is coded as the article its name
  points to (decided 2026-09-22, on s1art166)**: the PDF is the whole of
  *World Health Statistics Quarterly* 42(1) 1989 on preventable mortality, six
  articles; the corpus row is Uemura's, pp. 26-41, which the file stem names.
  The others are not separate rows.
- **A cause list with its age cap is one rule (decided 2026-09-22,
  recheck_48)**: the cap is part of the list's definition (OECD/Eurostat,
  Nolte and McKee), so A2 is SINGLE, not COMPOUND. The seven articles coded
  COMPOUND were all of this kind and were recoded; COMPOUND is now empty in the
  corpus. MULTIPLE (28) means a second rule applied to another part of the
  analysis; the article's kind is the rule behind its headline figure.
- **Preventable and treatable parts of a cause list (decided 2026-09-24,
  recheck_52, by Claude under R2's delegation)**: a list is coded by what it
  contains, not by what the article calls it, so a health-care-only list called
  "avoidable" is AMENABLE CAUSES (botero15). Where an article reports the
  preventable part and the treatable part of a list as figures of their own
  beside the headline, A2 is MULTIPLE (seven articles). No article's headline
  rule is PREVENTABLE CAUSES; the level holds only second rules.
- **External referent for OTHER POPULATION (decided 2026-09-20)**: where an
  article reports a mortality contrast and nothing else, the question is what
  kind of standard the contrast uses. **OTHER POPULATION requires a referent
  outside the study's own cohort** — matched controls from a register, national
  or regional rates, another country, another sex or ethnic group, a
  general-population life table. A contrast between exposure-defined subgroups
  of a single cohort, with no external referent, is not a conceptualisation of
  premature mortality and the article is excluded as not operationalised
  (clausen07, bemmel06, toender20, toren18, whitfield17, kokkinen19,
  stenbacka12). **COUNTERFACTUAL SCENARIO is not subject to that test**: its
  standard is the same population under conditions that did not obtain, so it
  is internal by definition, and section 3 names exposure counterfactuals as
  this level for that reason. heath22 stays on that ground, with the twelve
  other within-cohort exposure counterfactuals.
- **Decomposition of a difference (decided 2026-09-20, on s2art501 orpana19)**:
  where the reported figure decomposes a difference between two mortality
  schedules — an Arriaga or Pollard decomposition, a cause-specific
  contribution to a life-expectancy gap or to a change in life expectancy — the
  identification standard is **the comparison, not the life table** used to
  compute either side. The table is machinery; the null point is that the two
  schedules are identical. Which kind applies follows the other schedule: the
  same population at an earlier date is a COUNTERFACTUAL SCENARIO, the
  counterfactual of unchanged mortality (corpus convention across nine
  articles, among them s2art266 hiam17, s2art542, s2art249, s2art128, s2art553,
  s1art075); a different group, sex, region or country is OTHER POPULATION.
  Several such comparators in turn are standards of the same kind, so A2 stays
  SINGLE. ALL DEATHS is reserved for an absolute quantity of years counted to a
  table, or a level of life expectancy.
- **Life-expectancy measures (decided 2026-09-20)**: where the figure is a life
  expectancy or a life-expectancy gap, the identification kind is ALL DEATHS
  unless the article applies a restriction of its own — an age bound, an
  avoidability list, a comparison population — or unless the figure is a
  decomposition, which the rule above governs. The table used is the standard
  and goes in B1 and B2. The distinctive feature of these articles is in the
  extent pair, not the identification pair, which is why the sixty
  life-expectancy articles in the corpus distribute across every existing kind.
  No new level: a level addition forces re-runs under codebook section 19 and
  would have to be applied to all sixty.
- **Production-loss costing (decided 2026-09-20)**: where mortality is valued
  by forgone production — human capital, lost earnings, GDP per capita — the
  identification kind is FIXED AGE, specified in B1 by the productive horizon
  (a retirement age, a working-age band, an employment-probability weighting).
  The cause restriction is scope: it fails the removal test, since working
  years lost remains a coherent quantity without it. Exception, by the headline
  rule: where the same article also reports years of life lost counted to a
  life table, that figure leads and the answer follows the table, normally ALL
  DEATHS (worked case: s2art107 choi12). The rule reproduces the twelve FIXED
  AGE codes already in the corpus and makes a correction list of the seven
  production-loss articles coded ATTRIBUTED CONDITIONS or COUNTERFACTUAL
  SCENARIO with an age in B1.
  No new A1 level: the distinction is recoverable post hoc by crossing A1 with
  D1, as the explicit/implicit counterfactual split already is.

## 9. Sampling and reporting

- Purposive, block-wise, BERTopic-guided sample. **Counts describe the corpus,
  never the literature.** No percentages that read as prevalence.
- Saturation is **conditional**: computed over codeable articles, so the NOT
  STATED residue can still add levels; report the NOT STATED rate alongside the
  new-levels-per-block curve.
- If the sampling favoured concept-central articles, absence of defended
  standards is biased **against** the finding; state the direction explicitly.
- Corrections are claim-targeted: verified columns/subsets named in Methods,
  with the correction rate; cells not bearing on a reported claim were not
  re-verified, and the Methods says so.
