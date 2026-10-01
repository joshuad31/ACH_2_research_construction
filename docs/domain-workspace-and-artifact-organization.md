# ACH 2.0 Domain Workspace and Artifact Organization Standard

**Status:** Proposed v0.1 for one PTX pilot, then freeze as v1.0  
**Purpose:** Make an ACH 2.0 domain intelligible to a human or an LLM without mixing scientific artifacts, execution machinery, validation-only material, or different runs.  
**Authority:** This document organizes artifacts required by the current ACH 2.0 specification. It does not add a new evidentiary stage, alter the meaning of an artifact, or authorize a model to ignore the stage-specific prompts.

---

## 1. Design decision

An ACH project is organized as a **domain containing one corpus, one or more isolated runs, separate blind-validation workspaces, and one or more deliberately assembled releases**.

This resolves four different needs without forcing them into one flat folder:

1. **Domain continuity:** the corpus and durable project description can be reused.
2. **Run isolation:** questions, responses, FRDs, witnesses, language records, coverage sets, and crux results from different runs never become one identity by accident.
3. **Role separation:** a blind validator receives a validation-only workspace rather than the full research project.
4. **Human publication:** a release is an intentionally assembled reading copy, not a dump of runtime files.

The numbered folders represent the conceptual research sequence. Method files and operating machinery are placed after that sequence rather than interleaved with the evidence.

---

## 2. Governing rules

### 2.1. One canonical home

Every artifact has one canonical home. Indexes and reports link to that artifact; they do not silently create a second authoritative copy.

Copies are permitted only in:

- a deployed blind-validation workspace;
- a frozen public or expert-review release; or
- an explicitly identified archive or fork.

Every permitted copy records its source artifact ID or canonical relative path.

### 2.2. Run-local identity

Every run has its own questions, responses, candidate FRDs, validation results, validated FRDs, witnesses, language artifacts, matching records, coverage sets, and crux records. Two runs may reuse material by explicit reference, but their records are not merged.

### 2.3. Human path and machine index

Human-readable folders answer **where should I look?** Machine-readable registries answer **what exists, what is its status, and what does it depend on?** Neither replaces the other.

### 2.4. No hidden completion

An empty stage folder is labeled `NOT_STARTED`, `READY`, `IN_PROGRESS`, `BLOCKED`, or `COMPLETE` in the run status. The existence of a folder never implies that the stage was performed.

### 2.5. No exploratory hashing gate

Hashing is not a prerequisite to begin discovery or FRD work. Where the current specification requires immutable identity, dependency tracking, or a frozen release after FRD creation, the registry records the relevant hash. Missing platform information is marked unavailable. Folder organization must not become a throughput-blocking ritual.

### 2.6. Preserve failures in place

Failed, repaired, unavailable, unresolved, and withheld records remain in the stage that produced them with an explicit status. Do not hide them in a miscellaneous folder.

### 2.7. Separate working project from release

Never upload the entire working root as the public or expert-review package. A release is built from an allowlist and excludes secrets, browser state, temporary files, caches, private credentials, and unrelated archives.

---

## 3. Canonical domain tree

```text
ACH-DOMAIN/
├── README.md
├── START-HERE.md
├── DOMAIN-MAP.md
├── 01_CORPUS/
│   ├── README.md
│   ├── manifests/
│   ├── source-files/
│   ├── conversion-records/
│   ├── unavailable-sources/
│   └── provenance/
├── 02_RUNS/
│   └── RUN-<stable-run-id>/
├── 03_VALIDATION-WORKSPACES/
│   └── FRD/
│       └── RUN-<stable-run-id>/
│           └── BATCH-<stable-batch-id>/
├── 04_RELEASES/
│   └── RELEASE-<stable-release-id>/
├── 90_METHOD/
│   ├── specifications/
│   ├── prompts/
│   ├── templates/
│   ├── guides/
│   ├── tools/
│   └── runtime/
└── 99_ARCHIVE/
```

### Root navigation files

- `README.md` — what the domain is and what claims it does not make.
- `START-HERE.md` — the shortest path for the next operator: current run, current stage, exact next action.
- `DOMAIN-MAP.md` — links to the corpus, each run, each validation workspace, and each release. It is a map, not a scientific conclusion.

