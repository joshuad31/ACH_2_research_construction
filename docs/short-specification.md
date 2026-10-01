# Claim Registry ACH 2.0 — Short Specification

> Publication note: Paths to separate pilot implementations and playground records below are project locators, not links to files in this repository.

### Scope

**One project · one logical corpus · one retrieval database · one Archivist · one ranked index · one Discovery Quest Header · one Investigator · one Coordinator.**

Out of scope: multi-database, sharding, federated retrieval.

- The specification imposes no numerical source ceiling. Corpus size is a configuration matter bounded by the deployed retrieval service.
- The logical Archivist may be served through several authorized copies of the same corpus and custom instructions. Copies provide concurrent capacity; they create no independent evidence and no additional sources.

### What It Does

**Hard question + pile of sources → human-written competing hypotheses · Coordinator-led query-response quest assessed by ACH_Eval · source-validated FRDs · question-compressed witnesses · transcoded hypothesis and witness text · deletion-minimal hypothesis coverage sets · crux candidates.**

Every witness traces through a validated FRD to a source passage and through the question metadata that produced it. The whole run is re-runnable.

What it is **NOT:** not a truth machine. It is a process for distillation, comparison, and audit.

### What's Structurally New

*Key features:*

1. **Private-frame isolation** — Archivist receives the query, not the header, index, or hypothesis labels.
2. **Second, separate blind validation** — each fact vs. only its own source file.
3. **One custom dictionary, canonicalizer, and transcoder** for both witnesses and hypotheses before comparison.
4. **Every issued question is preserved** with its source selection, query-response round, and pointers to every FRD and witness descended from it.
5. **Every FRD receives exactly one producing question ID**, and that quest question is reused to compress the validated FRD into a witness.
6. **Hypothesis coverage sets are compared** to identify the witnesses rival hypotheses cannot accommodate.
7. **Final output** identifies the crux candidates in a human-readable report of fewer than 4,000 words.
8. **A Coordinator directs discovery and owns stopping**, assessing the quest with ACH_Eval, which carries the cumulative evidence record forward between checkpoints.
9. **Crux identification combines coverage-set membership screening with solver tests against a frozen rival theory.**

### Information and Responsibility Boundaries

| Role | Receives and performs | Does not receive or perform |
|---|---|---|
| **Coordinator** | Approved header and index, source manifest metadata, operational records, saved answers, and ACH_Eval; launches and directs the Investigator, controls checkpoints and stopping. | Reads no primary-source bodies in discovery; runs no blind source validation in its hypothesis-exposed context. |
| **Investigator** | Approved header and index, saved answers and qualitative research state, and Coordinator priorities; writes questions, owns submission and exact capture. | Receives neither ACH_Eval nor its allocation or scoring record; does not update allocations or decide a threshold was met; reads no primary-source bodies. |
| **Archivist** | Corpus, fixed topical/citation instructions, and one source-grounded question at a time; returns attributed source information. | Receives no header, index, hypothesis labels, allocations, source ranks, research state, or investigative role. |
| **Later source validator** | One candidate FRD and its named source, under the blind-validation rules. | Receives no hypothesis frame, quest assessment, or preferred outcome. |

Coordinator and Investigator are separate working contexts; one model may implement both in separate instances. Logical separation is required, different providers are not. ACH_Eval runs inside the Coordinator's assessment role, and the Coordinator is the sole assessment and stopping authority.

The Investigator should be highly motivated. Questions use topical language and named sources, without internal hypothesis labels or ACH scoring requests.

---

## Vocabulary to Define Up Front

### Core Definitions

**Source** — underlying item. Not an LLM summary of it.

**Source file** — its Markdown conversion + stable ID. What gets ingested, what validators read.

**Corpus** — all admitted source files. Not a source. Not a database.

**Eligibility** — primary *relative to this investigation*. Depends on question, not document type. *Example: drug label secondary to pharmacology, primary to failure-to-warn. Secondary not banned; doubtful ones flagged at validation.*

**Retrieval database** — the one database (NotebookLM). Disposable, rebuildable. Not system of record.

**Investigator** — uses the header, ranked index, and Coordinator feedback to write questions and conduct the quest. Has no access to ACH_Eval or primary-source bodies.

**Archivist** — the database. Gets corpus + fixed citation/format instructions + one source-grounded query. Never: header, index, hypotheses, ranks, goal.

**Archivist instructions** — database's citation/format rules. Not the header. No hypotheses.

**Ranked index** — one catalogue, every source file, A/B/C/F + relevance notes. Guidance, never evidence. Available to Investigator and Coordinator.

**Discovery Quest Header** — one frozen instruction set: question, hypotheses, evidence rules, stopping rules. Available to Investigator and Coordinator.

**Run** — the full sequence beginning after the corpus, index, and header have been prepared: quest query-response rounds → FRD creation → blind FRD validation → custom-dictionary and language-tool creation → question-guided witness extraction → transcoding → deletion-minimal hypothesis coverage sets → crux identification.

**Question database** — the run-specific, durable database of every question actually issued during the Investigator's quest. Every question record has one unique question ID (`QID`), is never merged with another question record, and remains available for later witness creation.

**Private quest state** — the Investigator-side working record required by the frozen Discovery Quest Header. The header defines its exact fields, update rules, question-selection use, and stopping use. It is never sent to the Archivist and is not evidence by itself.

### Language and Representation Tools

**Custom dictionary** — the run-specific collection of reviewed contextual senses of recurring terms in validated FRD claims. Comparison with ordinary-English frequency is a diagnostic for selecting and prioritizing review, not a decision about meaning.

**Canonicalizer** — a language tool built with the custom dictionary to reduce the number of grammatical constructions used during comparison and to encode the dictionary's custom terms.

**Transcoder** — the English-to-English encoder built from the canonicalizer and applied to witnesses and hypothesis statements.

**Reference English corpus** — a large, versioned collection of ordinary English used only to estimate how common a word normally is. It is not part of the investigation's evidence corpus.

**Base word form** — the form under which grammatical variations are counted together, such as counting `offer`, `offers`, and `offered` under `offer`. Every original form remains preserved in its sentence.

**Relative frequency** — the word's rate in the validated FRDs divided by its rate in the reference English corpus. A value greater than one means the word appears more often in the FRDs than in ordinary English.

**Occurrence** — one recorded use of a word in one validated-FRD sentence, together with the local text needed to understand that use.

**Contextual sense** — the meaning a word has in a particular group of occurrences. One written word may have several contextual senses that must remain separate.

**Sense group** — occurrences judged to use a word with the same contextual meaning. A sense group is the source material from which one `WORD (modifier)` dictionary entry is created.

**Dictionary binding** — the recorded decision that a particular word occurrence in a witness or hypothesis uses one particular custom-dictionary entry. If the context does not identify one entry safely, the binding remains unresolved.

**Scoped alias** — an approved alternate wording for one dictionary entry that may be used only in its recorded source, passage, or contextual scope. It is not permission for global replacement.

**Canonical form** — the one preferred word form or grammatical construction selected for consistent use in the run's controlled English. Selecting a canonical form standardizes expression; it does not declare the underlying claim true.

### Semantic and Logical Properties

**Referent** — the person, object, passage, event, or idea to which a name, noun phrase, or pronoun points.

**Polarity** — whether a statement affirms something or denies it.

**Modality** — how a statement presents possibility, probability, uncertainty, or necessity; for example, the difference between `may occur` and `must occur`.

**Protected property** — a part of meaning that canonicalization and transcoding are forbidden to change, including:
- Who said or did something
- Affirmation or denial
- Uncertainty, conditions, and alternatives
- Identity or role
- Time, quantity, and scope

**Controlled grammar profile** — the versioned house-style rules that state which grammatical constructions the canonicalizer prefers, which it rejects, and which require review.

**Normalization preview** — a side-by-side display of original and proposed controlled-English text, with every dictionary substitution and grammar change identified before approval.

**Conformance** — whether an artifact follows its frozen dictionary and grammar rules while preserving every protected property. Conformance is compliance with the language rules, not proof that the text is true.

**Semantic matching** — comparison of meaning rather than spelling alone. Here it asks what relationship the approved transcoded witness text has to the approved transcoded hypothesis text.

### Coverage Concepts

**Coverage option** — either one witness that completely covers one `REQUIRED_SUPPORT` unit or an approved group of partial matches that covers the unit only when used together. A grouped option does not merge its witnesses.

