# FRD VALIDATION INSTRUCTIONS — PTX (v2.1b)

Use a fresh context unexposed to the header, hypotheses, questions, responses, intended conclusion, prior verdicts, or downstream artifacts. Check each assigned candidate against only its named source file(s) in the packet. Do not browse, use outside knowledge, inspect other corpus files, or resolve opaque origin/QID references. Report any accidental exposure; do not describe a contaminated check as blind.

Check every clause, attribution, qualification, number, unit, and locator. Transmitted claims establish only the transmitter's report. Never recruit an unnamed source to rescue failure. For `disambiguate`, check every named source separately and record each result; produce one repaired FRD per supported claim per source. Unresolved attribution remains NOT READY. Named parts of one work may supply context; preserve exact locations and speaker.

## Labels and restrictions

- `[CLINICAL]` = human trial, cohort, case series, or systematic review.
- `[PRECLINICAL]` = animal, ex vivo, organ-bath, or in vitro finding.
- `[MECHANISM]` = source-described pathway; distinguish demonstrated from proposed, not itself clinical benefit.
- `[INFERRED]` = extrapolation from cited premises.
- `[NO SOURCE]` = support not located here; a retrieval gap, not proof of absence.

Check provisional labels against the source. Separate inference from source statements. Preserve species/model, route, exposure, units, clinical design, harms ascertainment, null findings, and claim-material source limitations. Do not upgrade mechanism to human benefit.

Use English without translation. Fukabori 1996 has a source-authored English abstract but a Japanese body: locating a Japanese string may confirm the locator, but the validator may not present its own English translation as source text or use it to rescue an English claim. Use source-authored English support or mark the English claim unresolved. MP75-18: use that abstract only, excluding neighboring abstracts. Flag damaged conversion or unseen figures; never invent their contents.

## Text and table checks

Prose inside quotation marks must be verbatim. Use the smallest complete sentence(s) that preserve necessary context. Do not insert an omission mark unless it appears in the source. For every quotation, record an exact searchable phrase and its match count; if OCR or line breaks require normalized-whitespace matching, say so. A zero-match string cannot be presented as a quotation.

For every relied-on table value, reproduce enough of the header and row to establish variable, group, timepoint, unit, and analyzed n. Explicitly distinguish mean from SD/SE, median from spread, baseline from endpoint, absolute from percentage change, and within-group from between-group comparisons and p-values. Check sign direction and arithmetic consistency when the displayed values permit it; label any calculation as the validator's calculation, not source text. Never normalize a suspicious unit or infer a precise value from a graph. Unresolved conversion, unit, denominator, or column ambiguity is material.

## Output for each FRD

**[Original FRD ID]** — preserve opaque origin and producing QID.

1. **Citation** — reference, exact filename(s), location(s), and missing metadata.
2. **Claim** — corrected source-supported wording, including claim-material limitations; otherwise support unestablished.
3. **Source text** — exact supporting or contradicting prose and/or table context under the rules above. Include searchable phrase and match count for quotations.
4. **Verdict** — RIGHT / MOSTLY RIGHT / PARTLY RIGHT / WRONG / NOT FOUND / SOURCE UNAVAILABLE. Evaluate the original candidate and identify every material repair, including numerical role errors.
5. **Provenance** — confirmed or corrected `OWN_RESULT`, `DERIVED_FROM(ancestor)`, or `DERIVATIVE_UNKNOWN`.

## Deliverable

Produce a repaired source-supported FRD with corrected claim, citation, attribution, scope, label, and provenance. A repair must remain within the candidate's factual nucleus; do not replace a failed candidate with an unrelated fact from the source. Preserve changed original wording in the audit explanation.

Assign exactly one readiness state:

- **READY FOR WITNESS CONSTRUCTION** — the repaired FRD and its evidence have no unresolved material defect.
- **NOT READY FOR WITNESS CONSTRUCTION** — faithful compression still requires unresolved material repair.

Verdict evaluates the original candidate; readiness evaluates the repaired FRD. A WRONG candidate may become READY only when a source-supported repair preserves its factual nucleus. NOT FOUND, SOURCE UNAVAILABLE, incomplete source checking, unresolved attribution, or unresolved numerical/table ambiguity is NOT READY.

If a locator fails, search throughout every named accessible source using wording variants before NOT FOUND. Record incomplete searches without a blanket NOT FOUND. Split compound claims when necessary; children retain parent origin, QID, and explicit parent ID. Account for every assigned ID exactly once and report verdict/readiness totals, recurring error patterns, inaccessible files, and held or failed IDs. Do not perform cross-FRD redundancy, source-ranking, hypothesis-relevance, or witness analysis.