Each run's `RUN-CONFIG.json` pins one exact corpus-manifest identity and path. Source files may be physically shared, but additions, removals, replacements, or material conversion changes create a new manifest version. A shared corpus therefore does not silently change an earlier run.

---

## 4. Canonical run tree

```text
02_RUNS/RUN-<stable-run-id>/
├── RUN-MAP.md
├── RUN-STATUS.md
├── RUN-CONFIG.json
├── 00_RUN-CONTROL/
│   ├── artifact-registry.jsonl
│   ├── intake-and-readiness/
│   ├── model-and-human-decisions/
│   ├── batch-manifests/
│   ├── prompt-snapshots/
│   └── exceptions-and-disagreements/
├── 01_FRAME/
│   ├── research-question/
│   ├── hypotheses/
│   ├── header/
│   ├── index/
│   └── coverage-units/
├── 02_DISCOVERY/
│   ├── 01_issued-questions/
│   ├── 02_query-responses/
│   ├── 03_quest-state/
│   ├── 04_ach-eval-checkpoints/
│   ├── 05_feedback/
│   └── 06_closeout/
├── 03_FRDS/
│   ├── 01_candidates/
│   ├── 02_harvest-accounting/
│   ├── 03_validation-deployments/
│   ├── 04_validation-results/
│   ├── 05_validated/
│   └── 06_source-assignment-audit/
├── 04_LANGUAGE-TOOLS/
│   ├── 01_vocabulary-harvest/
│   ├── 02_dictionary/
│   ├── 03_canonicalizer/
│   ├── 04_transcoder/
│   └── 05_conformance-tests/
├── 05_WITNESSES/
│   ├── 01_question-applications/
│   ├── 02_raw-witnesses/
│   ├── 03_fidelity-reviews/
│   ├── 04_repaired-or-held/
│   └── 05_released/
├── 06_TRANSCODING/
│   ├── 01_hypothesis-inputs/
│   ├── 02_witness-inputs/
│   ├── 03_binding-records/
│   ├── 04_rewrite-traces/
│   └── 05_released/
├── 07_MATCHING/
│   ├── 01_hypothesis-units/
│   ├── 02_match-fixtures/
│   ├── 03_match-records/
│   └── 04_disagreements-and-review/
├── 08_COVERAGE/
│   ├── 01_coverage-options/
│   ├── 02_coverage-sets/
│   ├── 03_removal-certificates/
│   └── 04_search-status/
├── 09_CRUX/
│   ├── 01_frozen-rival-theories/
│   ├── 02_membership-screening/
│   ├── 03_portability-tests/
│   ├── 04_certificates/
│   └── 05_candidates/
└── 10_REPORTS/
    ├── human-summary/
    ├── expert-review-packet/
    ├── public-argument/
    ├── source-access-record/
    ├── fork-record/
    ├── limitations/
    └── release-inventory/
```

The tree follows the current specification's causal chain:

```text
frame → discovery → FRDs → language tools → witnesses → transcoding
      → semantic matching → deletion-minimal coverage → crux → report
```

`00_RUN-CONTROL` is cross-cutting administrative material. It does not become evidence merely because it is in the run.

If Superior Mr. Fusion or a similar intake normalizer is used, its content profile, fragment, acquisition report, and readiness record live in `00_RUN-CONTROL/intake-and-readiness/`. They classify and route material; they do not replace the frame, source records, FRDs, or later results.

---

## 5. Required navigation contract for every stage

Every numbered stage folder contains one short `README.md` with exactly these headings:

1. `Purpose`
2. `Allowed inputs`
3. `Expected outputs`
4. `Current status`
5. `How to verify this stage`
6. `Next handoff`
7. `What this stage does not establish`

The stage README should normally remain under 800 words. Detailed methods belong in `90_METHOD`; actual records belong in the stage folder.

`RUN-MAP.md` links to each stage README. `RUN-STATUS.md` provides a compact table:

| Stage | Status | Count completed | Count held/failed | Last batch | Next action |
|---|---|---:|---:|---|---|

This table is the human checkpoint. The artifact registry is the machine checkpoint.

---

## 6. File and identifier rules

### 6.1. Stable identifiers

Use the identifiers already required by the method. Do not invent a second identity system merely for filenames.