**Removal certificate** — the recorded reason a witness cannot be deleted from a coverage set: a required unit would become uncovered, an approved joint-coverage group would break, or a necessary dependency would fail.

**Exhaustive enumeration** — a search that checked every available coverage-option combination under the frozen inputs and constraints.

**Resource-bounded enumeration** — a search stopped by a declared time, cost, or attempt limit. Its verified results remain valid, but additional results may still exist.

**Coverage unit** — an internal matching representation derived from the human-written hypothesis after the human approves it. Humans write ordinary hypothesis sections; they are never instructed to think or write in units.

**`REQUIRED_SUPPORT` unit** — a part of the written hypothesis that must receive affirmative witness coverage before the hypothesis has complete coverage.

**`CONTEXTUAL_CONSTRAINT` unit** — an assumption, antecedent condition, boundary, or qualification that every proposed coverage set must continue to satisfy.

**`ADVERSE_TEST` unit** — a recorded condition or finding that could count against or falsify the hypothesis. It remains visible but is not mandatory affirmative coverage.

**`CORROBORATING_EXPECTATION` unit** — a finding the hypothesis leads the analyst to expect. It remains visible but is not automatically a required-support unit.

### Semantic Matching Relations

**`EQUIVALENT`** — the witness and coverage unit express materially the same claim at the same strength and scope.

**`WITNESS_ENTAILS_UNIT`** — if the witness is accepted as written, the coverage unit follows from it; the witness is at least as strong and specific as the unit.

**`UNIT_ENTAILS_WITNESS`** — the coverage unit would imply the witness, but the witness is weaker or less specific than the unit. This is relevant partial support, not complete coverage.

**`PARTIALLY_COVERS`** — the witness supplies a material part of the unit but neither text implies the other completely. Several such witnesses may cover the unit only through an approved jointly sufficient group.

**`CONTRADICTS`** — the witness and unit cannot both be accepted as written under the same recorded scope and conditions.

**`NO_SEMANTIC_RELATION`** — no material support, contradiction, or partial-coverage relationship was found between the two texts. This label says nothing about whether their sources are independent.

**Match trace** — a short explanation identifying the exact words, grammatical structures, and protected properties that justify a semantic-matching relation.

**Adversarial fixture** — a deliberately difficult test pair in which wording remains similar while one meaning-bearing feature changes, such as reversing the actor and object. It tests whether the language tool follows meaning instead of superficial resemblance.

**Jointly sufficient** — two or more partial matches together provide complete coverage that none provides alone. The exact approved group must be recorded, and its witnesses remain separate artifacts.

### Status and Resolution Labels

**`ABSTAIN`** — the system declines to make the requested judgment because the available text or rules do not support a reliable decision. It is an honest unresolved result, not a failed attempt disguised as an answer.

**`REQUIRES_REVIEW`** — an automated step found a specific ambiguity or rule failure that a human must resolve before the artifact may continue.

**`APPROVED_EXCEPTION`** — a human-approved departure from the controlled grammar profile, recorded with its reason and scope. It does not change the general rule.

**`NO_COMPLETE_COVERAGE`** — the matching record contains no allowed witness option for at least one required part of the hypothesis, so no complete hypothesis coverage set can currently be built.

### Search and Enumeration

**Finite enumerated pool** — a fixed list in which every eligible item is known and can, in principle, be checked. Any recall estimate applies only to that frozen list.

**Open-world saturation** — a stopping judgment for discovery when recent searches produce no material additions under the recorded routes. It never means that all external literature has been found.

**Hybrid stopping** — separate reporting of progress in a finite known pool and progress in open-ended discovery.

### Source Provenance

**`OWN_RESULT`** — the source presents the claim as resting on its own data, observation, or argument.

**`DERIVED_FROM(ancestor)`** — the source explicitly repeats, cites, or depends on an identifiable earlier source for the claim.

**`DERIVATIVE_UNKNOWN`** — the source appears to depend on earlier material, but the ancestor cannot be identified from the available text.

**`BETTER_SOURCE_AVAILABLE`** — after blind validation is locked, a comparison finds another available source that anchors the claim more directly or appropriately.

**`REDUNDANT_WITH`** — a second artifact repeats the same underlying support without adding an independent source contribution. The artifact is preserved; the label prevents false corroboration.

**`INTRA_SOURCE_TENSION`** — two passages or witnesses from the same source appear to pull in different directions. The tension is recorded without pretending that two independent authorities disagree.

### Coverage and Crux

**Complete coverage** — the selected witnesses collectively represent every `REQUIRED_SUPPORT` unit; each `CONTEXTUAL_CONSTRAINT` remains satisfied; and adverse-test and corroborating-expectation results remain visible without becoming mandatory affirmative coverage.

**Deletion-minimal hypothesis coverage set** — a witness set that has complete coverage and contains no approved incompatibility. Test it by trying to delete each witness one at a time. The set is deletion-minimal only if every attempted deletion either leaves part of the hypothesis uncovered or breaks a necessary dependency.

*Note: "Deletion-minimal" does not mean that it is the smallest possible set by witness count, the only valid set, or the strongest-evidence set. Several different deletion-minimal sets may completely cover the same hypothesis.*

**Excluded witness** — a witness a rival hypothesis cannot accommodate: asserting it makes the rival's requirements unsatisfiable, or satisfiable only at the cost of complete coverage.

**Crux candidate** — a witness belonging to a home coverage set, passing membership screening against a rival, and failing both portability tests against that rival. More than one candidate may exist.

**Crux strength** — the count of the two portability tests a witness fails against a rival, and the number of rivals against which it fails both. Discrete, not a continuous score.

**Frozen rival theory (`B_H`)** — a machine-readable compilation of one hypothesis's coverage requirements, contextual constraints, necessary dependencies, and approved incompatibilities, fixed and versioned before testing. It implicitly contains every valid coverage set for that hypothesis, including sets no enumeration has reached.

**Portability test** — two solver questions: whether the witness is consistent with the rival's asserted units and contextual constraints (T1), and whether complete rival coverage remains possible using options that do not conflict with the established witness (T2).

**Certificate** — a machine-checkable record of why a test result holds: an example arrangement for an accommodated witness, the specific conflicting rule bundle for one that cannot be accommodated. A result without a certificate is not accepted.

**False-crux error** — treating a witness as a crux when a missed match or unformed valid rival set hides how the rival could accommodate it. Reliability depends on the approved matches and faithful compilation of the frozen theory.

---

*Everything else (FRD, witness, matching, scoring) — define at first use.*

---

## Governing Principles

- Write the specification so a smart college senior can read it. Use a specialized term only when it does necessary work, define it in plain language in the glossary or at first use, and keep the surrounding instructions free of unnecessary academic vocabulary.

- Before importing a term from outside literature, test whether its contextual meaning would be immediately clear to the intended reader. If not, add a plain-language glossary entry before using it in an instruction.

- **Keep required outcomes separate from proposed implementations.** When the protocol needs a function but the method is not yet understood or tested, state the requirement, mark the implementation unresolved, and link an implementation companion. Do not turn a research idea into a mandatory procedure merely to fill an empty module.

- Keep the main specification focused on stable inputs, outputs, non-negotiable rules, failure conditions, and known module status. Store experimental algorithms, long prompts, design alternatives, and research notes in linked companion documents.

- **Conclusions = "best understood from this corpus, this run." Never "settled."**

- **The human approves the complete hypotheses before discovery.** Models may assist with drafting and proofreading.

- **Authority is a cultural and sociological status** that exists outside ACH. ACH is blind to authority; a human analyst may evaluate authority after the core analysis.

- No count or prestige as a silent tiebreaker.

- "No conflict found" ≠ "proven compatible."

- Supporting and adverse evidence — identical treatment and visibility.

- Material change → new version. Old artifacts stay inspectable.


---

# PHASE I — Define the Run, Build the Corpus

### 1. Suitability

- Three admit conditions: contestable answer · strongest evidence for ≥1 hypothesis can go in corpus · everything relevant convertible to Markdown.
- Declare private or publishable.
- Output: criterion-by-criterion findings, not one verdict.

### 2. Mr. Fusion

- Pre-run tool used only before the header is created and frozen.
- Helps humans specify better deep-research queries for acquiring primary sources and understanding the subject.
- Helps organize the researcher's materials and prepare the information needed to construct the corpus, index, hypotheses, and header.
- May assist with hypothesis formulation; the human approves the result.
- Once the header is created and the quest begins, Mr. Fusion is no longer needed and has no role in the run.
- Its detailed reference implementation is stored under `reference materials/Tools for ACH`.

