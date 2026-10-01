# A compact illustrative ACH run

This is the worked example Joshua requested: a retrospectively selected and edited collection showing what compact FRDs, checked FRDs, questions and witnesses could look like. **It is an architecture example, not a real ACH run, a meta-analysis, a clinical recommendation, or a scientific conclusion about pentoxifylline.** Selection and question writing used hindsight and project context. The underlying observations come from the supplied corpus; the new organization and question applications are manufactured for this exercise. No historical files were changed.

Start with the [witness database](witness-database.md). Local source and historical-record paths now lead to the [provenance index](provenance-index.md); those underlying files are not in this repository. Each short entry links to exactly one question and one checked FRD. Follow the checked FRD to its cited source locator and short source anchor, or to its candidate counterpart. The [question database](question-database.md) displays both the retrospectively chosen raw question and its controlled-English transcoding. Witnesses themselves have not been transcoded.

## PTX run inputs

These are the latest surviving PTX frame and the selected FRD prompts. They show the concrete instructions behind the historical effort. The compact databases below were reconstructed with hindsight; they are **not** the direct output of one uninterrupted run using these four files.

- [Quest header](run-inputs/quest-header.md)
- [Ranked source index](run-inputs/ranked-source-index.md)
- [FRD creation prompt](run-inputs/frd-creation-prompt.md) — the revised prompt used for the later creation batches.
- [FRD validation prompt](run-inputs/frd-validation-prompt.md) — the selected v2.1b prompt.

The header and prompts are exact copies of the surviving files. The index preserves its text but displays its 111 machine-local source links as filenames, since the source files are not published here.

## What was delivered

The frozen size denominator is **111 original Markdown sources, 4,923,230 bytes**. Sizes below measure these GitHub-ready UTF-8 files, including headings, links and provenance references. The local working files had longer machine-specific links and different byte sizes. No compressed archive sizes, deployment folders or source copies enter these totals.

| Database | Entries | Bytes | Corpus size | Strict maximum |
|---|---:|---:|---:|---:|
| FRDs | 251 | 149,623 | 3.04% | 984,645 bytes, below 20% |
| Validated FRDs, three files together | 251 | 246,829 | 5.01% | 1,476,968 bytes, below 30% |
| Raw witnesses | 251 | 96,225 | 1.95% | 196,929 bytes, below 4% |
| Questions, raw and transcoded forms together | 251 | 102,877 | 2.09% | No requested separate cap |

There are **16 clusters**, **65 cited source files**, and **195 distinct historical candidate origins** behind this selection. **56 entries were newly extracted for the example** and are explicitly marked with a NEW origin. A cited file is not necessarily an independent study. Several findings from one study remain dependent; similar findings in different papers may also share underlying data. No count here is an evidence weight.

Every selected FRD has one matching checked FRD and one witness. The permitted maximum of three witnesses per checked FRD was unnecessary for this example. Witness prose ranges from 17 to 49 words; the maximum allowed is 60. Each witness has exactly one illustrative QID and one checked-FRD parent. The file tables and links are the databases: there is no application, external service, or new deployment framework to operate.

| File | Bytes | Corpus size |
|---|---:|---:|
| [frd-database.md](frd-database.md) | 149,623 | 3.04% |
| [validated-frds-clinical.md](validated-frds-clinical.md) | 89,787 | 1.82% |
| [validated-frds-mechanism.md](validated-frds-mechanism.md) | 80,972 | 1.64% |
| [validated-frds-exposure.md](validated-frds-exposure.md) | 76,070 | 1.55% |
| [question-database.md](question-database.md) | 102,877 | 2.09% |
| [witness-database.md](witness-database.md) | 96,225 | 1.95% |

The four database layers together occupy **595,554 bytes (12.10% of the corpus)**. This guide is additional explanatory material. The size ceilings are ceilings, not quantities to fill.

## What the validation label means here

Every checked entry is labeled **SOURCE_CHECKED_FOR_EXAMPLE**. Authors inspected source context while knowing the broader project and choosing the subset. This does not recreate independent blind validation. Historical READY labels supplied starting material; they did not settle the new check. A short verbatim anchor and a source locator make each record inspectable, while the checked claim preserves the necessary population, comparator, timing, qualification and limitation.

Candidate entries derived from historical records are compact renderings, so some retain errors that their linked checked entries correct. They are not newly manufactured errors. A historical key plus links to the original candidate and validation report preserves the distinction between the old records and this reconstruction. NEW entries are fresh extractions from the supplied sources, with source checks performed for this exercise. Several selected aspects can trace back to one historical candidate; the new F/V/W identifiers distinguish their present applications.

