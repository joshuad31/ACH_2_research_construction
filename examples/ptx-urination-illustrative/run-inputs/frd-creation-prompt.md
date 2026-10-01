# FRD GENERATION INSTRUCTIONS — PTX

Extract candidate claims about pentoxifylline, impaired voiding, bladder/detrusor function and pelvic-floor interventions from the assigned saved Archivist query-response files. Responses are discovery material, not evidence. Save candidates and harvest review to the assigned collision-safe files under `artifacts/frds/candidates`.

Process one query-response file at a time and finish its harvest before moving on. One FRD states one claim with exactly one producing QID. Never combine responses. Report missing QIDs; never invent them.

Anchor each claim to one source where possible. Split separately attributed clauses. If the same claim is explicitly separately attributed to multiple sources, create one candidate per source. If citations do not reveal which source supports which clause, retain all named candidate sources and set `disambiguate`; never guess or discard unresolved attribution. Record exact cited parts; separate files do not prove independence.

Preserve speaker, qualifications, conditions, quantities, adverse findings, nulls and limitations. Separate source findings from reports of other authorities. Do not convert response synthesis into source testimony or invent filenames/locators.

## Labels and restrictions

Preserve these provisional response labels and meanings:

- `[CLINICAL]` = human trial, cohort, case series, or systematic review.
- `[PRECLINICAL]` = animal, ex vivo, organ-bath, or in vitro finding.
- `[MECHANISM]` = source-described pathway; distinguish demonstrated from proposed, not itself clinical benefit.
- `[INFERRED]` = extrapolation from cited premises.
- `[NO SOURCE]` = support not located here; a retrieval gap, not proof of absence.

Source-attributed findings and interpretations are candidates, regardless of apparent mislabeling; flag suspected errors. For `[INFERRED]`, extract separately sourced premises where available. Unsupported synthesis and `[NO SOURCE]` gaps belong in harvest review, not evidence of absence. Labels establish neither truth nor an authority hierarchy.

Use English without translation. Fukabori 1996: originally published English abstract only. MP75-18: that abstract only, excluding neighboring abstracts. Cite exact source filename and heading, adding reliable page/table or exact search phrase when needed; citation bubbles alone are insufficient. Never invent quotations or locators; flag damaged conversion or unseen figures.

Keep species/model, route, dose/concentration, parent PTX/metabolites, rapid/slower effects and prevention/reversal distinct. Preserve clinical design/population, exposure assumptions, pelvic-floor program/adherence distinctions and harms limitations; unreported events are not zero.

## Entry format

Use neutral clusters such as measurement, pharmacology, tissue response, timing and limitations. Assign globally unique IDs in the form **FRD-[QID]-[CLUSTER]-[NN] — [short label]**; for example, `FRD-Q0002-MECHANISM-01`. Do not reuse an ID within or across QID files.

1. **Origin** — exact response filename/reference and one producing QID.
2. **File and location** — exact source and locator; every named candidate for `disambiguate`.
3. **Candidate claim** — one or two sentences, one proposition, no strengthening.
4. **Verification instruction** — passage, number, attribution or qualification to check; original label and suspected error.
5. **Provenance** — provisional `OWN_RESULT`, `DERIVED_FROM(ancestor)` or `DERIVATIVE_UNKNOWN`.
6. **Status** — `ordinary`, `disambiguate` or `needs-source` when no usable citation exists.

## Harvest review

List every processed response, FRD counts, disambiguate/needs-source counts, unresolved citations/labels and unextracted candidates with reasons. List required source filenames by cluster and cited sources yielding no FRDs. Distinguish gaps and unsupported synthesis from extracted claims. Preserve parent history when noting repeated support.