**2.1. Hypothesis formulation**

- The human analyst approves every complete hypothesis before the quest.
- Mr. Fusion may assist with selection and formulation. An LLM may proofread the result and provide quality-assurance feedback.
- A concise hypothesis statement may be about 30 words, but that is not enough semantic surface area for multiple witnesses to match against it.
- Every written hypothesis therefore contains at least four sections: a concise hypothesis statement · assumptions and antecedent conditions · potential falsification context · potential corroboration context.
- Additional sections may be added later, but they are not yet specified.
- The human-readable written hypothesis remains the controlling statement. Coverage units are created only afterward as an internal matching representation.
- Never instruct a human to write or think in fact atoms or coverage units.
- ACH does not determine whether a source or witness is authoritative. Authority belongs to later human analysis.

**2.2. Internal coverage representation**

- After the human approves and freezes the hypothesis, an LLM may derive coverage units from the four human-written sections for matching purposes.
- `REQUIRED_SUPPORT` units represent what must be supported for the hypothesis to receive complete affirmative coverage.
- `CONTEXTUAL_CONSTRAINT` units express assumptions, antecedent conditions, boundaries, or qualifications that must remain satisfied.
- `ADVERSE_TEST` units preserve the potential falsification context.
- `CORROBORATING_EXPECTATION` units preserve the potential corroboration context.
- Unit creation may clarify and tag what the human wrote but may not introduce a new factual commitment or rewrite the hypothesis.
- Coverage units are never presented as the way a human must formulate a hypothesis.

### 3. Source Discovery

- One unified pass, both domains.
- Domain P / Domain S = conceptual labels, not storage. Everything into one database.
- **Departure from v4.1:** v4.1 gathered domains separately, bridge hidden from search model. Four reasons: separation doesn't survive the architecture · blind Archivist + blind validation catch the bias downstream · citation-graph expansion recovers misses · combined collection never shown to hurt.
- **Cost to state plainly:** unified pass is hypothesis-aware, can skew. Separated acquisition still permissible.

### 4. Acquisition

- Convert → Markdown. Stable IDs. Provenance + shareability.
- Catch duplicates, OCR garbage. Keep unavailable-source list.
- **Out:** one corpus, one manifest.

### 5. Provisioning

- Load all into one database. Verify IDs match + ingestion succeeded.
- Doesn't fit → stop, report out of scope. Don't split.

### 6. Ranked Index

- One index. Every file once. A/B/C/F by usefulness to *this* question.
- Entry = 100–250 words: filename · author/year/title · relevance · faithful summary · contradictions and gaps.
- **Ranks guide attention. Never evidence.**

### 7. Completeness Check

- Three-way match: manifest ↔ files loaded ↔ index entries.
- Hunt: missing source families, comparators, adverse evidence, malformed IDs, bad ranks.
- Fix before freeze. After freeze → new version.

**7.1. Stakeholder challenge**

- Ask participants: any outside fact that changes how existing evidence reads?
- Silence buys "nothing disclosed this run." Never completeness.

### 8. Question Database and Query-Response Records

- Create a question database for the run. It is populated during the quest from questions actually issued by the Investigator.
- Assign every saved question one unique, permanent `QID` before or when it is submitted to the Archivist.
- **Never merge question records.** Even if question texts appear similar, each issued question remains the record of its own query-response round in its own run.
- Preserve every issued question and its Archivist response as one query-response round.
- Each question record must contain:
  - run ID
  - `QID`
  - round number and issue order
  - exact question text
  - issue time
  - one-to-three specified source IDs
  - frozen header version
  - response ID
  - exact Archivist response
  - cited source and passage identifiers
  - every candidate-FRD and validated-FRD ID descended from the response
  - every question-application and witness ID descended from that question
  - links to the applicable reproducibility records
- Coordinator and Investigator share the header, index, and research state. Send the Archivist only the source-grounded question and source identifiers. ACH_Eval and its numerical record remain with the Coordinator.
- **Multiple FRDs may share the same `QID`**, because one query-response round may produce several FRDs.
- **An FRD may never carry more than one producing `QID`.**
- The same quest questions later provide the current method for compressing validated FRDs into witnesses.

### 9. Header + Freeze Gate

- One complete operational header: mission, approved hypotheses, decisive tests, query rules, quest loop, coverage, and Coordinator-owned stopping. Later pipeline instructions remain separate.
- Create the header from the ranked index with assistance from Mr. Fusion after the human has approved the hypotheses.
- Build it with the [combined Quest Header generator and template](../prompts/quest-header-generator.md). Do not duplicate the ranked index or later pipeline instructions.
- **Freeze together:**
  - header
  - human-written hypotheses
  - internal coverage representation
  - index
  - manifest
  - database identity
  - prompts
  - configuration
  - question-database and query-response record formats
  - reference English corpus identity
  - dictionary-selection, canonicalizer-construction, and transcoder-conformance rules
- **Access:** Coordinator and Investigator receive header + index. Only the Coordinator receives and runs ACH_Eval. The Archivist receives neither the frame nor ACH_Eval.

---

# PHASE II — Coordinator-Led Corpus Interrogation

### 10. Initialize and assign ownership

- One Coordinator, one Investigator, one Archivist, one empty question database, the private quest state required by the frozen header, and one query-response record for each completed round.
- The Coordinator holds ACH_Eval, the operational record, and stopping authority. The Investigator owns question writing, submission, and exact capture. Neither reads primary-source bodies during discovery.
- The corpus is inside the Archivist's domain. Both Coordinator and Investigator receive the index and header; only the Coordinator receives ACH_Eval.
- A Chrome browser extension or a similar interface carries each Investigator query to the Archivist and returns the response.
- Mr. Fusion is not part of this phase and receives no role after the quest begins.
- **Separation comes from the data path. Not a rule either side could ignore.**

### 11. Pick Next Query

- The Investigator follows the frozen Discovery Quest Header to select and write the next question for the Archivist. The header—not a second generic module—defines how the hypotheses, ranked index, prior responses, private quest state, decisive tests, source coverage, novelty, and stopping conditions affect that choice.
- Preserve the header version used for every issued question so the selection procedure remains auditable and can change between runs without silently changing the question database's meaning.
- **Until a superior method of asking good questions of data is developed, the questions produced by this quest are the questions the later witness-compression stage reuses.**
- Do not add a second question-value formula outside the header. A header may contain explicit calculations or state rules when its human author has chosen and defined them.

### 12. Lint + Ask

- Strip: hypothesis labels, ranks, jargon, goals.
- Translate into corpus's own terms — authors, mechanisms, populations, statutes.
- **Every Investigator question must specify between one and three corpus sources.**
  - Two specified sources is optimal for an ordinary question
  - One source is optimal when clarification is needed
  - Three sources is permitted but is not the preferred default
- Confirm that every specified source exists, then submit the question to the Archivist. Named sources are starting anchors; other useful corpus sources may also be cited.
- Before submission, create the `QID` and save the exact specified-source list and frozen header version in the query-response record.
- Keep internal hypothesis labels, private state, ranks, and ACH_Eval records out of the Archivist message.

### 13. Integrate

- Preserve the exact query and exact response in the query-response record and add the issued question and its unique `QID` to the question database.
- Apply the frozen header's response-reading, private-state update, retry, coverage, novelty, and stopping instructions. These instructions may be project-specific and must not be silently replaced by a generic state mechanism.
- Keep: novelty, contradiction, qualification, attribution upgrades, independent corroboration.
- Suppress redundant wording. Never suppress independent support.
- **Orientation here is provisional and non-dispositive** until validation. Quest gives orientation, not verdict.

### 14. Stop or Continue

- Mode: `FINITE_ENUMERATED_POOL` · `OPEN_WORLD_SATURATION` · `HYBRID`.
- The Coordinator runs ACH_Eval at each checkpoint. Its cumulative fragment carries the evidence record, gaps, conflicts, corrections, and the current allocation forward, and is the privileged input to the next checkpoint. Allocations are provisional judgments, not calibrated probabilities or source validation, and the fragment does not replace downstream FRDs, blind validation, witnesses, or crux identification.
- The Investigator receives acquisition priorities from the Coordinator, never the allocation vector. Feedback identifies substantial and trivial novelty; consequential findings are retained even when allocations do not change.
- Apply the frozen header's stopping rule: unchanged allocations for configured consecutive checkpoints on every enabled axis, plus required decisive and adverse tests. Reopen a settled axis if later evidence moves it.
- **Exhausting the database ≠ exhausting the literature.**
- No recall percentage without a real sampling design.