Mechanical checks covered the byte limits, nonempty required fields, existing source paths, historical-key mapping, word limits, exact repeated witness text, and the one-to-one parent chain. All 251 source anchors were found in the corpus after whitespace and Unicode normalization. These checks catch structural mistakes; they do not prove semantic completeness or that the chosen subset is globally optimal. Source-checking and selection remain judgments in this example. Checks used the supplied Markdown conversions, not fresh inspection of the original PDFs; apparent source inconsistencies can therefore include conversion errors.

## How the example was chosen

The working rule was to retain a distinct result or a consequential, source-supported limitation that could answer a useful question in a short witness. Repeated renditions of the same source proposition were consolidated through selection. Animal, cell, nonurinary and uncontrolled findings retained their settings. A null significance result was not rewritten as proof of no effect. Source-specific limits were not generalized into claims about the entire corpus. Important contrary findings were eligible on the same basis as favorable findings.

“Optimal” here means a useful, compact, inspectable selection under the requested constraints. It does not mean a demonstrated mathematical optimum. This was not an exhaustive semantic comparison of all 1,570 candidates. The count target helped size the demonstration; it is not a future scientific stopping rule. The 251 witnesses are a concrete example to inspect and revise, not a quota that every future corpus should meet.

Questions were chosen or rewritten retrospectively, then transcoded into controlled English. The IQ database contains witness-extraction questions operating on checked FRDs; historical QIDs identify the original discovery queries. A substantive change from an old question receives a new IQ identifier. The raw-to-transcoded pair within that entry is intended to preserve meaning. The limited normalization follows the existing rulebook's treatment of locally defined names, endpoints, comparisons, eligibility and thresholds. The complete historical dictionary-building and independent transcoder-review protocols were not rerun. Per-question notes expose the actual transformation; already clear wording can remain unchanged.

Question transcoding helps expose ambiguity. It cannot make an unsupported finding true, turn a different question into the original question, or establish that a witness discriminates among hypotheses. After a validation repair, the practical test is: **can this corrected FRD answer the selected question within 60 words without importing facts or losing a material qualification?** If not, record no witness for that pairing, or explicitly authorize and identify a different question.

## How close the earlier attempt came

The earlier run had substantial reusable material: 121 query responses, 1,570 candidate FRDs, and 339 physical validation batches with output pairs. The audit mapped validation records to 1,001 candidates, including 967 labeled READY; 569 candidates lacked mapped validation output. Completing every dispatched batch therefore did not mean every candidate had been validated. The published validated-FRD folder was empty, although working validation reports contained usable repaired findings. Only two draft witness prototypes were present in the inspected research record.

The compact example demonstrates that a meaningful portion of this material can be organized into bounded outputs. It does not establish a percentage completion of the original ACH process: selection, consistent import, question alignment, witness construction and independent quality checking are substantive work, and hypothesis coverage and crux analysis were not completed here.

The original candidate files occupied 1,294,688 bytes, or 26.30% of the corpus; direct validation RESULTS occupied 2,588,177 bytes, or 52.57%. Those historical result files included quotations and validation commentary, so comparison with this concise checked database measures a changed packaging and selection policy as well as reduced repetition. It is not a measured percentage of semantic duplication. A separate local post-mortem handoff records the prior full audit; that handoff is not part of this publication copy.

Local prompts kept producing plausible records while the collection accumulated repeated findings, repairs, packets and unimported outputs. The original average was about 13 candidate FRDs per query response. Nothing reliably made each new record justify its marginal contribution to the existing collection.