Recommended filename patterns:

```text
Q0001__issued-question.md
Q0001__query-response.md
FRD-Q0001-001__candidate.md
FRD-Q0001-001__validation.md
FRD-Q0001-001-R1__validated.md
APP-FRD-Q0001-001-R1__origin.md
WIT-FRD-Q0001-001-R1__origin.md
BATCH-FRD-0001__manifest.csv
```

The record's internal ID is authoritative. A filename is a readable carrier for that ID.

### 6.2. No generic final filenames

Do not use names such as `final.md`, `new-final.md`, `fixed.md`, or `results2.md`. Use a stable ID, record type, and explicit version or status.

### 6.3. Batch manifest

Each batch has one CSV or JSON manifest containing:

- batch ID;
- run ID;
- assigned role;
- input artifact IDs and paths;
- permitted output folder;
- expected output types;
- actual output IDs;
- held or failed items and reasons;
- operator/model when known;
- start and completion timestamps when available;
- batch status.

A batch manifest is navigation and accounting. It does not replace the scientific records.

---

## 7. Blind FRD-validation workspace

Blind validation is deployed outside the run folder so a fresh Grokbot context can enter one narrow workspace without being invited to explore the hypotheses or discovery history.

```text
03_VALIDATION-WORKSPACES/FRD/RUN-<id>/BATCH-<id>/
├── START-HERE.md
├── VALIDATOR-INSTRUCTIONS.md
├── BATCH-MANIFEST.csv
├── candidates/
├── primary-sources/
└── outputs/
```

The workspace contains only what the short specification permits: candidate FRDs and their lineage metadata, validation-specific instructions and ethos, named primary sources, and an output location. It excludes the hypotheses, header, ranked index, ACH_Eval outputs, query-response text, quest state, stop report, witnesses, coverage, and crux material.

When a batch finishes:

1. copy or import the validator outputs to the run's `03_FRDS/04_validation-results/`;
2. place released repaired/validated records in `03_FRDS/05_validated/`;
3. update the batch manifest and run status;
4. retain the validation workspace as the deployment record or move it unchanged to `99_ARCHIVE` after the release identifies where it went.

The validator never writes directly over a candidate FRD.

---

## 8. Codex–Grokbot operating agreement

### 8.1. Human owner

The human owner selects the research question, authorizes material changes, resolves substantive disputes when able, and decides what is released. The human is not required to hand-sort every generated file.

### 8.2. Codex: project steward

Codex is responsible for:

- maintaining `DOMAIN-MAP.md`, `RUN-MAP.md`, and `RUN-STATUS.md`;
- preparing small batch manifests and exact path-scoped work orders;
- checking file presence, IDs, schema, lineage, and completeness;
- deploying blind-validation workspaces;
- importing Grokbot outputs without silently changing their scientific content;
- identifying discrepancies and routing only substantive decisions to the human;
- assembling an allowlisted expert-review or Google Drive release.

Codex may perform a scientific step only when explicitly assigned that stage under the same stage prompt. Stewardship checks are not a second source-validation verdict.

### 8.3. Grokbot: production worker

Grokbot receives one stage, one batch, one allowed input set, and one output folder at a time. Grokbot is responsible for:

- executing the supplied stage prompt faithfully;
- processing every manifest item or explicitly reporting why it could not;
- preserving IDs and source/QID lineage;
- writing only to the permitted output location;
- returning a completion summary tied to the batch manifest;
- leaving errors, unavailable sources, and unresolved items visible.

Grokbot must not reorganize the project, rename existing canonical artifacts, infer completion from empty folders, or continue into the next scientific stage without a new work order.

### 8.4. Fresh-context separation

FRD creation and blind FRD validation are different Grokbot assignments. A Grokbot context that saw the hypotheses, discovery record, or expected outcome cannot serve as the blind validator. The validator starts in the deployed validation workspace and receives no link back to the full run.

---

## 9. Standard Grokbot work order

Every work order uses this shape:

```text
ROLE
You are performing only: <stage and role>.

RUN AND BATCH
Run ID: <run-id>
Batch ID: <batch-id>

READ FIRST
1. <stage prompt>
2. <batch manifest>
3. <permitted inputs>

ALLOWED INPUTS
<exact files or one exact input folder>

ALLOWED OUTPUT
<one exact output folder>

REQUIRED ACTION
<short stage-specific instruction>

FORBIDDEN
- Do not inspect unlisted folders.
- Do not rewrite or rename inputs.
- Do not perform the next stage.
- Do not hide failed or incomplete items.
- Do not claim completion unless every manifest row has an output or a reason.

RETURN
1. Batch status: COMPLETE, PARTIAL, or BLOCKED.
2. Output artifact IDs and paths.
3. Held/failed items and reasons.
4. Any decision requiring the human owner.
```

The work order stays short because the scientific instructions remain in the stage prompt.

---

## 10. FRD creation and validation plan

### Step 1 — Adopt the map without moving evidence

Create the proposed domain/run maps and a migration table pointing from the present PTX paths to their proposed canonical homes. Do not move or rename the live project yet.

### Step 2 — Pilot one small FRD batch

Use five query-response files in one `BATCH-FRD-0001`. Five is a workload unit, not a scientific threshold. Grokbot receives the installed PTX FRD-creator prompt, the manifest, and only those five query-response files. It creates all candidate FRDs allowed by each file before moving to the next.

### Step 3 — Codex acceptance check

Codex checks only:

- every manifest input is accounted for;
- every candidate has one candidate ID, one producing QID, one claim, and its named source metadata;
- the required adverse/null/gap/condition material was not silently omitted from accounting;
- files are in the proper candidate and harvest-accounting folders;
- no item has been labeled validated.

Content defects are returned to the creator as named repairs. Codex does not silently edit the claim.

### Step 4 — Deploy one blind-validation batch

Codex creates `BATCH-VALIDATION-0001` under `03_VALIDATION-WORKSPACES`, copies the candidate records, installs the PTX blind-validator prompt as `VALIDATOR-INSTRUCTIONS.md`, and places or requests the named primary sources. The fresh Grokbot validator receives only this workspace.

### Step 5 — Import and reconcile

Codex imports all verdicts, repairs, failures, and unavailable-source records. It checks IDs and accounting, creates no substitute verdict, and updates run status.

### Step 6 — Freeze the folder standard

After the first complete creator-to-validator batch, repair confusing folder names once. Then issue this document as v1.0 and stop reorganizing during production. A later structural change requires a versioned amendment and a migration map.

### Step 7 — Continue in bounded batches

Continue with batches of five to ten query-response files, adjusting only for context limits or source size. A batch may fail without invalidating earlier completed batches. This is the error-resistant unit of progress.

### Step 8 — Advance toward witnesses

Begin witness work as validated FRDs accumulate; do not require the entire historical corpus to be perfect first unless a downstream language-tool dependency genuinely requires the frozen full population. Track a PTX operational milestone of 100 fidelity-reviewed, released witnesses. This is a motivating project milestone, not a universal ACH validity threshold and not proof of clinical efficacy.

---

## 11. Mapping the present PTX project without moving it

| Present path | Proposed conceptual home |
|---|---|
| `corpus/` | `01_CORPUS/` |
| `provenance/` | `01_CORPUS/provenance/` or the affected run's `00_RUN-CONTROL/` according to what the record describes |
| `frame/` | `02_RUNS/<run>/01_FRAME/` |
| `artifacts/questions/` | `02_RUNS/<run>/02_DISCOVERY/01_issued-questions/` |
| `artifacts/query-responses/` | `02_RUNS/<run>/02_DISCOVERY/02_query-responses/` |
| `artifacts/quest-state/` | `02_RUNS/<run>/02_DISCOVERY/03_quest-state/` and closeout subfolder |
| `artifacts/coordinator-private/fragments/` | `02_RUNS/<run>/02_DISCOVERY/04_ach-eval-checkpoints/` with role restrictions preserved |
| `artifacts/feedback-packets/` | `02_RUNS/<run>/02_DISCOVERY/05_feedback/` |
| `artifacts/frds/` | `02_RUNS/<run>/03_FRDS/` |
| `artifacts/language/` | `02_RUNS/<run>/04_LANGUAGE-TOOLS/` |
| `artifacts/witnesses/` | `02_RUNS/<run>/05_WITNESSES/` |
| `artifacts/transcoded/` | `02_RUNS/<run>/06_TRANSCODING/` |
| `artifacts/coverage/` | `02_RUNS/<run>/08_COVERAGE/` |
| `artifacts/crux/` | `02_RUNS/<run>/09_CRUX/` |
| `artifacts/reports/` | `02_RUNS/<run>/10_REPORTS/` |
| `Prompts/`, `Specification/`, `Templates/`, `Guides/` | `90_METHOD/` |
| `tools/`, `runtime/`, `archivist/`, `notebooks/` | `90_METHOD/` operational subfolders |
| `NotebookLM throughput strategy/` | `90_METHOD/guides/throughput/` |
| `archive/` | `99_ARCHIVE/` |