### 15. Late Sources

- Add to same database. Update manifest + index. Impact assessment under the frozen header's state and continuation rules.
- **Rerun affected work if the source changes:** hypotheses, prior query choices, earlier interpretations, dictionary senses, dependencies.
- No second database. A corpus beyond the deployed service's capacity is a configuration limit, not a licence to split the run.

---

# PHASE III — Build and Verify FRDs

### 16. Compile Candidate FRDs

- **Process one question-answer file at a time.** Harvest all possible FRDs from that file before moving to the next question-answer file.
- A question-answer file may produce several FRDs, including multiple claims from one source. Each FRD states one claim anchored to one cited source.
- Never combine raw material from different question-answer files into one FRD.
- Within the active question-answer file, map the answer's distinct propositions to the cited source passages and split compound claims when necessary.
- **Every FRD records exactly one `QID`:** the question whose query-response round supplied the raw material used to create that FRD.
- Several FRDs may share one `QID`; no FRD may carry two producing question IDs.
- Record source act + name the actor.
- **Required, not optional:** adverse findings, nulls, gaps, conditions, numbers, limitations.

### 17. Harvest Accounting + Lineage

- Sources appearing in answers vs. sources producing FRDs → find under-harvested.
- Group FRDs sharing a dataset or citation ancestor.
- Tag: `OWN_RESULT` · `DERIVED_FROM(ancestor)` · `DERIVATIVE_UNKNOWN`.
- Show raw counts beside lineage-adjusted. Neither measures authority.

### 18. Validation Packets

- One candidate FRD + only the source file it names.
- No hypotheses, header, ranks, downstream use.
- Query-response lineage metadata may travel with the FRD without disclosing the hypotheses. The validator need not receive the question text in order to preserve its identifiers.
- Any context already exposed to the outcome is retired from validation duty.

**18.1. Deploy the validation kit after FRD creation**

After completing FRD creation and the harvest review, the creating LLM announces: **"FRDs are complete. Ready to deploy the validation kit to a new folder."** The human analyst chooses the destination: **"OK, deploy to this folder: [destination]."** Deploy after that instruction; an already supplied destination and deployment authorization are sufficient.

The kit contains the candidate FRDs with their original IDs and Parent QID/reference metadata, the ethos, self-contained blind-validation instructions, a location for validation output, and an empty primary-source folder. Use a simple `primary sources` folder by default and make its location explicit in the deployed instructions. Preserve ordinary labels and filenames. A candidate collection may remain in one file; each validation still checks one FRD against only its named source.

Exclude the discovery header, ranked index, hypotheses, scores, quest state, original query-response text, research conversations, stop reports, and witness/crux conclusions. Those remain in the analyst's project archive. QID references are preserved as metadata and need not resolve inside the kit. Include a general pipeline document only if its deployed copy is specific to validation and does not direct the verifier to discovery material. Preserve any existing work at the destination.

After creating the kit and its source folder, the deploying LLM says: **"Deployed to [absolute destination]. Please put all primary sources into [absolute source-folder path], preserving their filenames, then start validation in a fresh context in [absolute destination]."** State that the kit is awaiting sources; do not describe source availability as checked before the files arrive. If the analyst already supplied the sources, report that they are present instead of asking for another copy. A source library may contain the full primary corpus, but the validator opens only the source named by the current FRD and any corresponding original needed to resolve a conversion issue.

Once sources are supplied, the fresh validator follows the kit's instructions and reports any missing named sources while continuing available checks. A context already exposed to the quest's hypotheses or outcomes may prepare the kit but may not perform blind validation.

### 19. Blind Validation

- Check structure, source act, attribution, every clause — against the source.
- Record enough source text to verify the call.
- Repair locator or claim before discarding. Failures stay in the audit trail.
- Distinguish jointly sufficient `{A+B}` from independent alternatives `{C}` / `{D}`.

**19.1. Query-lineage carry-through**

- A validated or repaired FRD preserves its one `QID` and the query-response metadata inherited from its candidate FRD.
- A split creates child FRDs that retain the parent's same `QID`.
- Metadata preservation must not reveal the specific hypotheses to the blind validator.

**19.2. Source-assignment audit**

- Separate "this source supports the claim" from "this is the best source to cite."
- Leaves the blind verdict alone. May emit only: `BETTER_SOURCE_AVAILABLE` · `REDUNDANT_WITH` · nothing.
- Conflict inside one source = `INTRA_SOURCE_TENSION`. Nonblocking. Not disagreement between authorities.
- Findings update lineage.

---

# PHASE IV — Language Framework and Witnesses

### 20. Artifact Registry

- Immutable IDs, hashes, dependency links for everything after the FRDs.
- Purpose: a change regenerates exactly what it should.
- Link run → `QID` → response → candidate FRD → validated or repaired FRD → question-application record → witness → transcoded witness → deletion-minimal hypothesis coverage set → exclusion or crux result.
- Each run creates its own question records, FRDs, validated FRDs, and witnesses. Records from different runs are not merged into one identity.
- Also records which external disclosure describes which version.

**20.1. Reproducibility records**

- Per model step and human decision: provider · model version · endpoint · timestamp · full prompts + hashes · settings · seed · tools · every attempt and retry · raw and parsed output.
- Plus: **the exact output released + the predeclared rule that selected it.**
- Unavailable platform data marked unavailable.
- Competing valid outputs preserved as disagreement.

### 21. Vocabulary Harvest

- Build the custom dictionary from validated FRDs.
- Freeze and identify the exact validated/repaired FRD content fields used for the harvest and the versioned reference English corpus used for comparison. Count only the source-grounded FRD claim text; exclude metadata, IDs, citations, filenames, prompts, validation commentary, and attached source blocks.
- Use one identified tokenizer and base-form procedure consistently for the vocabulary harvest. Record its name, version, settings, and manual corrections. Distinguish its token denominator from the whitespace word count used for witness ceilings; do not report the two counts as interchangeable.
- Count nouns, verbs, adjectives, and adverbs by base word form. Exclude ordinary function words such as articles and conjunctions unless the corpus uses one as a quoted or technical term. Preserve every original occurrence and spelling.
- Where comparable counts are available, calculate `FRD rate = occurrences / counted FRD tokens`, `English rate = occurrences / counted reference-corpus tokens`, and `relative frequency = FRD rate / English rate`. State the counting unit and whether the comparison uses base-form counts or only estimates for the base form's spelling. Do not describe an approximate spelling-frequency comparison as an exact base-form frequency measurement.
- If an actual reference count is zero and its denominator is known, use one occurrence over that denominator and flag the adjustment. If only a frequency estimate is available, identify its provider/version and limitations; a returned zero does not justify inventing a reference-corpus size. Leave an unavailable ratio unestimated rather than fabricating precision.
- Provisional working default: send a candidate occurring in at least three distinct validated-FRD sentences to contextual review. Retain the ordinary-English frequency comparison as a diagnostic or prioritization aid, not a required `relative frequency > 1` exclusion gate. The Pump.fun pilot found little filtering at that cutoff; it did not establish an optimal threshold or a universal corpus-size boundary. Missing reference-frequency data need not stop contextual review.
- Frequency creates candidates; it never decides meaning. A candidate becomes a dictionary entry only after the contextual-sense procedure in Module 21.1 succeeds.
- Do not set a target dictionary size. Publish every entry that passes the selection, sense, and example requirements; do not add weak entries to reach a quota or discard valid entries to remain under one.
- Record the total candidates reviewed, entries approved, provisional senses withheld, and reasons for rejection.

**21.1. Dictionary entries**

- Collect every occurrence of the candidate word with its validated-FRD sentence and enough adjacent text to understand the use.
- Compare every pair of occurrences. Use the following review scale:
  - `4 SAME`
  - `3 SAME WITH MINOR CONTEXTUAL VARIATION`
  - `2 RELATED BUT DISTINCT`
  - `1 DIFFERENT`
  - `0 CANNOT DECIDE`