The reconstruction also makes concrete fidelity problems visible. In the [PTX symptom-score example](validated-frds-clinical.md#v0003), standard deviations had been treated as mean improvements. Kaplan's 43.6-versus-33.6-month inconsistency concerns symptom duration, although an earlier Grok summary called it follow-up. Several pelvic-floor studies have different denominators for different outcomes; one global sample size cannot safely be stamped onto every finding. These errors call for compact checks of quantities and scope, not more narrative around the same claim.

## A small organization that could produce this kind of result

Use this folder's seven documents as the output template: one guide, one candidate database, three checked-database volumes, one question database and one witness database. Cluster IDs provide the organization. Keep the original source directory in place and link to it. Do not copy source texts or complete prompt histories into each record. Working dispatch packets can be temporary; accepted records enter these same databases.

The analyst sets the scope and budgets once. A coordinator keeps a short question/cluster ledger and sends bounded work. A curator selects candidate findings against what has already been retained. A separate validator receives the proposed claim and its named source material, without the desired hypothesis result. A witness writer receives one approved question and one checked FRD. These are roles and packet boundaries; they need no new user interface.

For each dispatch, specify a batch ID, assigned entry IDs, named input files, exact output fields, entry/byte allowance and stopping condition. A worker returns entries or a reason for no entry, followed by a one-line assigned/returned count. Reconcile IDs on import. A batch is complete when every assigned ID has an explicit outcome; a stage is complete only when the stage's full assignment ledger reconciles. Failed or missing records remain visible.

The coordinator commits a contribution only after it fits the current collection. A local worker need not read the entire frame or invent its own relevance standard. It receives a small, concrete assignment such as “extract the trial's between-group urinary outcomes with the null endpoint preserved.” The curator can compare that result with existing entries and reject another rendering of the same fact. The validator checks fidelity separately from that relevance decision.

## Short prompts to try next

**Curator.** “Given the assigned source-attributed response, this cluster's purpose and its current compact entries, propose at most four new candidate findings. For each, give its claim, source and locator, producing QID, and the distinct contribution it adds. Return fewer or none when the material repeats existing findings. Preserve adverse results and limitations. Do not invent evidence or extend the source's scope.”

**Validator.** “Check this candidate against its named source. Return the supported/repaired claim, a short exact source anchor and locator, material repairs, and READY or NOT READY with a reason. Keep population, comparator, route, dose, timing, uncertainty and interpretation distinct. An original verdict and the repaired claim's readiness are different fields. Do not judge which hypothesis should win.”

**Question normalizer.** “Preserve this question's meaning while making actors, treatment, comparator, endpoint and scope explicit. Expand only locally defined abbreviations. Show original and controlled-English versions and describe any change. Do not repair a mismatch by silently asking a different question. Mark a needed substantive revision for a new QID.”

**Witness writer.** “Using only this one checked FRD, answer this one controlled-English question in at most 60 words. Keep any qualification necessary to interpret the answer. Give exactly one parent QID and one parent checked-FRD ID. Return NO_FAITHFUL_ANSWER if the pair cannot support a useful answer within the limit. Do not add a causal explanation, corpus-wide absence claim or hypothesis verdict.”

**Collection reviewer.** “Compare the proposed entries with the retained collection. Identify repetitions, lost qualifications and missing contrary findings. Retain an additional entry only for an explicit distinct contribution. Keep different studies and genuinely different conditions distinguishable; repeated citations are not independent corroboration. Report remaining gaps rather than filling them with background.”

These prompts are starting rules inferred from the example. They have not been shown to reproduce it prospectively. Requiring another model to recreate the exact wording would test memorization of the example; a useful test would ask whether it preserves comparable distinctions, fidelity and size under the same constraints.

## Guardrails and stopping

For the next trial, calculate byte ceilings from the frozen source files before work starts. Give each batch a share of the remaining allowance. Check limits before importing its output. A count or byte breach returns to collection selection; do not remove important qualifications merely to squeeze text under a limit. If adequate coverage cannot fit, stop with a specific unresolved gap and request one scope/budget decision.

Start with at most four candidates per response as a provisional anti-proliferation rule, then enforce collection-wide distinctness. Four is not scientifically privileged and does not prevent repetition across responses. Reuse an existing fact's ID when another question retrieves it; keep the additional question association without copying the full record. A materially different study population, comparator or outcome can justify a distinct entry.

Use a small mechanical check for unique IDs, existing parents, assigned/returned reconciliation, complete file bytes and witness word counts. These checks are suitable for automation. Ask the human only about substantive ambiguity, scope changes or unresolved evidence, with the relevant small packet. Routine bookkeeping should not require an analyst with a checklist to supervise each batch.

Keep retrieval priority separate from evidentiary support. An A-ranked source is not automatically more trustworthy, and repeated sentences from one study are not independent support. Every witness must be supported by its own parent record; correct IDs and a compliant word count do not prove that relationship. Never enforce a word limit by chopping off the end of a claim.

Stop this exercise at the requested databases. No witness transcoding, coverage sets, crux claims, new discovery, or deployment application were needed to make the example concrete.

## Ideas worth testing later

First test these short prompts on a small held-out slice under the same output budget. Give the outputs to a reviewer who is not told which generation method produced them, alongside separate source-fidelity checks. Compare lost qualifications, useful distinctions retained, repeated propositions, bytes and human interventions. Do not optimize on bytes alone.

If that works, add an incremental dictionary containing only ambiguities actually encountered. Store a current flat version and small changes separately; avoid copying the entire history forward. Test question normalization against near misses before making language-tool completion a prerequisite for every ordinary-English witness.

Later, witness transcoding and coverage sets deserve their own bounded experiment. Deletion-minimal means that no member can be removed without breaking the specified coverage; it does not mean a uniquely smallest set. Useful coverage requires defensible semantic mappings and may return gaps. None of that is established by this folder.

The immediate next step is to inspect this example and revise the few rules responsible for concrete defects. A UI or elaborate deployment system can wait until those rules repeatedly produce acceptable compact collections.