Until migration is authorized, the proposed maps may point to these existing paths. A path map is enough to test findability without risking a disruptive move.

---

## 12. Expert-review and Google Drive release

Each release mirrors the run stages rather than exposing the working tree:

```text
04_RELEASES/RELEASE-<id>/
├── 00_READ-ME-FIRST.md
├── RELEASE-MANIFEST.csv
├── REBUILD.md
├── OMISSIONS-AND-LIMITATIONS.md
├── 01_CORPUS/
├── 02_FRAME/
├── 03_DISCOVERY/
├── 04_FRDS/
├── 05_LANGUAGE-TOOLS/
├── 06_WITNESSES/
├── 07_TRANSCODING/
├── 08_MATCHING/
├── 09_COVERAGE/
├── 10_CRUX/
├── 11_REPORTS/
├── 12_METHOD-SNAPSHOT/
├── 13_SOURCE-ACCESS/
└── 14_FORK-AND-CHALLENGE-RECORDS/
```

`00_READ-ME-FIRST.md` tells a reader:

- the exact research question;
- what was completed and what was not;
- the quickest useful reading path;
- where the strongest artifacts and the failures are;
- what claims the release does not establish;
- how to contact the owner if the reader wishes to inspect more.

`RELEASE-MANIFEST.csv` lists every included artifact, canonical source path, run ID, artifact ID, stage, status, and release path. It also lists intentionally omitted required artifacts as `NOT_CREATED`, `NOT_EXECUTED`, `UNAVAILABLE`, `PRIVATE`, or `NOT_SHAREABLE` rather than pretending the release is complete.

For a fork, the release also includes its parent-release identity, fork record, declared changes, per-stage accounting, adoption entries, and any correspondence records. A challenge that performs no rerun is labeled a challenge rather than a counter-run. Inherited validation is labeled inherited, never presented as validation performed by the fork.

If a source cannot legally or practically be shared, release its manifest entry and locator instead of the file. Never include API keys, tokens, private browser data, credentials, or unrelated personal material.

---

## 13. Minimum acceptance test

The organization standard passes its PTX pilot only if a fresh human or LLM can answer all of these questions from `START-HERE.md` and the maps without searching the whole drive:

1. What is the active run and current stage?
2. Where are the exact frame, corpus manifest, questions, and query responses?
3. Which FRDs are candidates, which were validated or repaired, and which failed?
4. Which primary source and producing QID belong to any selected validated FRD?
5. What did Grokbot do in the last batch, and what remains?
6. Where can a fresh validator work without seeing the hypotheses?
7. How many released witnesses exist, and which FRD and question produced each one?
8. Which downstream stages are complete, in progress, blocked, or not started?
9. Which folder is safe to upload for outside review?
10. What limitations prevent the artifacts from being interpreted as proof of clinical efficacy or a completed ACH run?

If those questions cannot be answered, add or repair navigation links and manifests before adding another organizational layer.

---

## 14. What this standard deliberately does not do

- It does not claim that the current PTX run is complete.
- It does not claim that a candidate FRD is source-validated.
- It does not turn ACH_Eval allocations into calibrated probabilities.
- It does not make Grokbot's output correct merely because it is neatly filed.
- It does not require a large confirmatory study before useful incremental artifacts may be produced.
- It does not require the human owner to become a software engineer or records administrator.
- It does not make the 100-witness PTX milestone a universal protocol rule.

Its job is narrower: preserve the conceptual chain, prevent cross-role and cross-run mixing, make partial progress legible, and let another person find the evidence worth reviewing.