- Use two independent review passes that cannot see one another's output before submitting. Either pass may be performed by a model or a human under the same frozen instructions. Preserve both ratings and their rationales. A disagreement that would change a sense boundary goes to human review; it is not resolved by averaging.
- Identify boundary-moving disagreements from the complete pair ratings, not only pairs a grouping algorithm happened to visit. A short review summary may point to those ratings. Preserve unresolved groups while continuing work on unrelated agreed groups.
- **Place occurrences in one sense group only when every pair inside the proposed group is rated `3` or `4` after review.** A `2`, `1`, or unresolved `0` prevents automatic grouping. This conservative rule prevents a chain of merely similar uses from silently becoming one meaning.
- An order-dependent grouping procedure proposes a partition; it does not prove that this partition is uniquely determined. Report pair-rating agreement separately from agreement on the resulting groups. Neither is independent proof that the selected senses are correct.
- **Create one entry per approved sense group.** Write it as `WORD (modifier)`, with a modifier of no more than five words that distinguishes this sense without deciding a dispute the sources leave unresolved.
- Select one canonical label and definition for each approved group; preserve competing proposals as review material. Harmless wording differences may be settled by choosing a faithful plain-language label without repeating the sense review. A difference that changes the definition or membership remains a substantive disagreement. Label-string agreement and sense-group agreement are different measurements.
- Each entry records: immutable entry ID · base word form · exact `WORD (modifier)` · plain-language definition · source or passage scope · every occurrence ID · three example sentences · allowed scoped aliases · related but separate entries · reviewer decisions · version and status.
- **Every published entry must have at least three distinct source-sentence examples** from its own sense group. Count sentence identities, not occurrences: three uses of a word in one sentence supply one example. Select three distinct sentences, preferring three different FRDs when available. Store each raw sentence verbatim and a display copy that marks the linked occurrence as `WORD (modifier)` without rebinding other same-spelling occurrences automatically.
- A plausible sense with fewer than three examples is marked `PROVISIONAL — INSUFFICIENT EXAMPLES` and is not used as an active custom-dictionary entry. Its occurrences remain preserved for a later version.
- An `ACTIVE` flag in an experimental output does not replace these checks. Before applying a dictionary, confirm that the selected wording, supported sentence examples, scope, and unresolved decisions are actually present; repair selection/export mistakes from the retained occurrences rather than rerunning all reviews.
- **The number of contextual variants is therefore the number of reviewed sense groups that satisfy the three-example rule**, not a number chosen in advance.

### 22. Canonicalizer

- Build the canonicalizer from the frozen custom dictionary and grammatical examples found in the validated FRDs. Its output is one controlled grammar profile for the run.
- The canonicalizer creates a shared house style so witnesses and hypotheses read as if the same careful technical writer expressed them. It standardizes wording and structure without imitating an individual author and without changing meaning.
- First list the grammatical shapes needed to preserve the corpus's protected properties: attribution · actor and action · affirmation and denial · uncertainty and necessity · conditions · alternatives · identity and role · time · quantity · scope · reference.
- Group grammatical constructions that express the same relationship with the same protected properties. A construction may join the same group only after a reviewer finds it meaning-preserving in both directions.
- **Select the preferred construction for each group by this order:**
  1. Preserve every protected property
  2. Make the actor, source, and referent explicit
  3. Make negation, conditions, and modifier scope unambiguous
  4. Use the fewest clauses and words that preserve meaning
  5. Use frequency in validated-FRD examples only as the final tie-break
- **The controlled grammar profile normally prefers:**
  - Explicit nouns instead of ambiguous pronouns
  - Explicit source attribution
  - Active voice when the actor is known
  - Preserved passive voice when the actor is unknown
  - One main claim per sentence when splitting does not change scope
  - `If [condition], then [result]` for conditions
  - Explicit repetition when ellipsis would create ambiguity
  - Visible alternatives rather than silently choosing one
- **Never normalize away** a difference in attribution, polarity, modality, condition, identity, role, temporal or quantitative scope, or unresolved alternatives.
- For every custom term, record its approved canonical entry and any scoped aliases, including reviewed inflected forms where needed. Preserve the input's number, tense, and quantifiers: never add "each" or convert a generic plural into a singular solely to accommodate a dictionary citation form. Similar spelling or a shared base word never licenses substitution between different contextual senses.
- Freeze the dictionary, controlled grammar profile, test examples, and reviewer decisions together. A change creates a new version and triggers retranscoding of affected artifacts.
- The canonicalizer is the rule set and language map used to build the transcoder; it is not itself the encoded output. Reserve parentheses for `WORD (modifier)` labels; use square brackets for other parentheticals.

**Working implementation:** The reusable `canonicalizer.json` is `ach-ce-v0.1.3`, with 14 rules and 12 protected properties. The Run 4 profile (`results/run4-aguilar/canonicalizer.json`) adapts it to the new qualified records; the Run 4 dictionary (`results/run4-aguilar/dictionary.json`) preserves disputed senses as provisional. See the implementation supplement for the deliberately narrowed, question-selected claim-nucleus harvest and measured limits. These are pilot language tools, not a universal language-equivalence method.

**22.1. Canonicalizer conformance tests**

- Test every preferred construction with meaning-preserving examples and with near-miss examples involving actor reversal, negation, uncertainty, conditions, and ambiguous modifier attachment.
- A preferred construction passes only when the canonical form preserves the intended meaning and refuses the near-miss meaning.
- When the profile cannot express a protected distinction safely, return `REQUIRES_REVIEW` or preserve an `APPROVED_EXCEPTION`; never force the text into the nearest available pattern.
- Preserve test inputs, expected results, actual results, and the profile version.

**22.2. Reuse across runs**

- A new run may reuse a prior custom dictionary, canonicalizer, and transcoder when doing so saves time.
- Reuse is most appropriate when all hypotheses remain unchanged, because these language artifacts are then unlikely to require major changes.
- Reuse still requires a comparison against the new run's validated-FRD vocabulary and grammatical shapes. New or changed senses create a new dictionary and language-tool version rather than silently changing the reused artifacts.

### 23. Transcoder

- The transcoder is the executable English-to-English process compiled from one frozen custom dictionary and one frozen controlled grammar profile.
- Apply the same transcoder version separately to every witness and every human-written hypothesis statement before semantic matching.
- **For each input, perform these steps in order:**
  1. Preserve the exact original text and assign an input ID
  2. Locate candidate custom terms and create a dictionary binding for each occurrence
  3. Leave an occurrence unresolved when its context does not safely select one contextual sense
  4. Replace approved bindings with their exact `WORD (modifier)` forms or permitted scoped aliases
  5. Rewrite the sentence using the preferred controlled-grammar construction
  6. Produce a normalization preview identifying every term substitution, referent clarification, sentence split, reorder, and grammatical rewrite
  7. Compare original and transcoded text for every protected property
  8. Release the transcoded text only after the conformance result is `PASS` or a human approves a recorded exception
- **The transcoder may clarify a uniquely supported referent, but it may not:**
  - Invent context
  - Choose among unresolved meanings
  - Strengthen or weaken uncertainty
  - Reverse an actor and object
  - Turn a report into an assertion
  - Add a causal link
  - Resolve a source dispute
- A `REQUIRES_REVIEW` or `ABSTAIN` result does not enter semantic matching until resolved. The raw witness or hypothesis remains preserved and unchanged.
- Every transcoded artifact records: input ID and raw text · output ID and controlled-English text · dictionary and grammar versions · binding decisions · rewrite trace · protected-property comparison · reviewer · conformance status.
- The transcoder's purpose is representational consistency, not truth determination. Coverage is still computed from the approved transcoded text, and metadata never supplies coverage.
- **Owner clarification, September 6:**
  - Raw witnesses have a hard maximum of **60 words**
  - Transcoded witnesses may use **80 words**, uniformly
  - Count all whitespace-separated prose tokens, including parenthetical sense labels
  - Extra space accommodates dictionary expansion and faithful restructuring, not new claims
  - Hypothesis statements remain uncapped
  - Check each representation against its own ceiling and flag a failure rather than dropping material meaning

**Working implementation:** `transcoder.py` runs contextual binding, controlled-English rewriting, mechanical checks, and a separate semantic review. The pilot usage record (`ACH-language-tools/README.md`) distinguish successful transformations, unresolved meanings, and failed requests. A recorded prior defect can guide a targeted repair; its rationale does not supply the independent review's verdict. The implementation standardizes representation, not source truth or hypothesis scores; coverage and crux methods remain separate downstream work.

### 24. Witness Construction

- An LLM uses a question from the run's question database to query one validated FRD and determine how the limited text in that FRD can answer the question.
- Treat the LLM's compressed answer as the witness produced by that question–validated-FRD pair.
- The producing question supplies the first compression lens, not a guarantee that every validated FRD can yield a faithful, useful answer within the ceiling. Record a specific compression failure when it cannot; do not invent an answer or silently change its producing QID.
- **Required origin reuse:** use the question identified by the FRD's one producing `QID` to query that validated FRD for the purpose of producing a witness.
- One approved question paired with one validated FRD produces exactly one witness.
- One question may produce multiple distinct witnesses by being paired with multiple validated FRDs. One validated FRD may produce multiple distinct witnesses by being paired with multiple questions.
- Two questions do not produce the same witness, and two validated FRDs do not produce the same witness.
- Record every unique question–validated-FRD pairing and its one resulting witness in a question-application record. Applying another question does not add another producing `QID` to the FRD.
- Do not pair every question in the database with every validated FRD. Only a small number of questions selected by the authorized origin, cluster-best, and optional nearest-neighbor procedures may be applied to an FRD.
- A validated FRD produces one witness for each approved question actually paired with it, subject to a small per-FRD maximum. The exact maximum remains to be set.
- Preserve every extracted witness and its lineage; release to matching still depends on conformance.
- **Use 60 words as the hard maximum for untranscoded witnesses, and 80 words as the maximum after transcoding**, as clarified by the owner on September 6. Count whitespace-separated tokens of witness prose; metadata is excluded, while attribution, qualifications, and parenthetical sense labels in the prose count. A numeral or hyphenated compound without spaces counts as one token. Neither maximum is a target to pad toward.
- Apply each representation's maximum uniformly; no per-FRD larger allowance. A different pair of limits requires the analyst's decision. Neither limit is a demonstrated optimum or a losslessness guarantee: the original Pump.fun W60 arm had 56/64 audit passes and eight witnesses requiring revision.
- First try to repair a failed witness within the common ceiling. If material meaning cannot be preserved, retain the failure and its parent record while continuing other work; consider a different common ceiling rather than silently dropping the qualification. A self-declared success or compliant word count does not establish fidelity.
- Each witness carries only its parent QID and FRD ID. Earlier forms remain in the linked registry; dictionary bindings appear as visible `WORD (modifier)` labels.
- FRDs never rewritten.

**24.1. Dictionary and language-tool application**

- Apply the custom dictionary and canonicalizer when preparing witness text for the transcoder.
- Preserve the connection from every encoded custom term to its dictionary entry.
- For each candidate custom-term occurrence, two independent binding passes compare its local context with the definitions and three examples of every entry sharing that base word form.
- Automatically approve a binding only when both passes select the same entry and neither identifies a protected-property conflict. Preserve both choices and rationales.
- A disagreement, multiple plausible entries, or insufficient context returns `REQUIRES_REVIEW`. If human review cannot select one safely, leave the occurrence unresolved and withhold the artifact from matching; never choose the most frequent sense merely to continue.
- A term absent from the custom dictionary remains ordinary English. Absence never authorizes the transcoder to invent a new active entry during witness or hypothesis processing.

**24.2. No-dictionary-term FRDs**

- A validated FRD does not need to contain a custom-dictionary term in order to produce a witness.
- Ordinary English remains available when no run-specific dictionary entry is needed.

**24.3. Question-guided compression**

- The LLM uses the question to decide which validated FRD content is relevant to the witness and how that content can answer the question. The question does not act on the FRD by itself.
- Use the validated Claim as corrected or qualified by its Verdict, checked against the FRD's attached source text. A candidate wording rejected during validation must not re-enter through compression. If those fields remain materially inconsistent, identify the FRD repair needed rather than silently choosing a convenient reading. Dictionary harvesting still uses the corrected Claim field, not verdict commentary as vocabulary evidence.
- Preserve qualifications needed to make each retained assertion faithful, including countervailing findings and exceptions. Omitting irrelevant detail may be legitimate; losing something that changes the answer to the producing question is a material omission, even if the remaining assertions are individually supported.
- Reusing quest questions is the current technique because those questions were originally selected to distill primary-source material in relation to the hypotheses.
- Earlier blind FRD validation does not guarantee hypothesis-neutral witness selection. Describe actual hypothesis exposure when evaluating compression; these pilot comparisons do not establish that exposure has no effect or authorize changing the existing blind-retrieval/FRD-validation boundaries.
- If one FRD produces several witnesses, keep their shared FRD origin visible.

**24.4. Cluster and neighbor question settings**

- Cluster-best experiment: identify the question within an FRD cluster that, as asked, is most directly related to answering at least one hypothesis, and apply that question to every validated FRD in the cluster.
- If the cluster-best question differs from an FRD's producing question, record it as an additional question application rather than a second producing `QID` on the FRD.
- Nearest-neighbor experiment: optionally identify the neighboring cluster with the largest number of sources in common, select its most relevant question, and apply that question as an additional lens.
- The nearest-neighbor experiment is an ACH 2.0 variant setting, not a required step.
- Preserve whether each witness came from required origin reuse, the cluster-best experiment, or the optional nearest-neighbor experiment.

### 25. Fidelity Audit

- Give the auditor the exact producing question, the parent FRD's Citation, Claim, Source text and Verdict, and the witness prose. A QID alone cannot substitute for the question. Preserve their identifiers so any finding can be traced.
- Check both directions separately:
  - **Unsupported assertion** — what does the witness assert more strongly, more broadly, or differently than the validated FRD permits?
  - **Material omission** — what meaning needed to answer the producing question can a reader no longer recover from the witness?
- For each problem, identify the actual words or missing meaning and explain the consequence. Name the affected protected property when useful: attribution, polarity, modality, conditions, alternatives, identity/role, time, quantity, scope, or fabrication.
- Ask what strongest reading the witness permits that the FRD forbids, and whether the reader recovers the same source position, a weaker position, or a wrong position. Explain any tension between these answers and the verdict; a credible forbidden reading must not disappear merely because the separate unsupported-assertion list is empty.
- Return `PASS`, `REVISE_WITNESS`, `REPAIR_FRD`, or `HUMAN_REVIEW`, with a short reason. Use `PASS` when no material fidelity defect is identified. Unsupported assertions or material omissions call for repair or an explicit unresolved result, not a generous pass. A merely weaker answer is not automatically wrong, but a materially weaker answer is not an equivalent one.
- A long or unbounded "no-loss" reconstruction is another generated witness to audit against the parent FRD, not the truth baseline for judging shorter witnesses. Report unsupported assertions and missing material meanings separately; neither length nor one favorable error count determines overall fidelity.
- This is the working two-direction audit procedure tested in the Pump.fun pilot, not a proof of accuracy. Its construction (`ACH-2.0-playground-results/witnesses/FROZEN_WITNESS_INSTRUCTION.md`) and audit (`ACH-2.0-playground-results/audit/FROZEN_FIDELITY_AUDIT_INSTRUCTION.md`) prompts are worked references; their file-writing and scratch-directory instructions are not required infrastructure.

**25.1. Independent approximation check**

- Validator separate from constructor.
- Supply the evidence packet described in Module 25, without hypotheses, scores, preferred outcomes, or the constructor's self-evaluation. This witness-to-FRD check is different from blind primary-source FRD validation; it does not replace the earlier source check.
- Asks: does a competent reader recover the same source position? · what's the strongest reading the witness permits but the FRD forbids? · delete each sentence, what's lost?
- Returns: pass · revise the witness · repair the FRD · send for human review.
- Different model or fresh isolated context. Never one contaminated by construction.
- A pass is a best-effort judgment, not proof.
- When comparing compression methods, mix the audit items and conceal method labels if claiming method-blind evaluation. An ID such as `W60:FRD-...` reveals the arm even if a separate arm-key file is withheld. Describe actual isolation and information access, not just intended blindness.

### 26. Encode

- Transcode witnesses and hypotheses through the same custom dictionary, canonicalizer, and transcoder.
- Keep raw and encoded paired.
- Unresolved expressions stay unresolved. No guessing.
- Telemetry sufficient to spot systematic transformation failures.

### 27. Conformance Gate

- Audit: compression fidelity · dictionary bindings · scoped aliases · protected properties · controlled-grammar compliance · lengths · leakage · raw-vs-transcoded correspondence.
- Reject an artifact from matching when it contains an unresolved binding, an unapproved grammar exception, an unexplained protected-property change, or a missing transformation trace.
- Route each defect to the responsible module. Never patch meaning during matching.
- Release or withhold individual witnesses on their actual result. A corpus-level PASS rate, zero assertions flagged in one audit category, or a constructor's claim of zero failures cannot approve a witness that still has a material defect. Keep unaffected work moving.

---

# PHASE V — Match Witnesses and Identify Crux Statements

### 28. Semantic Matching

- Use the transcoded witnesses and transcoded human-written hypothesis statements as the matching inputs.
- Coverage is determined from transcoded hypothesis text and transcoded witness text. Witness metadata, provenance, source counts, and independence do not supply coverage and do not alter a coverage relation.
- Match witnesses against the internal coverage units derived from each human-written hypothesis.
- For every witness–unit pair, two independent review passes that cannot see one another's results each assign exactly one relation: `EQUIVALENT` · `WITNESS_ENTAILS_UNIT` · `UNIT_ENTAILS_WITNESS` · `PARTIALLY_COVERS` · `CONTRADICTS` · `NO_SEMANTIC_RELATION` · `ABSTAIN`.
- Every review pass supplies a match trace naming the text and protected properties that justify its relation. A score or label without a trace is invalid.
- Automatically approve a relation only when both passes select the same relation and their traces do not conflict. Preserve disagreements. A human reviewer may approve one relation or return `ABSTAIN`; do not average relation labels.
- A witness gives complete coverage to a `REQUIRED_SUPPORT` unit only through `EQUIVALENT` or `WITNESS_ENTAILS_UNIT`.
- `UNIT_ENTAILS_WITNESS` and `PARTIALLY_COVERS` remain visible but never provide complete coverage alone.
- To approve joint sufficiency, name the exact witness group and compare its combined transcoded text with the unit. Approve the group only when the combined content entails the unit, every member supplies a material contribution, and no member alone provides complete coverage. Preserve every witness separately and record each member's contribution.
- Every `CONTEXTUAL_CONSTRAINT` must remain satisfied.
- `ADVERSE_TEST` and `CORROBORATING_EXPECTATION` results remain visible but do not become mandatory affirmative coverage.
- Preserve each match's raw and transcoded inputs, relation, traces, reviewer outputs, disagreements, prompts, model versions, and final disposition.

**28.1. Matcher qualification**

- Before a matcher version may create coverage options, test it with at least fifteen frozen adversarial fixtures written in the run's vocabulary.
- The fixture set must include at least two tests for each of these patterns: actor/object reversal · active/passive wording that preserves the actor · affirmation versus denial · possibility versus necessity · a source reporting a claim versus asserting it · a claim inside a condition versus an unconditional claim · high word overlap with changed roles or relationships.
- Include both cases that must keep the same relation and cases that must change relation. Report results separately for every pattern rather than hiding a failure inside one average score.
- Failure on a pattern prevents automatic matching for cases depending on that pattern. Those cases return `ABSTAIN` until the matcher or human review resolves them.
- Passing the fixtures qualifies the matcher only for these tested capabilities; it does not prove general language understanding.

**28.2. Witness identity and non-merger**

- Never merge witnesses, including witnesses that appear equivalent or substantially similar after transcoding.
- Each witness remains the separate child of its one approved question–validated-FRD pairing and retains its own lineage.
- Equivalent or substantially similar witnesses may contribute to different deletion-minimal coverage sets. Preserve those possible sets rather than collapsing their witnesses to reduce computation.
- Proper data hygiene takes priority over speculative savings in downstream computation. Crux-testing cost scales with witnesses × rivals rather than with the number of enumerated sets (Module 29.2), so preserving distinct sets does not multiply testing cost.

### 29. Deletion-Minimal Hypothesis Coverage Sets

- A set has complete coverage when its witnesses collectively represent every `REQUIRED_SUPPORT` unit and all `CONTEXTUAL_CONSTRAINT` units remain satisfied.
- The set must contain no approved incompatibility.
- The set is deletion-minimal when no witness can be removed without leaving a required unit uncovered or breaking a necessary dependency.
- Deletion-minimal does not mean smallest by witness count, uniquely valid, or strongest by evidentiary quality.
- For each `REQUIRED_SUPPORT` unit, list every coverage option supplied by the approved semantic-matching record. Jointly sufficient partial matches enter as one grouped option while their witnesses remain separate artifacts.
- If any required unit has no coverage option, emit `NO_COMPLETE_COVERAGE`, identify the uncovered unit, and do not manufacture or weaken a witness to continue.
- Order the required units from fewest to most available coverage options. Beginning with the least-covered unit reduces wasted search without changing which sets are valid.
- Construct candidate sets by selecting at least one coverage option for every required unit. When a selected option is a group, add every witness in that group.
- Reject a candidate immediately when it leaves a contextual constraint unsatisfied, completes an approved incompatibility, or omits a necessary dependency.
- For every surviving complete candidate, attempt to remove each witness in stable witness-ID order. Permanently remove a witness when the remaining set still gives complete coverage and remains valid. Repeat the deletion pass until no further witness can be removed.
- Record the remaining witnesses as a deletion-minimal set. For each witness, store a removal certificate identifying the exact coverage or dependency failure caused by its temporary deletion.
- Repeat the construction across every coverage-option combination. Store a set by its sorted witness IDs and do not emit the same set twice.
- Preserve every different deletion-minimal set that completely covers the same hypothesis. Do not prefer a set merely because it was found first or contains fewer witnesses.
- Declare the search `EXHAUSTIVE` only after every coverage-option combination under the frozen inputs and constraints has been checked. Otherwise declare `RESOURCE_BOUNDED`, record the stopping limit and unexplored combinations, and state that more deletion-minimal sets may exist.
- Witness or source counts do not decide whether a set has complete coverage. Coverage depends on the semantic mapping of transcoded witness text to the transcoded hypothesis representation.
- Preserve the witnesses, parent FRDs, producing `QID`s, question applications, coverage options, jointly sufficient partial matches, dependencies, constraints, removal certificates, search order, and matching record for every set.
- The procedure for approving an incompatibility remains to be specified.

**29.1. Crux identification — membership screening and portability testing**

- The required result is to identify the witnesses a rival hypothesis cannot accommodate while they help cover their home hypothesis.
- Form deletion-minimal coverage sets as completely as possible for every hypothesis before crux identification.
- **Membership screening:** a witness passes against a rival when it appears in none of that rival's formed deletion-minimal coverage sets. Absence alone is insufficient; both portability tests must also fail.
- Inputs: the approved transcoded hypotheses and witnesses, the typed semantic matches, the deletion-minimal coverage-set memberships, the necessary dependencies and approved incompatibilities, and pointers back to raw witnesses, FRDs, `QID`s, and sources.

**Frozen rival theory.** Compile each hypothesis once into a frozen rival theory `B_H`: a machine-readable statement of every condition a valid coverage set must satisfy — `REQUIRED_SUPPORT` units with their approved coverage options, `CONTEXTUAL_CONSTRAINT` units, necessary dependencies, approved incompatibilities. `B_H` implicitly contains **every** valid coverage set for that hypothesis, including sets no enumeration has reached. Freeze and version it before testing.

**Why this replaces set-by-set testing.** Testing a witness against each enumerated coverage set is both more expensive and less reliable: cost grows with the number of enumerated sets, and a witness may conflict with every displayed set while fitting a valid set the enumeration never produced. That is the false-crux error. Testing against `B_H` searches arrangements beyond the listed sets; missed semantic matches remain a source of false cruxes.

**The two tests.** For each witness `w` and each rival `r`, put `w` to the solver against `B_r` as two separate questions:

- **T1 — consistency.** Can `w` be held with the rival's asserted units and contextual constraints without contradiction? Failure means `w` contradicts something the rival must assert.
- **T2 — coverage.** Once `w` is established, can the rival achieve complete coverage using only options that do not conflict with it? Failure means `w` removes required coverage, completes an incompatibility with needed witnesses, or breaks a necessary dependency.

**Classification.** Both tests are binary, and the pair classifies the witness against that rival:

| T1 | T2 | Result |
|---|---|---|
| pass | pass | The rival accommodates it. Not a crux against this rival. |
| fail | pass | Conflict recorded. The rival can still cover without holding it. |
| pass | fail | Conflict recorded. The rival can hold it but not while covering. |
| **fail** | **fail** | **Crux candidate if membership screening passes.** The rival can neither hold the witness nor reorganize to cover without it. |

- **Home requirement.** A crux candidate must appear in at least one deletion-minimal coverage set of the hypothesis it supports. A witness no hypothesis needs is not a crux however badly a rival fails on it.
- **Certificates.** Every test returns exactly one of three outcomes, each with a machine-checkable certificate: **accommodated**, with an example arrangement; **cannot be accommodated**, with the conflicting rule bundle; **unknown due to search limit**, reported as unknown and never converted into either answer. Record the resource budget that produced an unknown.
- **Record.** For each candidate store the witness, its home hypothesis and coverage sets, every rival tested, membership-screening results, the T1/T2 results with certificates, the exact conflicting content, material uncertainty, and full lineage to FRD, `QID`, and source.

**29.2. Comparison cost**

- Let `H` be the number of frozen hypotheses and `W_h` the distinct witnesses appearing in at least one valid coverage set of hypothesis `h`. Each is tested against every rival under both tests.

```
C = 2 × Σ over each hypothesis h of:  W_h × (H − 1)
```

- Uniform witness count `W`: `C = 2 × H × W × (H − 1)`. Worked example `H = 4`, `W = 6` gives `C = 144` tests — whether a rival has one valid coverage set or one thousand.
- Cost scales with **witnesses × rivals**, not with coverage-set enumeration, because `B_H` contains every valid set at once.
- Excluded from `C`: compiling each `B_H`, a fixed cost incurred once per run and the step whose **fidelity**, not speed, is the real risk; and further analysis applied only to pairs failing both tests. Tests are counted, not timed.

### 30. Crux Candidates and Core Termination

- Identify and preserve every crux candidate, ordered by the number of rivals against which membership screening passes and both portability tests fail.
- The practical value of crux identification is to reduce a large corpus and witness registry to a small number of data needles that deserve concentrated human investigation. An analyst can try to undermine a crux witness; if it fails, the hypothesis coverage set that depends on it becomes vulnerable in the exact way recorded by its removal certificate and portability tests.
- Every candidate result must identify the witness, the hypothesis it helps cover, each rival it defeats, and the certificates showing why that rival can neither hold it nor cover without it.
- A crux result does not determine the witness's truth, cultural or sociological authority, source independence, or dispositive legal or scientific quality.
- The core protocol terminates after crux identification, with limitations and any unknown-due-to-search-limit results disclosed. When no witness qualifies against any rival, report that and deliver the coverage sets. Do not invent cruxes to terminate.

**30.1. Human-facing final report**

- Produce one initial analyst-facing report of fewer than 4,000 words. Do not make the analyst read the full witness registry in order to understand the result.
- State the crux candidates found, the rival hypothesis each one defeats, the exact conflicting language, the reason for selection, material uncertainty or disagreement, and the witness, FRD, question, and source pointers needed for audit.
- Keep the complete machine-readable registry, alternate coverage sets, ACH_Eval outputs, and validation records as linked audit artifacts rather than dumping them into the initial report.
- The report may say only **"best understood from this corpus and this run."** It must repeat that the protocol does not guarantee that every relevant item was extracted from the original corpus.

### 31. Optional Analysis After Core Termination

- Review the conflict-recorded witnesses — those failing exactly one test against a rival — when the analyst wants more than the crux candidates themselves.
- Permit the human analyst to evaluate the authority and dispositive quality of individual witnesses.
- Keep these activities separate from the core termination rule.

---

# PHASE VI — Test, Publish, and Fork

### 32. Optional Continuation

- A later continuation may add sources, resume the quest, review additional ranked candidates, or run the optional human-authority analysis.
- A continuation that changes the hypotheses may require changes to the custom dictionary, canonicalizer, and transcoder rather than reusing them unchanged.

### 33. Evaluation Harness

**Measure:**
- question-database completeness
- question-record non-merger
- one-QID-per-FRD conformance
- one-file-at-a-time FRD harvesting
- query-response-to-FRD lineage accuracy
- FRD validation fidelity
- approved-application cap conformance
- one-witness-per-question–FRD-pair conformance
- question-application-to-witness lineage
- witness non-merger
- witness compression fidelity
- dictionary-selection reproducibility
- contextual-sense stability
- binding accuracy
- controlled-grammar conformance
- protected-property preservation
- transcoding fidelity
- text-only unit-match accuracy
- deletion-minimal-set validity, deduplication, and enumeration status
- assessment and crux-result reproducibility
- exclusion accuracy
- agreement between the process's strongest crux candidates and expert review

**Standards:**

- Do not claim validated allocation accuracy from a crux result, or the reverse. ACH_Eval and crux identification answer different questions.
- The desired validation compares the process's result with conclusions reached by human experts who can read all of the quest questions and answers. The exact expert-review procedure, success measure, number of tests, and confidence calculation remain **TODO** items.
- Crux identification returns a determinate result per witness–rival pair with a checkable certificate, or an explicit unknown. **Report unknown-due-to-search-limit results as unknown**; never convert them into either answer, and never present a certificate-free result as a crux.
- Localize every failure to a named module.
- Separate measured counts from model-judged labels and conclusions inferred from them. State which items were audited, by whom when known, what the reviewers could see, and what was not tested. Recomputable arithmetic does not independently validate the underlying judgments.
- A single hypothesis-exposed witness compared with a single unexposed witness cannot separate exposure effects from ordinary generation variation. For a stronger leakage claim, add repeated same-condition comparisons and supply the exact question to the judges. A small or balanced set of flagged differences is not proof of no leakage; do not require a new large experiment merely to use qualified pilot results.
- **Claims boundary to state:** until human-alone, model-alone, and combined use are tested on the same task and corpus — claims limited to **capability, traceability, compression, auditability. Not improved judgment or accuracy.**

### 34. Publication

**Release:**
- The human-facing report under 4,000 words
- Shareable corpus
- Manifest
- Rebuild instructions
- Index
- Header
- Human-written hypotheses
- Internal coverage representation
- Run-specific question database
- Query-response records and specified-source lists
- FRDs and their one producing `QID`
- Validation records
- Question-application records
- Custom dictionary
- Canonicalizer
- Transcoder
- Separate, unmerged witnesses
- Raw and transcoded forms
- Semantic matching
- Deletion-minimal hypothesis coverage sets
- ACH_Eval checkpoint outputs
- Exclusions
- Strongest crux candidates
- Links to relevant implementation companions

**Note:** Unavailable sources and settings marked unavailable, not silently omitted.

### 34.1. Forking

- Clone parent run. Declare source additions, hypothesis revisions, prompt changes.
- Rerun only what those affect. Rest by reference.
- Publish the diff + whether the conclusion moved.
- **Disagreement is demonstrated by re-running, not by appending criticism.**

---

## Optional Routes

**A — Per-publication Q&A.** One publication → Q&A harvest → FRDs. Seeds the quest, cuts cost. Subordinate to adaptive selection. Never a checklist.

**B — Extended crux review.** After the crux report, permit review of conflict-recorded witnesses and additional ranked candidates without changing the initial report's word limit.

**C — Human authority and dispositive review.** A human may separately evaluate the authority and dispositive quality of each witness; ACH itself remains blind to authority.

**D — Future retrieval.** Any NotebookLM replacement must demonstrate: private-frame isolation · source attribution · auditability · same ordered artifacts. One-database interface only.

**E — Nearest-neighbor question lens.** Enable the optional cluster-neighbor question application and compare its witness yield with the required origin reuse and cluster-best experiment.

---

## Still Open

1. The current ACH_Eval embodiment supports one or two axes, each with two substantive hypotheses and an unresolved option. Broader approved frames require a compatible configured assessment method rather than silent hypothesis rewriting.
2. What small maximum number of approved questions may be paired with one validated FRD?
3. **Owner-set limits in Module 24:** 60 words before transcoding; 80 afterward, uniformly. Still open: fidelity across other corpora and downstream coverage matching; these limits do not establish losslessness.
4. How is the cluster-best question selected when several questions are equally relevant?
5. How are ties in nearest-neighbor shared-source count resolved when the optional variant is enabled?
6. **(29)** What process approves an incompatibility or identifies a necessary dependency?
7. **(29.1)** How faithfully does compilation of a frozen rival theory `B_H` preserve the approved hypothesis requirements? This is the fidelity risk in crux identification — a compilation question, not a search question.
8. **(29.2)** What resource budget should a portability test receive before returning unknown, and how often does that limit bind on larger corpora?
9. How does crux yield behave across other corpora and frames? The method is implemented and has been run end to end; behavior outside the runs performed to date is not yet measured.

**Not open:** Single vs. multiple databases. **Decided. Multi-database operation, partition policy, sharding, routing — excluded future scope.**
