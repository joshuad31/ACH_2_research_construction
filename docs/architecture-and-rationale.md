# Claim Registry ACH 2.0

*Architecture and Rationale: Question-Mediated Distillation of a Source Corpus into Crux Candidates*

**Contents**

1. Overview
2. Recipe 1: the partitioned, Coordinator-guided quest
3. Bridge: FRD creation and validation
4. Recipe 2: from validated FRDs to crux candidates
5. The distillation cascade
6. Foundations and limits
7. Glossary

## 1. Overview

### 1.1 Purpose

Claim Registry ACH 2.0 is an architecture that uses language models to evaluate competing hypotheses about a hard question against a large corpus of source documents. ACH stands for Analysis of Competing Hypotheses. The architecture takes a corpus that no single reader or model can hold in view and distills it into a small set of crux candidates: short, source-traceable statements that distinguish the competing hypotheses and deserve concentrated human attention. Every crux candidate can be followed back through its parent records to the passage in the source that supports it.

The architecture is a process for distillation, comparison, and audit. It is not a truth machine. Its conclusions are the best understanding available from a particular corpus and a particular run.

### 1.2 Two core recipes and a bridge

The architecture is organized around two core recipes joined by a bridge.

**Recipe 1: the quest.** An Investigator that cannot read the corpus directly asks an Archivist that holds the corpus a series of source-grounded questions. The Archivist answers from the source material without receiving the investigation's hypotheses. At intervals, a Coordinator assesses the accumulated answers against the hypotheses using an assessment prompt referred to as ACH_Eval, and feeds the results back to the Investigator, which uses them to ask questions more likely to change the assessment. The quest ends when further questions stop changing the assessment. Its principal byproduct is a question database: every question actually issued, each with a unique question identifier (QID), preserved together with its answer.

**Bridge: facts and validation.** The Archivist's answers are converted into entries in a Facts and References Database (FRD). Each FRD entry states one claim anchored to one source and records the one question whose answer produced it. Each entry is then validated against the source it names.

**Recipe 2: distillation to cruxes.** The question database is used a second time. Each validated FRD is compressed into one or more short witnesses by applying a question to it. A custom dictionary, a canonicalizer, and a transcoder rewrite the witnesses and the full hypothesis statements into one consistent controlled English. Semantic matching then assembles the witnesses into deletion-minimal coverage sets for each hypothesis, and crux identification selects the witnesses that help cover one hypothesis but that a rival hypothesis cannot accommodate.

> See diagram depicting the complete compilation chain as a vertical sequence of fourteen steps: (1) conversion of a large corpus to Markdown; (2) creation of a corpus index; (3) identification of hypotheses and creation of a header containing the ACH frame and quest instructions; (4) quest rounds in which queries are sent to the Archivist and responses are returned for analysis; (5) Bayesian updating that uses the ACH frame and prior context to elicit maximally novel responses, with a return path from step 5 to step 4 indicating repeated quest rounds; (6) termination of the quest once the expected marginal value of further novelty approaches zero; (7) transformation of query responses into FRD entries; (8) validation of FRD entries against the sources they name; (9) question-guided witness creation; (10) creation of a custom dictionary from validated FRD entries; (11) creation of a canonicalizer and a transcoder; (12) transcoding of witnesses and full hypothesis statements; (13) formation of deletion-minimal hypothesis coverage sets of witnesses; and (14) crux identification. Steps 1 through 6 form Recipe 1 and its preparation, steps 7 and 8 form the bridge, and steps 9 through 14 form Recipe 2. An annotation states that the producing question and its QID are retained through witness creation.

### 1.3 The idea that connects the recipes

A question selected because its answer could change the assessment of competing hypotheses carries a record of why particular information was worth obtaining. The architecture uses that record twice.

In the first pass, the question directs extraction from the corpus. Of everything the corpus contains, the Archivist's answer selects the material relevant to the question, and that material becomes validated FRDs. In the second pass, the same question is applied to a validated FRD to decide which of its content belongs in a witness. The question supplies the relevance criterion, and the validated FRD supplies the evidential limit. Sources constrain FRDs, and validated FRDs constrain witnesses.

When the Coordinator gives the Investigator consistently good feedback during the quest, the resulting questions are the ones with the greatest potential to distill the corpus effectively, in both passes.

> See diagram depicting one approved question, identified by its QID, used in two passes. In the first pass, the question selects material from a stack of source documents, producing a cited response that becomes a source-grounded FRD, which is then validated against its named source. In the second pass, the same question is applied to the validated FRD to produce a witness. Captions state that the question selects relevance twice, that sources constrain FRDs, and that validated FRDs constrain witnesses.

### 1.4 Roles at a glance

| Role | Holds or receives | Performs | Does not receive or perform |
|---|---|---|---|
| Investigator | The header with its ACH frame; the ranked index; saved answers; qualitative feedback from the Coordinator | Writes and submits source-grounded questions; captures each exchange exactly | Direct access to the corpus. In certain embodiments, ACH_Eval and its allocations |
| Archivist | The corpus; fixed citation and formatting instructions; one question at a time | Answers each question from the source material, with attribution | The header or the hypotheses. In certain embodiments, also the index, source ranks, allocations, or the research state |
| Coordinator | The header; the index; source manifest metadata; saved answers; ACH_Eval | Runs checkpoint assessments; directs the Investigator; decides when the quest stops | In certain embodiments, source bodies during the quest, and blind validation in its hypothesis-exposed context |
| Validator | One candidate FRD and the source file it names | Checks the FRD against the source; confirms, repairs, or rejects it | In certain embodiments, the hypotheses, the header, assessments, or the intended use of the FRD |

In certain embodiments, one model implements more than one role in separate working contexts. Logical separation of the contexts is what matters; different model providers are not required.

### 1.5 Core features and embodiments

The two recipes rest on the following core features:

1. A partition between the Investigator and the Archivist. The Investigator obtains evidence only by querying the Archivist, and the Archivist answers faithfully to the source material without receiving or acknowledging the ACH frame.
2. A multi-round quest in which the Investigator seeks the most novel answers. Novelty is gauged by the change between successive assessments that the Coordinator produces with ACH_Eval, and the Coordinator uses those assessments to direct the Investigator.
3. An Investigator equipped with an index of the corpus, which serves as its map, and a header containing the ACH frame, which serves as its compass, with the Coordinator's assessment-based feedback serving as its metal detector.
4. A question database, produced by the quest, that is reused to distill validated FRDs into witnesses, each witness having exactly one parent QID and exactly one parent FRD.
5. A custom dictionary of reviewed contextual word senses, a canonicalizer built from that dictionary and from sentences in validated FRDs, and a transcoder applied to both witnesses and full hypothesis statements.
6. Formation of deletion-minimal hypothesis coverage sets from the transcoded witnesses, carried as far toward completion as possible before crux identification begins.
7. Crux identification that selects witnesses belonging to the coverage of their home hypothesis but not to a rival hypothesis, the strongest candidates being those that belong to no rival at all.

Recipe 2 operates on validated FRDs, so the bridge that produces them is a required input to Recipe 2.

Other particulars described in this document are examples of certain embodiments. These include numerical settings, word limits, counts, caps, cadences, record formats, rating scales, the number of hypotheses and axes, the choice of models or retrieval services, and the specific methods used within each step. They may be varied without departing from the architecture.


## 2. Recipe 1: the partitioned, Coordinator-guided quest

### 2.1 Preparing the run

Before the quest begins, the run is defined and its inputs are prepared. In certain embodiments, steps whose outputs vary least from one repetition to the next are placed first, and steps that involve more judgment are placed later, so that uncertainty introduced early does not propagate through everything that follows. Converting sources to Markdown is highly repeatable; creating the index is moderately repeatable; writing the hypotheses and the header involves the most judgment.

**Suitability.** In certain embodiments, a question is admitted when three conditions hold: its answer is contestable, the strongest evidence for at least one hypothesis can be placed in the corpus, and the relevant material can be converted to Markdown. Each condition is reported separately rather than folded into a single verdict.

**Corpus.** Sources are converted to Markdown before any model uses them. Each converted source file receives a stable identifier and a record of its provenance and shareability, and all are listed in a manifest. Converting in advance, rather than letting a model convert files silently when it reads them, makes conversion quality inspectable. Duplicates and unreadable conversions are caught at this stage, and sources that could not be obtained are listed.

In certain embodiments, the corpus is loaded into a single retrieval database that serves as the Archivist, and the loaded files are checked against the manifest. The retrieval database is disposable. The committed Markdown files, index, header, and records form the system of record, and the database can be rebuilt from them. Several authorized copies of the same corpus and instructions may provide concurrent capacity, but copies create no independent evidence and no additional sources.

**Eligibility.** In certain embodiments, admission favors sources that are primary relative to the investigation. Whether a document is primary depends on the question rather than on the type of document. A drug label is secondary to the pharmacology it summarizes but primary to a question about failure to warn. A clinical guideline is secondary to the trials it cites but primary to a question about whether the guideline itself is valid. Secondary sources are not prohibited; doubtful ones are flagged during validation.

**Source discovery.** In certain embodiments, sources for every conceptual domain of the question are gathered in one unified search, and expansion along citation graphs from the most relevant sources recovers material the search missed. Separate acquisition for each domain is also permissible. A unified search is aware of the investigation's purpose and can skew selection; the partitioned Archivist and blind validation limit the downstream effect of that skew.

**Ranked index.** An index catalogues every source file once. In certain embodiments, each entry runs roughly 100 to 250 words and records the filename, author, year, and title; a note on relevance to the question; a faithful summary; contradictions and gaps; and a rank, such as A, B, C, or F, reflecting the source's expected usefulness to this investigation. The index is the Investigator's map. It shows where relevant material may be found, but it is never evidence, and its ranks guide attention without establishing any claim.

In certain embodiments, a completeness check matches the manifest, the loaded files, and the index entries against one another. It also looks for missing families of sources, missing comparators, missing adverse evidence, malformed identifiers, and poor ranks, and these are fixed before the run is frozen.

**Hypotheses.** In certain embodiments, a human analyst approves the complete hypotheses before the quest, and models assist only with drafting, proofreading, and quality feedback. In certain embodiments, an intake tool helps the analyst organize materials, specify searches for sources, and draft hypotheses before the header is created; the intake tool has no role once the quest begins.

In certain embodiments, each hypothesis is written in ordinary language with at least four sections:

- a concise hypothesis statement;
- assumptions and antecedent conditions;
- potential falsification context; and
- potential corroboration context.

A concise statement of about thirty words gives several witnesses too little meaning to match against, which is why the fuller written form is used. In certain embodiments, a full hypothesis statement runs to at least roughly 100 words, although the governing requirement is that each section is answered meaningfully, not a word count. The human-written hypothesis remains the controlling statement throughout the run.

**Frames and axes.** The ACH frame contains one or more axes, each asking one material question. In certain embodiments, an axis has two substantive hypotheses and a residual hypothesis. In certain embodiments, the residual hypothesis states that the evidence is insufficient to support either substantive hypothesis cleanly. In other embodiments, it states that no single explanation dominates, for example because different explanations govern different groups, periods, or segments. Either way, the residual hypothesis is written out with the same sections as the substantive hypotheses. Other embodiments use three or four substantive hypotheses together with a residual hypothesis. In practice, fewer hypotheses per axis, with a second axis added when a second material question exists, has worked better than many hypotheses on a single axis. In certain embodiments, the frame has one or two axes. Axes are assessed separately, and their allocations are never multiplied together.

**Conceptual domains.** In certain embodiments, the hypotheses are formulated across a problem domain and a solution domain. The question then becomes whether a mechanism, interpretation, or finding established in one setting carries over to another. Examples include whether a drug's known pharmacology addresses a mechanism of disease in a patient group for which the drug has not been studied, and whether the facts behind a prior legal decision bear on a new case. The domains are conceptual labels. Sources from both are held in one corpus.

**Header.** The Discovery Quest Header, or header, is the investigation's instruction set. In certain embodiments, it contains the mission, the approved hypotheses, the decisive tests, the query rules, the quest loop, guidance on coverage and novelty, and the stopping arrangements. The ACH frame in the header is the Investigator's compass. In certain embodiments, the header is created from the ranked index after the hypotheses are approved. In certain embodiments, the header omits instructions for steps that occur after the quest, such as FRD creation, so that the Investigator chooses questions for their bearing on the hypotheses rather than for producing convenient downstream records.

**Freeze.** In certain embodiments, the following are frozen together before the quest begins: the header; the human-written hypotheses and their internal coverage representation; the index; the manifest; the identity of the retrieval database; the prompts; the configuration; the formats of the question database and query-response records; and the rules for building the language tools of Recipe 2. A material change after the freeze creates a new version of the affected artifacts, and earlier artifacts remain inspectable.

### 2.2 The partition

The first core feature of Recipe 1 is a partition between the Investigator and the Archivist.

The Investigator is not permitted to access the corpus directly. To obtain evidence relevant to the ACH frame, it must query the Archivist. The Archivist is not permitted to understand or acknowledge the ACH frame; it answers each question in a manner faithful to the source material.

In certain embodiments, the separation is enforced by the data path rather than by an instruction that either side could ignore. Source bodies are never placed in the Investigator's working context; corpus content reaches the Investigator only through the Archivist's answers. The Archivist's input consists of the corpus, its fixed citation and formatting instructions, and one question at a time. The Archivist never receives the header or the hypothesis labels, and in certain embodiments it also never receives the index, allocations, source ranks, or the research state.

> See diagram depicting the information boundaries of the quest. On one side, the Investigator and the Coordinator both hold the header and the index, and only the Coordinator holds ACH_Eval and its allocations. On the other side, the Archivist holds the corpus. A single channel connects the Investigator to the Archivist, carrying one source-grounded question outward and one attributed response back. A separate feedback channel runs from the Coordinator to the Investigator and carries qualitative priorities but no allocations.

**Why the partition matters.** The partition does four kinds of work.

- It makes the method of inquiry visible. Because new findings can enter the Investigator's record only through recorded exchanges, the Investigator must externalize every request for information. The result is an inspectable sequence: what was asked, what was returned, what changed, and what was asked next. This makes it harder to blend source selection, interpretation, narrative construction, and self-assessment into one uninspectable operation.
- It keeps coherent storytelling away from the step that reports what sources say. Language models are good at producing explanations that are coherent and satisfying. The Archivist cannot tailor an answer to a story it cannot see.
- It preserves the Investigator's attention for the hypothesis contest. The Investigator reasons over a compact frame, index, and record rather than the full corpus. In one investigation, the index and header together were about 1% of the size of the corpus: roughly 360 KB, against 33 MB across 194 source files.
- It makes each side separately auditable. The Archivist's answers can be checked against the corpus, and the Investigator's questions can be checked against the index, the header, and the transcript.

**Scope of the partition.** Questions are written in the corpus's own terms and may be directional in ordinary language, for example by asking for the strongest evidence that a necessary causal link fails. A question about a particular intervention or objection necessarily reveals part of what the investigation cares about. What the partition withholds is the private frame: the hypotheses and their labels, the assessment, the ranks, and the research history. It does not eliminate every possible influence of framing. An ideal investigator with full access could choose to behave in the same partitioned way; the value of the partition lies in enforcing a useful division of labor on real models with limited attention and context.

**Division of labor between Coordinator and Investigator.** In certain embodiments, the Investigator is score-free. It asks questions and calculates nothing. It does not receive ACH_Eval, does not see the allocation among hypotheses, and does not decide whether a threshold has been met. The Coordinator is score-aware. It runs ACH_Eval, judges which topics have produced meaningful novelty and which only trivial novelty, and gives the Investigator the feedback it needs to calibrate its questions without having to stop and calculate. This division exists for throughput: an Investigator that must repeatedly pause to compute allocations asks far fewer questions. In certain embodiments, neither the Coordinator nor the Investigator reads source bodies during the quest, and the Coordinator does not perform blind validation in its hypothesis-exposed context.

In certain embodiments, the header gives the Investigator a motivated role, for example that of an advocate seeking to justify a clinical trial. The role is constrained by required adverse testing and by the Coordinator's independent assessment, so that energetic questioning does not become selective questioning.

### 2.3 The multi-round quest

The second core feature of Recipe 1 is a multi-round quest in which the Investigator asks the Archivist many rounds of questions with the goal of uncovering the most novel answers.

**Novelty.** Novelty is the decision-relevant change that a batch of answers makes to the evidence record. Its working indicator is the change between the Coordinator's most recent ACH_Eval output and its next ACH_Eval output, and the Investigator seeks the questions whose answers could produce the greatest change. ACH_Eval moves its allocation only when the evidence record changes in a way that bears on the hypotheses; restated content, new wording, and sheer volume do not move it. The size of the change therefore indicates how much a batch of answers mattered. It is an indicator rather than the whole of novelty: consequential findings can change the evidence record without changing the allocation, as when a strong supporting finding and a strong adverse finding offset each other. Such findings are carried forward into FRDs and witnesses all the same. Novel answers include corrections, adverse findings, qualifications that narrow a claim, independent corroboration, and gaps localized precisely enough to guide an experiment, as well as confirmations. An answer does not need to reverse the leading hypothesis to be novel. The objective is substantial novelty rather than a steady trickle of trivial change.

**A round.** In each round, the Investigator:

1. selects the next question, following the header and the Coordinator's most recent feedback;
2. removes hypothesis labels, ranks, internal jargon, and stated goals, and expresses the question in the corpus's own terms, such as authors, mechanisms, populations, and statutes;
3. names the sources the question should draw on and confirms that they exist in the corpus;
4. assigns a unique QID and records the exact question, the named sources, and the header version before submission;
5. submits the question to the Archivist and captures the exact response; and
6. integrates the response into its research state as the header directs, keeping contradictions, qualifications, attribution corrections, and independent corroboration, and suppressing redundant wording but never independent support.

In certain embodiments, each question names one to three sources: two for an ordinary question, one when the task is clarification, depth, or repair of an unclear attribution, and three when comparison or triangulation requires it. Named sources are starting anchors rather than a closed set. Comparing the sources a question named with the sources the answer actually cited also shows whether the retrieval service routed to the sources requested.

In certain embodiments, a browser extension or automation agent carries each question to the Archivist and returns the response to a designated storage location. In certain embodiments, question-and-answer harvests prepared from individual publications seed the quest; such seeds remain subordinate to adaptive question selection and never become a checklist.

The orientation the quest produces is provisional. The quest indicates where the evidence appears to point; validation and Recipe 2 determine what survives source checking and comparison.

### 2.4 Map, compass, and metal detector

The third core feature of Recipe 1 is the equipment the Investigator works with.

| Instrument | Artifact | What it tells the Investigator |
|---|---|---|
| Map | The ranked index | Where relevant material may be found in the corpus |
| Compass | The ACH frame in the header | Which distinctions matter and which direction to search |
| Metal detector | The Coordinator's feedback based on ACH_Eval | Where recent questions found something substantial and where they found only trivial change |

The header's purpose is to drive the discovery of novelty. The Coordinator's use of ACH_Eval supplies enough feedback for Bayesian updating to be carried out effectively over the course of the quest.

**Checkpoints.** In certain embodiments, the Coordinator runs ACH_Eval every five to six rounds. Each run consumes the new query-response records together with the previous cumulative ACH_Eval output and produces a new cumulative output, which becomes the privileged input to the next checkpoint. The sequence of outputs is itself a record of the quest, distinct from the query-response records and the FRDs.

**Feedback.** At each checkpoint, the Coordinator tells the Investigator which topics produced substantial novelty and which produced only trivial change. It names disputed premises, missing comparisons, and the source families most likely to resolve them, and it flags answers that need clarification or repair. In certain embodiments, the feedback is qualitative and never includes the allocation vector, so the Investigator is not tempted to aim its questions at a visible number. The Investigator translates each priority into a source-grounded question.

**Bayesian updating.** Two updates happen at each checkpoint. ACH_Eval revises the allocation among the hypotheses in light of the new answers, and the Coordinator's feedback revises where the Investigator aims its next questions. Together they carry out Bayesian updating in a practical sense: the working assessment is revised as evidence accumulates, and each revision redirects the search. The allocations are structured judgments of what the record warrants (Section 2.5), not computed posterior probabilities.

**The Coordinator's skill matters.** A weak Coordinator uses ACH_Eval for little more than deciding when the quest should stop. A strong Coordinator uses it to identify which topics hold the greatest potential yield of novelty and steers the Investigator toward them.

### 2.5 ACH_Eval

ACH_Eval is a structured estimator of the relative support the evidence record gives each competing hypothesis. In certain embodiments, each run of ACH_Eval:

- builds a condensed evidence record first and assesses the hypotheses second, and emits one cumulative output containing both;
- registers every input once, with its provenance and its disposition;
- maintains a ledger of evidence families with stable finding identifiers, recording quantities, conditions, adverse results, dependencies, and restrictions on use;
- maintains a register of gaps, conflicts, and corrections, quarantining disputed details from settled use without discarding them;
- allocates a fixed number G of integer units among the hypotheses of each axis, each unit representing 100/G percent;
- reports the leading hypothesis, the basis and confidence of the judgment, the principal drivers with their finding identifiers, and the strongest objection;
- compares the new allocation with the previous comparable allocation and labels the cause of any change;
- records prospective forecasts with fixed horizons; and
- names up to three acquisition priorities, each expressed as a targeted question, which the Coordinator can translate into feedback.

**Archivist-only evidence.** Because, in certain embodiments, neither the Coordinator nor the Investigator reads source bodies during the quest, the evidence ACH_Eval receives normally consists entirely of Archivist answers. In certain embodiments, ACH_Eval has an edition specialized for that situation. That edition:

- treats usable, source-attributed answers as working evidence, so that a single well-attributed answer can drive the assessment;
- does not treat missing primary files as an evidential gap;
- never adds weight to the residual hypothesis merely because evidence arrived through the Archivist;
- tracks agreement between separate answers about the same reported finding as a reconstruction tier (one qualifying answer, two concordant answers, or three or more), without awarding points for agreement or treating repetition as validation; and
- resolves conflicts between answers with targeted follow-up questions rather than direct source checks.

Without rules of this kind, an assessment designed around direct source access treats every Archivist-derived finding as permanently provisional and drifts toward the residual hypothesis regardless of what the answers say.

**Compaction.** In certain embodiments, when an output would exceed a length target, a compaction step shortens prose while preserving quantities, conditions, adverse results, provenance, dependencies, and restrictions on use. The output declares whether its carry-forward of earlier evidence is complete or partial.

**Allocation gauge.** The gauge G sets how large a change must be before it registers. In certain embodiments, G is 28, 33, 40, or 50. A finer gauge registers smaller changes. A coarser gauge registers only substantial changes, and so rewards questions whose answers could change the assessment substantially. A gauge that is too coarse ends quests early, because modest but real changes fail to cross a unit boundary and consecutive checkpoints show no change. In certain embodiments, much finer gauges, such as 100 units, are avoided because they register trivial changes and give the Investigator little reason to seek substantial ones. A preliminary comparison of runs at two gauges is consistent with the coarser gauge stopping sooner. The gauge is treated as a tunable parameter.

**Estimating the quality of ACH_Eval's output.** No perfect ACH procedure exists against which ACH_Eval could be scored, and none is needed to estimate how good its output is likely to be. The reference standard is the best available method for evaluating competing hypotheses, not a hypothetical perfect one. The quality of ACH_Eval's output depends on two things: the rules it enforces for categorizing and weighing evidence, and the capability of the model that runs it. Both can be assessed without a perfect reference, and several properties bound or check the output directly:

- **Bounded resolution error.** Because allocations are integers in a gauge of G units, a reported allocation differs from the judgment it expresses by less than about one unit, or 100/G percentage points, for each hypothesis: about three points at a gauge of 33 and two points at a gauge of 50. The same bound gives an unchanged checkpoint a definite meaning: the underlying judgment moved by less than about one unit. The bound covers resolution only; it does not bound errors in the judgment itself.
- **Auditable rules.** The rule set can be audited, rule by rule, against established standards for handling evidence. These include registering every input once with its provenance, keeping stable finding identifiers, and tracking dependence among sources so that repetition is not counted as corroboration. They also include preserving adverse results, quantities, and conditions; quarantining disputed details without discarding them; attributing every change in the allocation to its cause; and stating the strongest objection to the leading hypothesis. A rule set that meets these standards constrains how far a capable model can drift from a well-grounded judgment.
- **Model capability.** The rule set is independent of the model that executes it. As models improve, the same rules yield more reliable output, and the expected quality of a run can be estimated from the audited quality of the rules together with the known capability of the model.
- **Agreement across gauges and models.** In runs to date, assessments of the same inputs at different gauges agreed on the rank order of the hypotheses on every axis tested, and different models given the same inputs have agreed on rank order in most or all cases. Agreement is evidence that a ranking reflects the evidence rather than the idiosyncrasies of one model. Because models can share biases, it is evidence of reliability rather than proof of accuracy.
- **Detection of errors within the evidence.** The rules catch errors inside the sources' own reporting. In one run, ACH_Eval found that a reported significance level was inconsistent with the means, standard deviations, and group sizes reported alongside it.
- **Scorable forecasts.** Each run records forecasts with fixed horizons, so ACH_Eval's forecasts can be scored as the quest proceeds and across runs. This yields an empirical measure of calibration that accumulates over time.
- **Audit against later results.** Coverage-set and crux results for the same corpus can reveal whether ACH_Eval overlooked or misused consequential evidence. They serve as an audit comparison, not as an independent standard of truth.

ACH_Eval's allocations are therefore not calibrated probabilities, but neither are they unconstrained guesses. They are judgments with a known resolution, produced under auditable rules by a model of known capability, and checked by agreement, forecast scoring, and later audit. On that basis, they support the Coordinator's decisions about when to stop and where to direct the Investigator.

### 2.6 Stopping

The Coordinator decides when the quest stops. In certain embodiments, an axis is settled once its allocation has shown no change for a configured number of consecutive checkpoints, three in certain embodiments, and the quest stops when every enabled axis is settled. This is a heuristic implementation of the principle that the quest ends once the expected marginal value of further novelty approaches zero. Consecutive unchanged checkpoints show that the reported judgment has been stable to within about one unit of the gauge. They do not, by themselves, show that further questions have negligible value, since offsetting findings can leave an allocation unchanged. In certain embodiments, stopping additionally requires that the decisive tests have been addressed or found to be absent from the corpus, and that each hypothesis has faced at least one serious adverse test. In certain embodiments, a settled axis is reopened if later answers would move it.

Stopping means that further questioning is unlikely to change the assessment enough to justify its cost, given this corpus. It does not mean the question is settled. Exhausting the retrieval database is not the same as exhausting the literature.

Language models tend to stop early because their curiosity is bounded by the domains they can imagine. In certain embodiments, a human analyst reviews each stop, looks for domains missing from the record, and may direct the quest to continue or add sources. A source added after the freeze goes into the same retrieval database, and the manifest and index are updated. If the new source changes the hypotheses, earlier question choices, earlier interpretations, dictionary senses, or dependencies, the affected work is redone.

### 2.7 The byproduct: the question database

Every issued question is preserved in the question database under a unique, permanent QID. Question records are never merged, even when two questions read alike, because each is the record of its own round. In certain embodiments, each question record contains:

- the run identifier and the QID;
- the round number and order of issue;
- the exact question text and the time it was issued;
- the named sources;
- the header version in force;
- the response identifier and the exact response;
- the sources and passages the response cited; and
- pointers to every FRD, question application, and witness descended from the question.

Several FRDs may descend from one question, because one answer can yield several facts. The question database is the link between the two recipes: the questions that distilled the corpus once, during the quest, are available to distill the validated FRDs again in Recipe 2.


## 3. Bridge: FRD creation and validation

Recipe 2 operates on validated FRDs. This section describes how the Archivist's answers become validated FRDs. The validated FRD database is a required input to Recipe 2; the particular methods used to create and validate FRDs are examples of certain embodiments.

### 3.1 FRD creation

An FRD entry states one claim anchored to one source. It records the source, a locator for the supporting passage, the claim, and the QID of the question whose answer supplied the material.

In certain embodiments, FRDs are created from one query-response record at a time. Every FRD that record can yield is harvested before the next record is opened, and material from different records is never combined into one FRD. A record may yield several FRDs, for example one for each named source that supplied harvestable material. Within a record, the distinct propositions in the answer are mapped to the passages they cite, and compound claims are split into separate FRDs.

Each FRD records exactly one producing QID. Several FRDs may share the same QID, but no FRD carries two producing QIDs. The FRD states what act the source performs, such as reporting a measurement, arguing a position, or citing another work, and it names the actor. Adverse findings, null results, gaps, conditions, numbers, and limitations are recorded rather than smoothed away.

In certain embodiments, FRD text contains no hypothesis labels or framing. Each FRD is then a plain statement of what a source says, and a later step rediscovers which hypothesis the statement bears on. In certain embodiments, the model that ran the quest creates the FRDs, because it understands why each question was asked; in other embodiments, a separate model creates them.

**Harvest accounting.** In certain embodiments, the sources that appear in answers are compared with the sources that produced FRDs, to find under-harvested material. FRDs that share a dataset or a citation ancestor are grouped and tagged OWN_RESULT, DERIVED_FROM(ancestor), or DERIVATIVE_UNKNOWN. Raw counts are shown beside lineage-adjusted counts so that repeated reports of one observation are not mistaken for independent corroboration. Neither count measures authority.

### 3.2 Validation

Validation checks each FRD against the source it names.

In certain embodiments, validation is blind. Each validation packet contains one candidate FRD and only the source file that FRD names. It contains no hypotheses, header, ranks, assessments, or statement of how the FRD will be used. Identifiers such as the QID may travel with the FRD as metadata without revealing the hypotheses.

The validator checks the FRD's structure, the act attributed to the source, the attribution itself, and every clause of the claim against the source. It records enough source text to justify its decision. Before discarding an FRD, it attempts to repair the locator or the claim, and failures remain in the audit trail. When an FRD must be split, each child FRD keeps the parent's QID. In certain embodiments, the validator also distinguishes passages that support a claim only jointly from passages that each support it independently.

In certain embodiments, the context that created the FRDs packages a validation kit: the candidate FRDs with their identifiers and QID metadata, self-contained blind-validation instructions, a location for the validation output, and a folder for the source files. A fresh context then performs the validation. The kit excludes the header, the index, the hypotheses, assessments, quest state, the original query-response text, and any downstream conclusions. The validator opens only the source named by the FRD under review, plus any original file needed to resolve a conversion problem.

**Keeping validation blind.** Exposure to the hypotheses runs one way. A context that has seen the hypotheses or the intended outcome is retired from validation duty. It may continue with later steps, but it does not validate further FRDs. The most common exposure is indirect, as when an operator asks a validating context whether enough validated entries exist to write a particular document; that question discloses the goal. In certain embodiments, the operator avoids this by completing validation of a batch before asking any question that discloses the goal, or by branching the conversation at a point before the exposure and continuing validation in the unexposed branch. Adversarial instructions reduce the risk of contamination but do not remove it. The structural protection is the boundary itself.

**Source-assignment audit.** In certain embodiments, after the blind verdict is locked, a separate comparison may record that another available source anchors the claim more directly (BETTER_SOURCE_AVAILABLE), that an artifact repeats support already present without adding an independent contribution (REDUNDANT_WITH), or that two passages of one source pull in different directions (INTRA_SOURCE_TENSION). These labels update lineage without changing the verdict.

**What validation establishes.** Validation establishes what a source says, to the extent the check succeeds. It does not establish that the source is true, that its evidence is independent, that it applies to another setting, or that every relevant passage was found. Checking the claims that were extracted cannot reveal passages that retrieval never surfaced. In runs performed to date, roughly 80 to 85 percent of candidate FRDs were confirmed, 10 to 15 percent were attributed to the wrong source, and 5 to 10 percent were wrong. These rates are why Recipe 2 starts from validated FRDs rather than from raw answers.

### 3.3 Coverage review

Because validation cannot find what retrieval missed, coverage is reviewed separately. In certain embodiments, the review is performed for each conceptual domain and includes three checks:

- **Capture fidelity.** Every source cited in the answers either produced FRDs or has a recorded reason it did not.
- **Hub identification.** The identifiers of the most-cited sources are entered, one at a time, into services that list related work within a field. The returned lists are merged, and papers are ranked by how many seeds returned them. A paper returned for many seeds is, in practice, a hub of its domain.
- **Hub presence.** Each hub is checked for presence in the corpus and for citation in the answers.

When a hub is missing from the record, the Archivist is first asked about it directly by author and title. If the hub is in the corpus but is not being cited, the index and header are adjusted to direct attention to it, and the affected part of the quest is repeated. If the hub is absent from the corpus, it is acquired, converted, added, indexed, and questioned. In certain embodiments, an analyst also searches the retrieval database for terms taken from the questions and answers; failure to find them signals that something may be missing.

Passing the review shows that the record is anchored to the central work of each domain. It does not show that no peripheral but decisive source was missed. Where such a source is suspected, the correct output is a named gap rather than a claim of completeness.

**Rankings as diagnostics.** In certain embodiments, several independently produced rankings of sources are compared: rank in the index, frequency of citation in the Archivist's answers, number of FRDs per source, and hub rank. Ranking is a simple task that different models can repeat at different steps, which makes it one of the few quantities comparable across steps. Disagreement among these rankings has potential as a diagnostic of where the retrieval service's notion of salience and the sources' actual relevance diverge.


## 4. Recipe 2: from validated FRDs to crux candidates

Recipe 2 carries out four operations. Apart from the core features listed in Section 1.5, the procedures described in this section are examples of certain embodiments.

- it distills validated FRDs into witnesses;
- it rewrites the witnesses and the full hypothesis statements into one controlled English;
- it assembles the witnesses into deletion-minimal coverage sets for each hypothesis; and
- it identifies the witnesses that distinguish the hypotheses.

> See diagram depicting Recipe 2 in the context of the whole architecture. A human-specified ACH frame, consisting of competing hypotheses and an investigation objective, leads to an adaptive quest that selects a high-value question. That parent question, applied to the corpus, yields an Archivist response; this is the first distillation pass. The response becomes an FRD. The validated FRD, together with the same parent question, yields a witness; this is the second distillation pass. A custom dictionary and canonicalizer derived from validated FRDs, and the full hypothesis statements, feed a transcoding step. Transcoding yields formalized witnesses and formalized hypothesis statements that share terminology and syntax. These feed the formation of deletion-minimal hypothesis coverage sets, which feed crux identification. A traceability chain runs from a crux witness to its parent FRD and on to the primary source. Captions state that signal means relevance to the ACH frame and noise means irrelevance to it, and that formalization reduces ambiguity while crux identification remains subject to semantic review and practical evaluation.

### 4.1 Question-guided witness creation

A witness is a concise answer to a question, drawn from one validated FRD. A language model applies an approved question to one validated FRD. It decides which of the FRD's content is relevant to the question and how that content answers the question, and it writes the compressed answer as the witness. The question does not act on the FRD by itself; it gives the model the reason the information mattered.

**Parentage.** Every witness has exactly one parent QID and exactly one parent FRD. FRDs and questions are not exclusive to each other: more than one question may be applied to the same FRD to extract more than one witness, and one question may be applied to several FRDs. One question applied to one FRD yields exactly one witness. Each application of a question to an FRD is recorded as a question application. Applying another question to an FRD does not give the FRD a second producing QID. Witnesses are never merged, even when two appear equivalent after transcoding, because each is the child of a distinct application and each may contribute to a different coverage set.

**Which questions are applied.** The FRD's producing question, the question whose answer caused the information to be retrieved, is applied first. In certain embodiments, additional questions are allocated using rough rankings of the sources in the index, the FRDs in the FRD database, and the questions in the question database, so that questions of greater value produce more witnesses than questions of lesser value. Questions are not applied to every FRD indiscriminately. In certain embodiments, each FRD receives at most a small number of question applications. In certain embodiments, the additional lenses include:

- **the cluster-best question:** within a cluster of related FRDs, the question most directly related to answering at least one hypothesis, applied to every FRD in the cluster;
- **the nearest-neighbor question:** the most relevant question from the neighboring cluster that shares the most sources with the FRD's cluster; and
- **question transcoding:** a best-effort variant in which a quest question is rewritten before it is applied, for example to make it better suited to compressing FRDs.

Each witness records which lens produced it.

**Why the producing question is the default lens.** The argument has three steps. The question was selected because its answer could advance an unresolved issue. The validated FRD arose from the answer to that question. The question therefore supplies an already-documented reason for deciding what a shorter representation of that FRD must keep. A generic instruction to summarize leaves the compressor to guess what matters.

Consider an investigation that asks whether a recorded pressure drop was a physical event or a sensor artifact. A question asks what independently measured pressure and calibration results were recorded during the alarm interval, and which measurements were simultaneous. Validation establishes that an independent gauge read normal, but only after the alarm, not during it. A generic summary might keep "an independent gauge showed normal pressure," which is related to the source but misleading for the inquiry. A witness produced by the same question keeps the timing limitation, because that limitation determines whether the FRD answers the question at all.

The producing question is a justified default, not a guarantee. A question may have been poorly framed, its presupposition may fail validation, or the most useful content of an FRD may be incidental to it. Additional lenses address those cases, while the original QID remains the record of the FRD's origin. When a question compared several sources, a single-source FRD may support only part of the answer; the witness preserves that partial contribution rather than inventing the missing cross-source conclusion. When an FRD cannot yield a faithful, useful answer within the length limit, the compression failure is recorded rather than covered over.

**Content rules.** A witness uses the validated claim as corrected or qualified by the validator's verdict, checked against the source text attached to the FRD. Wording rejected during validation cannot re-enter through compression; if the claim and the verdict are materially inconsistent, the FRD is sent for repair rather than resolved by choosing a convenient reading. The witness preserves the qualifications each retained assertion needs in order to remain faithful, including countervailing findings and exceptions. Omitting irrelevant detail is legitimate. Omitting something that changes the answer to the question is a material omission, even if every remaining sentence is individually supported. An FRD does not need to contain a custom-dictionary term in order to produce a witness.

**Length.** In certain embodiments, a witness has a hard maximum of 60 words before transcoding and 80 words after transcoding. Words are counted as whitespace-separated tokens of witness prose, including attribution, qualifications, and dictionary sense labels, and excluding metadata. A numeral or an unspaced hyphenated compound counts as one word. The limits are ceilings, not targets. When a witness cannot preserve its material meaning within the ceiling, repair is attempted first. If repair fails, the failure is recorded with its parent records rather than dropping the qualification, and a different common ceiling may be considered. Neither limit guarantees that compression is lossless.

**Metadata.** A witness carries no metadata other than the identifiers of its parent QID and parent FRD. Those identifiers do more work than their size suggests. They are keys into historical databases that store every earlier form of the material: the query-response record, the candidate FRD, the validated FRD, and the witness before transcoding. A witness's pre-transcoding text is found through these keys rather than stored on the witness. Links to dictionary entries need no separate metadata either, because in controlled English every dictionary term appears in its visible `WORD (modifier)` form (Section 4.3).

**Fidelity audit.** Each witness is audited against its parent FRD and question in two directions. The auditor receives the exact producing question, since an identifier alone is not enough; the parent FRD's citation, claim, source text, and verdict; and the witness. It asks two questions separately:

- **Unsupported assertion.** What does the witness assert more strongly, more broadly, or differently than the validated FRD permits?
- **Material omission.** What meaning needed to answer the question can a reader no longer recover from the witness?

For each problem, the auditor identifies the words or the missing meaning, explains the consequence, and names the affected protected property where useful (Section 4.3). It also asks what the strongest reading is that the witness permits but the FRD forbids, and whether a reader of the witness would recover the same source position, a weaker one, or a wrong one. A credible forbidden reading is not dismissed merely because no unsupported assertion was listed. The outcome is PASS, REVISE_WITNESS, REPAIR_FRD, or HUMAN_REVIEW, with a short reason.

In certain embodiments, an independent approximation check by a separate model or a fresh context repeats these questions without the constructor's self-evaluation, and additionally deletes each sentence of the witness to see what is lost. When different compression methods are compared, audit items are mixed and method labels are concealed, including labels embedded in identifiers. A pass is a best-effort judgment, not proof. In one pilot, 56 of 64 witnesses written to the 60-word ceiling passed the audit, and 8 required revision.

### 4.2 The custom dictionary

**Why it is needed.** Some terms matter more to the ACH frame than others, and the terms that matter most are the most likely to carry several nuanced meanings. A witness and a hypothesis can use the same word for different things. If the run treats those uses as one term, unrelated claims appear to match. Identifying the right nuance requires matching on the specific lexical meaning of a word. The more likely a model is to identify that meaning, the more likely it is to interpret correctly the contextual meaning needed to match witnesses to hypothesis statements and to form coverage sets. The unit of the dictionary is therefore not the word but each reviewed contextual sense of the word.

**Harvest.** In certain embodiments, the dictionary harvest follows these rules:

- The dictionary is built only from the claim text of validated FRDs, as corrected. Metadata, identifiers, citations, filenames, prompts, validation commentary, and attached source blocks are excluded.
- One identified tokenizer and base-form procedure is used throughout, with its name, version, settings, and manual corrections recorded. Its token counts are kept distinct from the whitespace word counts used for witness ceilings.
- Nouns, verbs, adjectives, and adverbs are counted by base word form, so that *offer*, *offers*, and *offered* count together, while every original form is preserved in its sentence. Ordinary function words are excluded unless the corpus uses one as a quoted or technical term.
- Where comparable counts are available, a candidate's rate in the validated FRDs is compared with its rate in a versioned reference corpus of ordinary English. The resulting relative frequency helps prioritize review. It does not decide meaning or approve entries, a missing reference count does not stop review, and an unavailable ratio is left unestimated rather than invented.
- A candidate that occurs in at least three distinct validated-FRD sentences is sent to contextual review.
- No target dictionary size is set. Every entry that meets the requirements is published, and no weak entry is added to reach a quota.

**Sense review.** For each candidate, every occurrence is collected with its sentence and enough surrounding text to understand the use. Every pair of occurrences is then rated on a five-point scale:

- 4: same sense;
- 3: same sense with minor contextual variation;
- 2: related but distinct senses;
- 1: different senses;
- 0: cannot decide.

In certain embodiments, two independent review passes that cannot see each other's work rate the pairs, and either pass may be performed by a model or a person under the same frozen instructions. A disagreement that would move a sense boundary goes to human review rather than being averaged, and disagreements are identified from the complete set of pair ratings. Occurrences are placed in one sense group only when every pair within the group is rated 3 or 4. A 2, a 1, or an unresolved 0 prevents automatic grouping. This conservative rule prevents a chain of merely similar uses from silently becoming one meaning.

**Entries.** Each approved sense group becomes one dictionary entry, written as `WORD (modifier)`, where the modifier has no more than five words and distinguishes the sense without deciding a dispute the sources leave open. In certain embodiments, an entry records:

- an immutable identifier;
- the base word form and the exact `WORD (modifier)` label;
- a plain-language definition and its scope;
- every occurrence identifier and three example sentences;
- allowed scoped aliases and related but separate entries; and
- reviewer decisions, version, and status.

In certain embodiments, an entry becomes active only when its sense group has at least three distinct supporting sentences. Sentences, not occurrences, are counted, so three uses of a word in one sentence supply one example. Where possible, the three sentences come from three different FRDs. A plausible sense with fewer examples is held as provisional: it is not used in the run, and its occurrences are preserved for later. The number of senses a word has in the dictionary is therefore the number of reviewed sense groups that meet the example requirement, not a number chosen in advance.

**Example.** The word *control* appears in five validated-FRD sentences, but not in a single sense. Three sentences use it for an experimental comparison group, producing the active entry `control (experimental comparison)`. Two use it for authority over an organization, and that sense is held as provisional for lack of examples. Five occurrences of the word do not supply three examples for each meaning.

> See diagram depicting the creation of dictionary entries. Validated FRD claim text leads to finding recurring candidate words, then to collecting each occurrence with its sentence and context, then to comparing occurrences to decide whether they use the word in the same sense, then to grouping occurrences by meaning, with the requirement that every pair within a group pass review. A decision point asks whether the sense group has three distinct supporting sentences. The yes branch leads to an active dictionary entry in `WORD (context modifier)` form, with definition, examples, and scope. The no branch leads to a provisional sense that is not used in the run and whose examples are preserved. An accompanying table shows the worked example of *control*.

The three-sentence requirement is a working rule of certain embodiments, not a law of language. Ordinary-English frequency guides the order of review but does not determine meaning or approve entries.

### 4.3 The canonicalizer

**What it is built from.** The canonicalizer is built from the frozen custom dictionary and from grammatical examples found in validated FRDs. To canonicalize sentences, it is necessary to know how the terminology was actually used in the sources, and the exact word-for-word sentences preserved in validated FRDs supply those examples. The canonicalizer's output is a controlled grammar profile for the run.

**What it does.** The canonicalizer creates a shared house style, so that witnesses and hypotheses read as though the same careful technical writer had written them. It standardizes wording and structure without imitating any individual author and without changing meaning. It reduces the number of grammatical constructions used during comparison and encodes the dictionary's custom terms.

**Protected properties.** Canonicalization may never change any of the following:

- who said or did something (attribution, actor, and action);
- whether a statement affirms or denies (polarity);
- how a statement presents possibility, probability, uncertainty, or necessity (modality);
- conditions and unresolved alternatives;
- identity and role;
- time, quantity, and scope; and
- the person, object, passage, event, or idea a phrase refers to (the referent).

**Building the grammar profile.** In certain embodiments, the grammatical shapes needed to preserve these properties in the run's material are listed first. Constructions that express the same relationship with the same protected properties are grouped; a construction joins a group only after a reviewer finds it meaning-preserving in both directions. The preferred construction for each group is chosen in this order:

1. preserve every protected property;
2. make the actor, the source, and the referent explicit;
3. make negation, conditions, and the scope of modifiers unambiguous;
4. use the fewest clauses and words that preserve meaning; and
5. only as a final tie-break, prefer the construction used most often in validated-FRD examples.

In certain embodiments, the profile prefers explicit nouns over ambiguous pronouns, explicit source attribution, active voice when the actor is known, retained passive voice when the actor is unknown, one main claim per sentence when splitting does not change scope, "If [condition], then [result]" for conditions, explicit repetition where ellipsis would create ambiguity, and visible alternatives rather than a silent choice among them.

The canonicalizer never normalizes away a difference in attribution, polarity, modality, condition, identity, role, time, quantity, scope, or unresolved alternatives. It preserves the input's number, tense, and quantifiers. Similar spelling or a shared base word never licenses substitution between different dictionary senses. For every custom term, the approved entry and any scoped aliases, including reviewed inflected forms, are recorded; a scoped alias may be used only in its recorded scope and never as a global replacement.

**Notation.** In certain embodiments, parentheses are reserved for dictionary sense labels in `WORD (modifier)` form, and every other parenthetical is written in square brackets. Parentheses in source-derived text are converted to square brackets during canonicalization. Any parenthetical in controlled English therefore marks a dictionary binding, and each binding is visible in the text itself without additional metadata.

**Conformance tests.** Each preferred construction is tested with meaning-preserving examples and with near-miss examples involving reversal of actor and object, negation, uncertainty, conditions, and ambiguous attachment of modifiers. A construction passes only when its canonical form preserves the intended meaning and refuses the near-miss meaning. When the profile cannot express a protected distinction safely, the result is REQUIRES_REVIEW, or a human records an APPROVED_EXCEPTION with its reason and scope. Text is never forced into the nearest available pattern. Test inputs, expected results, actual results, and the profile version are preserved.

**Freezing and reuse.** The dictionary, grammar profile, test examples, and reviewer decisions are frozen together; a change creates a new version and triggers transcoding again for the affected artifacts. The canonicalizer is the rule set and language map from which the transcoder is built; it is not itself the encoded output. In certain embodiments, a later run reuses an earlier dictionary, canonicalizer, and transcoder to save time. Reuse is most appropriate when the hypotheses are unchanged, and it still requires comparison against the new run's validated-FRD vocabulary and grammar; new or changed senses create new versions rather than silently altering the reused tools.

### 4.4 The transcoder

**What it is.** The transcoder is the executable English-to-English process compiled from one frozen dictionary and one frozen grammar profile. The same transcoder version is applied, separately, to every witness and to every full hypothesis statement before semantic matching.

**Steps.** For each input, the transcoder:

1. preserves the exact original text and assigns an input identifier;
2. locates candidate custom terms and creates a dictionary binding for each occurrence;
3. leaves an occurrence unresolved when its context does not safely select one sense;
4. replaces approved bindings with their exact `WORD (modifier)` forms or permitted scoped aliases;
5. rewrites the sentence using the preferred constructions of the grammar profile;
6. produces a normalization preview showing every term substitution, referent clarification, sentence split, reordering, and grammatical rewrite;
7. compares the original and transcoded text for every protected property; and
8. releases the transcoded text only when the conformance result is PASS or a human has approved a recorded exception.

**Binding.** In certain embodiments, two independent binding passes compare each candidate occurrence's local context with the definitions and example sentences of every dictionary entry that shares its base word form. A binding is approved automatically only when both passes select the same entry and neither identifies a conflict with a protected property. A disagreement, several plausible entries, or insufficient context yields REQUIRES_REVIEW. If human review cannot select an entry safely, the occurrence stays unresolved and the artifact is withheld from matching; the most frequent sense is never chosen merely to keep work moving. A term absent from the dictionary remains ordinary English, and the transcoder never creates a new active entry while processing a witness or hypothesis.

**What it may not do.** The transcoder may clarify a referent when only one referent is supported. It may not invent context, choose among unresolved meanings, strengthen or weaken uncertainty, reverse an actor and an object, turn a report of a claim into an assertion of the claim, add a causal link, or resolve a dispute between sources. An output of REQUIRES_REVIEW or ABSTAIN does not enter semantic matching until it is resolved, and the raw witness or hypothesis remains preserved and unchanged.

**Records.** In certain embodiments, every transcoded artifact records its input identifier and raw text, its output identifier and controlled-English text, the dictionary and grammar versions, the binding decisions, the rewrite trace, the protected-property comparison, the reviewer, and the conformance status.

**Lengths.** Transcoding lengthens text because dictionary labels and explicit restructuring add words. In certain embodiments, a witness may grow from at most 60 words to at most 80, and a full hypothesis statement of roughly 100 words may grow to roughly 140. Hypothesis statements are not capped. Each representation is checked against its own limit, and a failure is flagged rather than resolved by dropping material meaning.

**Why transcoding matters.** Transcoding both the witnesses and the full hypothesis statements with the same tools gives them shared terminology and consistent syntax. That consistency makes it more likely that semantic matching finds every valid relationship between witnesses and hypothesis requirements. In turn, it becomes more likely that every deletion-minimal coverage set that exists is actually formed, which is a precondition for reliable crux identification (Section 4.8). In certain embodiments, transcoding is what makes compact coverage sets of four, five, or six witnesses achievable. Transcoding standardizes representation; it does not determine truth, and coverage is always computed from the approved transcoded text rather than from metadata.

**Conformance gate.** Before release to matching, an artifact is checked for compression fidelity, dictionary bindings, scoped aliases, protected properties, compliance with the grammar profile, length, leakage of withheld information, and correspondence between raw and transcoded forms. An artifact with an unresolved binding, an unapproved grammar exception, an unexplained change to a protected property, or a missing transformation trace is withheld, and each defect is routed to the step responsible for it. Meaning is never patched during matching. Witnesses are released or withheld individually on their actual results; a high pass rate across the run does not approve a witness that still has a material defect.


### 4.5 Coverage representation of hypotheses

Hypotheses are written by people in ordinary language, and people are never asked to write or think in smaller units. In certain embodiments, after a human analyst approves a hypothesis, a language model derives from its written sections an internal set of coverage units for matching:

- **REQUIRED_SUPPORT units** state what must receive affirmative witness coverage before the hypothesis is completely covered.
- **CONTEXTUAL_CONSTRAINT units** state assumptions, antecedent conditions, boundaries, or qualifications that every coverage set must continue to satisfy.
- **ADVERSE_TEST units** preserve the potential falsification context: conditions or findings that could count against the hypothesis. They remain visible but are not required affirmative coverage.
- **CORROBORATING_EXPECTATION units** preserve the potential corroboration context: findings the hypothesis leads one to expect. They remain visible but are not automatically required.

Deriving units may clarify and tag what the analyst wrote. It may not add a factual commitment or rewrite the hypothesis. The written hypothesis remains the controlling statement, and the residual hypothesis receives coverage units in the same way as the substantive hypotheses. In certain embodiments, the units are derived from, or carried through, the same transcoder as the hypothesis text they come from, so that witnesses and units are compared in the same controlled English.

### 4.6 Semantic matching

**Inputs.** Semantic matching compares transcoded witnesses with the coverage units of the transcoded hypothesis statements. Coverage is determined from text alone. Witness metadata, provenance, source counts, and independence never supply coverage and never alter a coverage relation.

**Relations.** For each pair of a witness and a coverage unit, a relation is assigned:

| Relation | Meaning |
|---|---|
| EQUIVALENT | The witness and the unit express materially the same claim at the same strength and scope. |
| WITNESS_ENTAILS_UNIT | If the witness is accepted as written, the unit follows; the witness is at least as strong and specific as the unit. |
| UNIT_ENTAILS_WITNESS | The unit would imply the witness, but the witness is weaker or less specific. This is relevant partial support, not complete coverage. |
| PARTIALLY_COVERS | The witness supplies a material part of the unit, but neither text implies the other completely. |
| CONTRADICTS | The witness and the unit cannot both be accepted as written under the same recorded scope and conditions. |
| NO_SEMANTIC_RELATION | No material support, contradiction, or partial coverage was found. This says nothing about whether the sources are independent. |
| ABSTAIN | The text does not support a reliable decision. This is an honest unresolved result, not a failed answer. |

In certain embodiments, two independent review passes that cannot see each other's results each assign exactly one relation and supply a match trace naming the words, grammatical structures, and protected properties that justify it. A relation without a trace is invalid. A relation is approved automatically only when both passes select it and their traces do not conflict. Otherwise a human reviewer approves one relation or records ABSTAIN; relation labels are never averaged.

**What counts as coverage.** A witness completely covers a REQUIRED_SUPPORT unit only through EQUIVALENT or WITNESS_ENTAILS_UNIT. UNIT_ENTAILS_WITNESS and PARTIALLY_COVERS remain visible but never provide complete coverage alone. Several partial matches may cover a unit together as a jointly sufficient group. Such a group is approved only when its members' combined text entails the unit, every member contributes something material, and no member covers the unit alone. The exact group and each member's contribution are recorded, and the witnesses remain separate artifacts. Every CONTEXTUAL_CONSTRAINT must remain satisfied, and results for ADVERSE_TEST and CORROBORATING_EXPECTATION units remain visible without becoming required affirmative coverage.

**Matcher qualification.** A matcher earns its place by what it refuses, not only by what it finds. Two statements can share almost every word and mean different, or even opposite, things. A matcher that follows wording rather than meaning will merge them, and a merged pair quietly corrupts every coverage set built on it. This is the failure the dictionary, canonicalizer, and transcoder are designed to prevent. In certain embodiments, therefore, a matcher version must pass a set of adversarial test pairs before it may create coverage options. The following pairs illustrate the patterns tested:

| Requirement | Witness | What changed | Required relation |
|---|---|---|---|
| The council appointed the prince. | The prince was appointed by the council. | Voice changed; the actor is preserved. | EQUIVALENT. A qualified matcher must still find this match; refusing everything is not rigor. |
| The council appointed the prince. | The prince appointed the council. | Actor and object reversed (identity and role). | NO_SEMANTIC_RELATION. The same words reordered: overlap is total, but the claim is different. The two claims are not equivalent, yet both could be true; CONTRADICTS would require further recorded conditions that make them incompatible. |
| The rite must be performed by the prince. | The rite may be performed by the prince. | Necessity weakened to possibility (modality). | UNIT_ENTAILS_WITNESS. Not a contradiction, but not coverage: the witness is weaker than the requirement. |
| The figure holds a mortal office. | The commentary argues that the figure holds a mortal office. | An assertion became a report of one (attribution). | PARTIALLY_COVERS. That a source holds the position is material support, but it is not the position established. |
| The revised list of rulers and priests is preserved. | The list of revised rulers and priests is preserved. | A modifier attaches elsewhere (scope). | ABSTAIN. Nothing in the text decides whether the list or the rulers were revised. |

> See diagram depicting pairs of statements that must not be matched naively. Each row shows a requirement and a witness that share most of their words, identifies the single meaning-bearing feature that changed (voice with the actor preserved, reversal of actor and object, necessity weakened to possibility, an assertion turned into a report of an assertion, and a modifier attached to a different word), and gives the relation a qualified matcher must return in each case.

In certain embodiments, the qualification set contains at least fifteen frozen test pairs written in the run's vocabulary, with at least two pairs for each of these patterns:

- reversal of actor and object;
- active and passive wording that preserves the actor;
- affirmation versus denial;
- possibility versus necessity;
- a source reporting a claim versus asserting it;
- a claim inside a condition versus an unconditional claim; and
- high word overlap with changed roles or relationships.

The set includes pairs whose relation must stay the same and pairs whose relation must change. Results are reported for each pattern and never averaged into a single score. A failed pattern does not merely lower an average: it removes automatic matching for every case that depends on that pattern, and those cases return ABSTAIN until the matcher or a human reviewer resolves them. Passing qualifies a matcher only for the capabilities actually tested; it does not demonstrate general language understanding. A relation is a judgment about two pieces of text and says nothing about whether either is true.

### 4.7 Deletion-minimal hypothesis coverage sets

**Definitions.** A set of witnesses has complete coverage of a hypothesis when its witnesses together represent every REQUIRED_SUPPORT unit and every CONTEXTUAL_CONSTRAINT remains satisfied. Results for ADVERSE_TEST and CORROBORATING_EXPECTATION units remain visible without becoming required. A set with complete coverage and no approved incompatibility among its members is deletion-minimal when no witness can be removed without leaving a required unit uncovered or breaking a necessary dependency.

Deletion-minimal is a test that each set either passes or fails; it is not a contest between sets. It does not mean smallest by number of witnesses, uniquely valid, or strongest in evidentiary quality. Several different deletion-minimal sets can completely cover the same hypothesis, and all of them are kept.

**Formation.** In certain embodiments, sets are formed as follows:

1. For each REQUIRED_SUPPORT unit, list every coverage option in the approved matching record. A coverage option is either one witness that completely covers the unit or an approved jointly sufficient group, which enters as one option while its witnesses remain separate.
2. If any required unit has no coverage option, report NO_COMPLETE_COVERAGE, identify the uncovered unit, and present the gap for analyst review and further research. Never manufacture or weaken a witness to continue.
3. Order the required units from fewest to most coverage options. Starting with the least-covered unit reduces wasted search without changing which sets are valid.
4. Build candidate sets by choosing at least one coverage option for every required unit, adding every witness of a chosen group.
5. Reject a candidate immediately if it leaves a contextual constraint unsatisfied, completes an approved incompatibility, or omits a necessary dependency.
6. For each surviving candidate, try removing each witness in a stable order. Permanently remove a witness when the remaining set still has complete coverage and remains valid, and repeat until no further witness can be removed.
7. Record the remaining witnesses as a deletion-minimal set. For each member, store a removal certificate: the coverage or dependency failure its temporary removal caused.
8. Repeat across every combination of coverage options. Store each set by its sorted witness identifiers and never record the same set twice.

The search is declared EXHAUSTIVE only after every combination of coverage options under the frozen inputs and constraints has been checked. Otherwise it is declared RESOURCE_BOUNDED: the stopping limit and unexplored combinations are recorded, together with a statement that further deletion-minimal sets may exist. For every set, the witnesses, parent FRDs, producing QIDs, question applications, coverage options, jointly sufficient groups, dependencies, constraints, removal certificates, search order, and matching record are preserved. Witness counts and source counts never decide whether a set has complete coverage; coverage depends only on the semantic mapping between transcoded witness text and the transcoded hypothesis.

**Example.** A hypothesis has two required units, A and B, and semantic review has approved this coverage: witness W1 covers A; witness W2 covers B; witness W3 covers both A and B.

| Witness | Covers A | Covers B |
|---|---|---|
| W1 | Yes | No |
| W2 | No | Yes |
| W3 | Yes | Yes |

The set {W1, W2} is deletion-minimal: dropping either witness leaves a unit uncovered. The set {W3} is also deletion-minimal: dropping its only witness leaves both units uncovered. Only {W3} has the fewest witnesses, but both sets pass the test. Discarding {W1, W2} for being larger would throw away a second, independently valid way in which the corpus covers the same hypothesis.

> See diagram depicting the formation of deletion-minimal coverage sets. Formalized witnesses and a formalized hypothesis with identified coverage requirements lead to semantic matching, then to recording which witnesses, or approved groups of witnesses, fully cover which requirements, and then to finding witness sets that cover every required part of the hypothesis. One branch, taken when no full coverage exists, shows the gaps for analyst review and further research. The other branch tries deleting each witness in turn and asks whether every single deletion breaks full coverage. If not, a redundant witness is removed and the check repeats. If so, the set is recorded as deletion-minimal and preserved alongside every other set that passes. The accompanying example shows witnesses W1, W2, and W3 covering requirements A and B, with both {W1, W2} and {W3} passing.

**Why every set is kept.** Each deletion-minimal set is a distinct route by which the corpus covers the hypothesis. Crux identification depends on knowing all of those routes, as explained in Section 4.8. Equivalent or nearly identical witnesses may belong to different sets, and those sets are preserved rather than collapsed to save computation.

**Size cap.** In certain embodiments, coverage sets are limited to a maximum number of witnesses, for example four, five, or six. The cap is an adjustable setting. A tighter cap produces greater compression, because fewer witnesses survive into coverage sets, but it increases the risk that crux statements are lost. A hypothesis whose complete coverage would require more witnesses than the cap allows is reported as exceeding the cap rather than as uncovered, so that the cap never makes a covered hypothesis appear unsupported.

**Incompatibilities and dependencies.** In certain embodiments, the matching record also contains approved incompatibilities, meaning combinations of witnesses that cannot coherently appear in one set, and necessary dependencies, meaning witnesses whose contribution requires another witness. The procedure for approving incompatibilities and identifying dependencies may vary between embodiments.

**What coverage does not establish.** Complete coverage is not proof of truth. A completed search is different from the sets found so far.

### 4.8 Crux identification

**The required outcome.** Crux identification selects the witnesses that help cover their home hypothesis while one or more rival hypotheses cannot accommodate them. The strongest candidates belong uniquely to their home hypothesis: no rival can accommodate them. Its practical value is to reduce a large corpus and witness registry to a small number of data needles that deserve concentrated human investigation. An analyst can try to undermine a crux witness. If the witness fails, the coverage set that depends on it becomes vulnerable in exactly the way its removal certificate records.

**Sequencing requirement.** Crux identification begins only after deletion-minimal coverage sets have been formed, as completely as possible, for every hypothesis. A judgment that a witness does not belong to a rival is only as good as the record of the rival's coverage. Suppose sets A and B have been formed for a rival hypothesis, but a valid set C has not, because a matching relation was missed. A witness absent from A and B, or in conflict with both, would be wrongly judged foreign to the rival if set C accommodates it. Errors of this kind compound: a missed match yields a missing set, a missing set yields a false crux, and a false crux sends the analyst after the wrong evidence. Transcoding, matcher qualification, and exhaustive formation of coverage sets exist in large part to make complete formation achievable before crux identification begins.

> See diagram depicting the risk of compounding error when crux identification runs on an incomplete record of coverage sets. A fixed rival hypothesis is shown at the top. Beneath it are two coverage sets that have been formed and a third valid set that has not yet been formed. A witness is shown absent from, or in conflict with, the two formed sets but accommodated by the unformed set. A path shows how the missing set would cause the witness to be misclassified as a crux, and a caption states that crux identification therefore waits until coverage-set formation is complete.

**Home requirement.** A crux candidate must belong to at least one deletion-minimal coverage set of the hypothesis it supports, called its home hypothesis. A witness that no hypothesis needs is not a crux, however badly a rival fares against it.

**Two screens.** In certain embodiments, a witness becomes a crux candidate against a rival only when both of the following screens indicate that it does not belong to that rival.

*Membership screening.* The first screen asks whether the witness appears in any deletion-minimal coverage set of the rival. A witness that appears in none passes. Membership screening is inexpensive, because it consults sets that have already been formed. It also passes many witnesses that are merely irrelevant to the rival, so on its own it yields many false positives. Its reliability depends on how completely the rival's sets were formed, which is why the sequencing requirement applies.

*Portability testing.* The second screen tests the witness against a frozen rival theory. Each hypothesis is compiled once, before testing, into a machine-readable frozen theory. The theory states every condition a valid coverage set must satisfy: the REQUIRED_SUPPORT units with their approved coverage options, the CONTEXTUAL_CONSTRAINT units, the necessary dependencies, and the approved incompatibilities. Because the theory states the conditions rather than listing sets, it implicitly contains every valid coverage set of that hypothesis, including any that formation did not reach. The frozen theory is versioned. In certain embodiments, it is compiled without the coverage-set size cap, so that a rival able to accommodate a witness only through a set larger than the cap is not mistaken for a rival unable to accommodate it.

For each witness and each rival, a solver answers two separate questions:

- **T1, consistency.** Can the witness be held together with what the rival's frozen theory asserts, meaning its units and contextual constraints, without contradiction? Failure means the witness contradicts something the rival must assert.
- **T2, coverage.** Once the witness is taken as established, can the rival still achieve complete coverage using only coverage options that do not conflict with it? Failure means that taking the witness as established removes coverage the rival needs: it costs a required unit, completes an approved incompatibility with witnesses the rival depends on, or breaks a necessary dependency.

The two questions are evaluated separately, so each of the four combinations of results can occur.

| T1 | T2 | Result against this rival |
|---|---|---|
| Pass | Pass | The rival accommodates the witness. Not a crux against this rival. |
| Fail | Pass | Conflict recorded. The rival can still achieve coverage without holding the witness. |
| Pass | Fail | Conflict recorded. The rival can hold the witness, but not while achieving coverage. |
| Fail | Fail | The rival can neither hold the witness nor reorganize to achieve coverage without it. The witness fails portability. |

A witness that passes membership screening and fails portability against a rival is a crux candidate against that rival.

**Certificates.** Every portability test returns exactly one of three outcomes, each with a machine-checkable certificate. *Accommodated* comes with an example arrangement. *Cannot be accommodated* comes with the specific bundle of conflicting rules. *Unknown due to search limit* is reported as unknown, together with the resource budget that produced it, and is never converted into either of the other answers. A result without a certificate is not accepted.

**Strength and ordering.** Crux strength is a discrete count: the number of rivals against which a witness is a crux candidate, together with the number of test failures recorded against each rival. Candidates are ordered by the number of rivals they defeat.

**Cost.** Let H be the number of frozen hypotheses and W_h the number of distinct witnesses appearing in at least one coverage set of hypothesis h. Each such witness is tested against every rival under both portability tests, so the number of solver tests is:

```
C = 2 × Σ over each hypothesis h of ( W_h × (H − 1) )
```

With a uniform witness count W, this is C = 2 × H × W × (H − 1). For example, H = 4 and W = 6 give C = 144 tests, whether a rival has one valid coverage set or a thousand. Cost therefore scales with witnesses times rivals, not with the number of coverage sets, because each frozen theory contains every valid set at once. Membership screening adds only lookups against stored sets. Compiling each frozen theory is a fixed cost incurred once per run, and it is the step whose fidelity, rather than its speed, is the real risk.

**Tolerance for false positives.** Multiplying the stage ratios reported in Section 5, the stages before crux identification reduce the corpus to about one percent of its original size or less. Crux identification can therefore tolerate a high false-positive rate and still be valuable: a crux stage that did no more than eliminate half of the remaining witnesses would roughly double the overall distillation. The more consequential error is losing true cruxes. Its most likely source is a frozen theory that does not faithfully capture the hypothesis from which it was compiled.

**Records and report.** For each candidate, the record stores the witness; its home hypothesis and coverage sets; every rival tested; the screening and portability results with certificates; the exact conflicting content; material uncertainty; and full lineage through the FRD and QID to the source. In certain embodiments, the core analysis ends with a report to the analyst of fewer than 4,000 words. The report states the crux candidates found, the rival each one defeats, the exact conflicting language, the reason for selection, material uncertainty or disagreement, and the pointers to witness, FRD, question, and source needed for audit. The complete machine-readable registry, the alternative coverage sets, the ACH_Eval outputs, and the validation records are linked as audit artifacts rather than included in the report. The report states that its findings are the best understanding from this corpus and this run, and that the process does not guarantee that every relevant item was extracted from the corpus. If no witness qualifies as a crux candidate against any rival, the report says so and delivers the coverage sets; cruxes are never invented in order to finish.

> See diagram depicting the traceability chain from a crux candidate to its witness, from the witness to its parent FRD and producing question, and from the parent FRD to the passage in the primary source, with a caption stating that the retained provenance allows the analyst to inspect the source behind the distinguishing evidence.

**What a crux result does not determine.** A crux result does not determine a witness's truth, its cultural or sociological authority, the independence of its source, or its dispositive legal or scientific quality. In certain embodiments, after the core analysis ends, the analyst may review conflict-recorded witnesses, meaning those that failed only one portability test against a rival, and may separately evaluate the authority and dispositive quality of individual witnesses.

**Status and alternatives.** Crux identification is the stage in which methods are least settled. The screens described above form one implemented embodiment that has been run end to end. Their practical performance has not been established, and other strategies for selecting witnesses that rivals cannot accommodate may be substituted for them or combined with them.

### 4.9 Crux-seeded search

Crux candidates tell the analyst which FRDs to retrieve first. Those FRDs, in turn, identify the passages in the sources that provide the strongest evidence for each hypothesis.

In certain embodiments, identified cruxes then seed a search of the entire corpus for further cruxes. A language model is given a hypothesis statement and the validated parent FRD of an identified crux, and is asked whether any other evidence in the corpus is at least as good at establishing support for that hypothesis. In certain embodiments, this search is performed by a model outside the quest's partition that reads the corpus directly. Because that model sees the hypothesis, its findings are treated as new candidates and pass through validation before use. In other embodiments, the search runs through the Archivist, using questions that describe the exemplar finding without the hypothesis framing, which preserves the partition. Either way, new findings enter the pipeline as new records with their own lineage.

The same procedure can estimate how much of the most valuable evidence the distillation retained. Evidence that the search finds, and that the final witness sets lack, is evidence the earlier stages missed.


## 5. The distillation cascade

Each stage of the architecture keeps less of the corpus than the stage before it, and each keeps what remains traceable to its source. The share each stage keeps is a ratio reported from runs performed to date. The cumulative shares and fold reductions are calculated by multiplying those ratios; they were not measured end to end in a single run. All figures depend on the corpus, the quality of the questions, the number of question applications, the coverage-set cap, and the hypothesis frame, and none is guaranteed.

| Stage | What remains | Share kept from previous stage (reported) | Cumulative share of the corpus (calculated) |
|---|---|---|---|
| Corpus | Source files in Markdown | Not applicable | 100% |
| 1. Quest, FRD creation, and validation | The validated FRD database | 10% to 20% | 10% to 20% |
| 2. Question-guided witness creation | The witness pool | 20% or less | 2% to 4% or less |
| 3. Coverage sets, cap of five witnesses | Witnesses belonging to at least one deletion-minimal set | About 30% | About 0.6% to 1.2% |
| 3. Coverage sets, cap of four witnesses | Witnesses belonging to at least one deletion-minimal set | About 10% to 15% | About 0.2% to 0.6% |
| 4. Crux identification (illustrative) | Crux candidates | 50% or less | About 0.3% to 0.6% at a cap of five; about 0.1% to 0.3% at a cap of four |

**Stage 1.** The query-response process followed by FRD creation and validation typically yields a validated FRD database of 10 to 20 percent of the corpus's size, a reduction of 80 to 90 percent. Metadata such as citations, locators, verdicts, and lineage makes up roughly a quarter to a third of that database.

**Stage 2.** When each validated FRD yields one witness through its producing question, the witness pool is at least 80 percent smaller than the validated FRD database. Two features account for this: the witness length ceiling, and the absence of metadata on witnesses beyond their two parent identifiers. Allocating additional question applications adds witnesses and reduces this figure accordingly.

**Stage 3.** Counting each witness once, however many coverage sets it belongs to, the witnesses that belong to at least one deletion-minimal set are about 70 percent fewer than the witness pool when sets are capped at five witnesses, and 85 to 90 percent fewer when sets are capped at four.

**Overall, before crux identification (calculated).** Multiplying the reported ratios, these stages together reduce the material requiring human evaluation to about one percent of the corpus or less, a distillation on the order of a hundredfold. The range is roughly 80 to 170 fold at a cap of five and roughly 170 to 500 fold at a cap of four.

**Stage 4 (illustrative).** Crux identification may tolerate many false positives. If its screens did no more than eliminate half of the remaining witnesses, the overall distillation would reach roughly 170 to 330 fold at a cap of five, and more at a cap of four.

**Growth during transcoding.** Transcoding lengthens the matching representation: a witness of up to 60 words may grow to up to 80, and a full hypothesis statement of roughly 100 words may grow to roughly 140. This affects the text used for matching, not the reading load of the human analyst, who can read each witness in its original form and follow its identifiers to earlier forms.

**Retention of valuable evidence.** Limited evidence from one investigation suggests that the final witness sets retain at least one-third of the most valuable information bearing on the hypotheses. That investigation evaluated whether the mechanistic basis of an approved drug supported a targeted trial in a new patient group. The estimate was made by identifying the FRDs that ACH_Eval treated as most relevant and then searching the entire corpus for insights at least as good. It is a preliminary estimate from a single investigation, and its benchmark was not independent of ACH_Eval's judgment.

**What the reductions mean for a human analyst.** Even if the final witness sets contain only one-third to one-half of the true cruxes, an analyst who reads about one percent of a corpus or less, with a traceable route from every statement back to its source, is spared most of the reading the corpus would otherwise require. Compression makes information easier to use. It does not create evidence, and it does not guarantee that nothing important was lost.

> See diagram depicting the distillation cascade as a funnel of successively narrower bands: the full corpus; the validated FRD database at roughly one-tenth to one-fifth of the corpus; the witness pool at roughly one-fiftieth to one-twenty-fifth; the witnesses belonging to deletion-minimal coverage sets at about one percent or less; and the crux candidates at a fraction of one percent. Beside each band are the stage that produces it and the adjustable settings that influence its size, such as the witness length ceilings, the number of question applications, and the coverage-set cap. An arrow from the narrowest band back to the source passages indicates that traceability is preserved throughout.


## 6. Foundations and limits

### 6.1 How the architecture is used

People use the architecture for different reasons and with different levels of rigor. Some commit the full record to a public repository and seek expert review of the results. Some run it for their own understanding of an unfamiliar field. Some bring strong prior beliefs, and some run it adversarially to test a claim they doubt. The architecture cannot enforce a standard of rigor on its operator. The operator gets out what the operator puts in. The process contains no fraud-prevention measures, its final answer remains open to interpretation, and it does not certify whether a result is gold or fool's gold, or whether it found all, most, or only some of the needles in the corpus. What the architecture fixes is the structure of the reasoning and the record of how that reasoning was carried out.

Intended users include patients and caregivers who want to read the primary research on a condition for themselves and use it to advocate for their own care, and researchers who need nuanced answers to complex questions. A patient with a rare disease is entitled to know whether a missing answer reflects a gap in a physician's knowledge or a gap in the published research. A structured, source-anchored map of the evidence helps answer that question.

General-purpose research tools tend to return general answers to general questions, and they rarely tell users that a question is underspecified. This architecture helps its user ask sharper questions of a defined corpus and see how the answers relate to the small part of the literature that actually bears on the situation. Often the architecture's most valuable product is a better question rather than a final answer.

### 6.2 Distillation needs a criterion for what must survive

Any short representation of a large corpus omits information, so its usefulness depends on which distinctions it keeps. A summary of a topic can be accurate and still omit the exception, denominator, causal condition, or conflicting observation that decides the investigation. Fewer words and more readable text do not, by themselves, make a distillation successful.

Competing hypotheses supply the criterion. They identify the distinctions that matter: what would favor one explanation over another, what would invalidate a necessary premise, what would expose an omitted explanation, and what would establish that the record cannot yet decide. A question translates such a distinction into a request the corpus can answer. In this architecture, signal means relevance to the ACH frame, and noise means irrelevance to it. A compressed representation can be faithful relative to the hypotheses under evaluation even when it discards nuance that does not bear on them. The hard part is deciding what bears on them, and the question records that decision. The test of any distilled representation is whether it keeps what its intended use requires: conditions, attribution, adverse findings, uncertainty, and the limits of each source's contribution.

### 6.3 Competitive abduction

Deduction reasons from a general rule to a specific case and guarantees its conclusion if the premises are true, but it cannot reach beyond what the premises contain. Induction reasons from observed cases to a general rule; it reaches further, but a counterexample can defeat it. Abduction reasons from an observation to a candidate explanation. If a lawn is wet, rain is one explanation and a sprinkler is another. Abduction proves nothing. It proposes explanations that further evidence can support, refine, or refute.

The architecture is built on abduction, because abduction generates explanations worth testing. A coverage set is an abductive construction: witnesses that together cover a hypothesis that none of them establishes alone. The architecture practices competitive abduction, comparing several explanations against the same evidence. The relevant question is not merely whether evidence can be made consistent with a hypothesis, but which hypothesis would have predicted the evidence most strongly. Evidence compatible with every hypothesis distinguishes none of them. Crux candidates are the places where the hypotheses genuinely diverge.

The architecture does not make abduction certain. It makes abduction disciplined, and it makes each abductive step inspectable.

### 6.4 Lovely versus likely explanations

Peter Lipton distinguished between lovely explanations, which are elegant, coherent, and satisfying, and likely explanations, which are probably true given the evidence. Language models are trained on human writing and tuned to produce text people find compelling, which pulls them toward loveliness. They can produce a narrative that hangs together even when the evidence does not support it.

The architecture keeps loveliness away from the steps that establish what the evidence says:

- The Archivist cannot tailor its answers to a story it cannot see.
- The validator answers a narrow question: does the named source support this FRD?
- The fidelity audit asks what a witness asserts beyond, or omits from, its validated parent.
- The matcher is qualified on meaning rather than on wording.
- Crux results carry certificates that can be checked.

Explanatory virtues such as scope and elegance may legitimately influence how an analyst frames hypotheses. They cannot change what a source says.

### 6.5 What a fork can and cannot change

Different analysts may legitimately frame the same question differently. They can define the hypotheses differently, choose a different material objection, make the residual hypothesis broader or narrower, or assemble a different corpus. A fork that changes the frame changes the starting framing of the investigation. A fork that adds or removes sources changes the evidence. Both are legitimate when disclosed.

What a fork cannot change is what a source says. A passage exists or it does not. An FRD matches its passage or it does not. A quotation is in context or it is not. These questions can be checked again by anyone with the source. Interpretation still enters when judging how strongly a passage bears on a hypothesis, so re-checkability does not make every judgment objective. It does make source fidelity contestable on shared, inspectable ground.

### 6.6 The residual hypothesis and the bad-lot problem

Inference to the best explanation faces the bad-lot objection: the best explanation among those considered may still be wrong, because the true explanation may be missing from the list. The architecture answers this objection in two ways.

The internal answer is the residual hypothesis. It formally acknowledges that the current frame may be inadequate: the evidence may be insufficient or conflicting, the domains may not meaningfully connect, or no single explanation may dominate. The residual hypothesis remains live throughout the run. ACH_Eval reassesses the full allocation at every checkpoint, and the residual hypothesis is written out and compiled like the others. Allocations are not credences; a hypothesis that currently receives few units remains in the frame and can regain weight when the evidence warrants.

The external answer is forking. An investigator who believes the true explanation is missing can fork the run, add or revise hypotheses, run it again, and publish the difference. Forking does not guarantee that the true explanation will be found, but it makes omissions visible, contestable, and correctable.

### 6.7 Stopping as a judgment about cost

A quest does not end because a hypothesis has been proven. It ends because further questioning is expected to add too little to justify its cost. This is not permission to stop early because the results favor a preferred hypothesis. Stopping follows adverse testing, a search for the ways each hypothesis could fail, and continued attention to the residual hypothesis. The honest statement at the end of a quest is: further questioning is unlikely to change the assessment enough to justify its cost, unless a fork changes the frame, the corpus, or the validation record.

### 6.8 Structured cross-checking

The objection that language models hallucinate is serious, and it is the reason the architecture has the shape it does. The architecture does not assume that language models are reliable. It assumes that they can hallucinate, overfit to framing, prefer lovely explanations, omit sources, and ask biased questions, and it places a specific constraint against each failure:

- partitioned roles, with separation enforced by the data path;
- a frozen header and frozen hypotheses;
- one-claim, one-source FRDs, each with one producing question;
- validation against the named source, kept blind in certain embodiments;
- two-direction fidelity audits of witnesses;
- a conformance gate for transcoded text;
- qualification of the matcher against adversarial pairs;
- certificates for crux results;
- reproducibility records;
- coverage review; and
- forks.

The narrower objections that remain map to specific points of audit:

- An incomplete corpus is addressed by coverage review.
- A badly framed header is addressed by forks.
- An overstatement missed in validation is addressed by the fidelity and source-assignment audits.
- A false similarity found by the matcher is addressed by qualification and by ABSTAIN.
- Coverage that looks complete but is not is addressed by the distinction between exhaustive and resource-bounded search.

An inspectable criticism of a particular run is always available, which is the practical difference between a general complaint about unreliable models and a checkable claim about this process.

### 6.9 Records, audit, and forking

**Artifact registry.** In certain embodiments, everything produced after FRD creation receives an immutable identifier, a content hash, and links to what it depends on, so that a change regenerates exactly what it should. The lineage chain runs from the run to the QID, the response, the candidate FRD, the validated FRD, the question application, the witness, the transcoded witness, the coverage set, and the crux result. Each run creates its own records, and records from different runs are never merged into one identity.

**Reproducibility records.** In certain embodiments, each model step and human decision is recorded with the provider, model version, endpoint, and time; the full prompts and their hashes; settings, seeds, and tools; every attempt and retry, with raw and parsed outputs; and the output actually released, together with the predeclared rule that selected it. Platform information that is unavailable is marked unavailable. When several valid outputs compete, they are preserved as a disagreement.

**The record as audit trail.** A reader evaluating a run can read the question records, the Archivist's responses, the FRD creation record, and the validation record. Together they show how each question was formed, what the Archivist returned, how each return became an FRD, and whether that FRD survived validation. This chain shows that the corpus was actually used to produce the analysis, not merely possessed by the analyst. The principal integrity risk is undisclosed iteration: deciding after seeing a result that the evidence is weak and quietly gathering more until the result changes. Gathering more evidence is legitimate when the process, the intermediate results, and the motivation are disclosed. In certain embodiments, the records carry enough metadata that an audit surfaces the discrepancies manipulation would create.

**Publication.** In certain embodiments, a published run includes:

- the report to the analyst;
- the shareable corpus, the manifest, and instructions for rebuilding the retrieval database;
- the index, the header, the written hypotheses, and their coverage representation;
- the question database and the query-response records;
- the FRDs with their producing QIDs, and the validation records;
- the question applications and the witnesses in raw and transcoded form;
- the dictionary, canonicalizer, and transcoder;
- the matching records, the coverage sets, and the crux results; and
- the sequence of ACH_Eval outputs.

Sources that cannot legally be shared are listed by full citation and description, and unavailable settings are marked as unavailable rather than silently omitted.

**Forking.** In certain embodiments, a fork clones a published run, declares its source additions, hypothesis revisions, and prompt changes, reruns only the steps those changes affect, and refers to the parent run for everything else. It publishes the difference and whether the conclusion moved. Because converted sources and most index entries can be reused, setting up a fork is intended to take less than an hour of effort. Disagreement is demonstrated by running again, not by appending criticism. A motivated fork can still run, but it cannot hide what it changed. A reader who studies how questions were asked and answers weighed across a run and its forks can also learn to reason about evidence by example.

### 6.10 A conceptual objective for question selection

The following expression describes what question selection aims at. It is a conceptual statement, not an execution rule or an estimator.

Let K_t be the evidence record after round t, q a feasible next question, Z_q the eventual source-checked contribution of its answer (or a documented limitation), V the quality of the record for the investigation, and c(q) the cost of asking, answering, and checking q. Then:

```
U_t(q) = E[ V(K_t updated with Z_q) − V(K_t) | K_t, q ] − c(q)
```

The objective prefers useful, checked progress relative to cost. V must not be defined circularly as whatever makes a preferred answer more confident; source accuracy, material coverage, dependence among sources, and applicability all bear on it, and corrections must not be relabeled as new discoveries.

In certain embodiments, the realized change is measured as the change in ACH_Eval's allocation between successive checkpoints. The Coordinator approximates the expectation by steering the Investigator toward topics whose recent questions produced substantial change and away from topics that produced only trivial change. Under an explicit probabilistic model of hypotheses and possible observations, expected information gain is one possible choice of utility. ACH_Eval's allocation changes are not computed as that quantity.

For the second distillation pass, the corresponding design target is the shortest practical witness that preserves what the validated FRD allows one to say in answer to the question, including its material limits.

### 6.11 Evaluating the mechanisms

The architecture's mechanisms are intended to be tested separately, under matched conditions, so that an apparent improvement can be attributed to the mechanism responsible rather than to a stronger model, a better index, more computation, or more human intervention.

| Mechanism | Controlled comparison | Result that would support the mechanism |
|---|---|---|
| The Investigator's lack of direct access to sources | Same frame, index, models, feedback, and task; vary direct access to sources | Better independently checked diagnostic yield, or fewer errors, at comparable total cost |
| The Archivist's lack of access to the frame | Same questions and corpus; vary whether the full frame is supplied | Fewer source distortions favoring the exposed frame, without unacceptable loss of relevant evidence |
| Adaptive feedback from the Coordinator | Adaptive questions versus a fixed schedule of questions | More distinct consequential findings, better adverse coverage, or fewer wasted questions within matched budgets |
| Compression by the producing question | Same validated FRDs; the producing question versus generic summarization versus a newly optimized question | Fewer material omissions at matched length, without more unsupported assertions |
| Feedback that rewards evidential quality | Feedback on evidence quality versus feedback that rewards support for one hypothesis or score movement | Better source-checked evidence and corrections, including findings against the desired outcome |
| The allocation gauge | Same corpus and questions; vary the gauge | Differences in stopping point and in the size of registered changes, with comparable final rankings |

In certain embodiments, the evaluation also measures:

- the completeness of the question database and the separation of question records;
- conformance to the one-producing-QID rule and lineage accuracy;
- validation fidelity and witness compression fidelity;
- stability of dictionary senses, binding accuracy, and preservation of protected properties;
- the accuracy of text-only matching;
- the validity and enumeration status of coverage sets;
- the reproducibility and exclusion accuracy of crux results; and
- agreement between the strongest crux candidates and the conclusions of human experts who can read all of the quest's questions and answers.

Evaluations use repeated runs; conceal method labels from reviewers where feasible; record retrieval and validation costs; include important facts the system never surfaced, not only the precision of what it chose; keep measured counts separate from model-judged labels; and localize each failure to the step responsible. Unknown results are reported as unknown. ACH_Eval allocations and crux results answer different questions, and the accuracy of one is never claimed on the basis of the other. A comparison can show that a component helped on the tasks tested; it cannot establish a universal optimum.

### 6.12 What the architecture is and is not

The architecture is a constrained, competitive, multi-hypothesis process for distilling, comparing, and auditing evidence. It separates the formulation of questions from the retrieval of evidence, so that coherent narratives do not contaminate reports of what sources say. It keeps a residual hypothesis live to acknowledge uncertainty and the possibility that the frame is incomplete. It lets adversarial investigators expand the frame, and expose their disagreements, by forking.

The following principles govern its use:

- Conclusions are the best understanding available from this corpus and this run, never settled facts.
- Authority is a cultural and sociological status that exists outside ACH. The analysis is blind to authority; a human analyst may evaluate authority after the core analysis.
- No count and no source prestige acts as a silent tiebreaker.
- "No conflict found" does not mean "proven compatible."
- Supporting and adverse evidence receive identical treatment and identical visibility.
- A material change creates a new version, and earlier artifacts remain inspectable.

Until human-only, model-only, and combined use have been compared on the same task and corpus, the architecture's demonstrated contributions are capability, traceability, compression, and auditability, not improved judgment or accuracy.

The architecture is not a truth machine. It is not a substitute for experiments, judicial decisions, clinical expertise, legal judgment, or policy choice. It does not resolve disagreements about values, it does not guarantee completeness, and it does not promise that any hypothesis is correct. Its value is narrower and stronger. It gives an investigator a disciplined way to ask precise, consequential questions of a large corpus, to distill the answers into a small set of traceable crux candidates, to test those candidates against their sources and their rivals, and to state honestly when the result is support, objection, a gap, a mismatch, or unresolved uncertainty.


## 7. Glossary

### 7.1 Roles and the run

**Archivist.** The role that holds the corpus and answers one source-grounded question at a time, with attribution. It never receives the ACH frame, the index, hypothesis labels, allocations, ranks, or the research state. In certain embodiments, it is implemented with a retrieval-augmented service such as NotebookLM.

**Investigator.** The role that uses the header, the index, saved answers, and the Coordinator's feedback to write and submit questions and to capture each exchange exactly. It has no direct access to the corpus. In certain embodiments, it is score-free.

**Coordinator.** The role that runs ACH_Eval at checkpoints, gives the Investigator qualitative feedback on where novelty has and has not been found, and decides when the quest stops.

**Validator.** The role that checks a candidate FRD against the source file it names. In certain embodiments, it works without any knowledge of the hypotheses.

**Intake tool.** In certain embodiments, a tool used only before the header is frozen, to help organize materials, specify searches for sources, and draft hypotheses.

**Run.** One complete pass through the architecture after the corpus, index, and header are prepared: the quest, FRD creation and validation, the language tools, witness creation, transcoding, coverage sets, and crux identification.

**Quest.** The multi-round exchange of questions and answers between the Investigator and the Archivist, directed by the Coordinator.

**Round.** One question and its answer.

**Checkpoint.** A point in the quest at which the Coordinator runs ACH_Eval and gives feedback; in certain embodiments, every five to six rounds.

### 7.2 Sources and preparation

**Source.** An underlying document or record, not a model's summary of it.

**Source file.** The Markdown conversion of a source, with a stable identifier. It is what the retrieval database ingests and what validators read.

**Corpus.** All admitted source files for a run.

**Manifest.** The list of source files with their identifiers, provenance, and shareability, together with sources that could not be obtained.

**Eligibility.** Whether a source is primary relative to the investigation. Eligibility depends on the question, not on the type of document.

**Retrieval database.** The database through which the Archivist answers questions. It is disposable and can be rebuilt from the committed files.

**Ranked index.** A catalogue of every source file, with summaries, relevance notes, and ranks. It is the Investigator's map and is never evidence.

**Discovery Quest Header (header).** The investigation's frozen instruction set, containing the ACH frame. It is the Investigator's compass.

**Freeze.** The act of fixing the header, hypotheses, coverage representation, index, manifest, database identity, prompts, and configuration before the quest. Later material changes create new versions.

### 7.3 Hypotheses and assessment

**ACH frame.** The set of competing hypotheses, organized into one or more axes, that governs an investigation.

**Axis.** One material question within the ACH frame, with its own hypotheses and its own allocation. Allocations on different axes are never multiplied together.

**Hypothesis; full hypothesis statement.** A human-approved, ordinary-language statement of an explanation, written in certain embodiments with a concise statement, assumptions and antecedent conditions, potential falsification context, and potential corroboration context.

**Residual hypothesis.** The hypothesis on each axis that holds the outcome in which neither substantive hypothesis is cleanly supported. In certain embodiments, it states that the evidence is insufficient; in others, it states that no single explanation dominates.

**Rival hypothesis.** Any other hypothesis in the same frozen frame.

**ACH_Eval.** The Coordinator's assessment prompt: a structured estimator that maintains a cumulative evidence record and allocates units among hypotheses. The quality of its output is estimated from its resolution bound, the audited quality of its rules, the capability of the model running it, agreement across gauges and models, and scored forecasts.

**Allocation.** The integer units ACH_Eval assigns to the hypotheses of an axis. An allocation is a structured judgment of what the record warrants, with a resolution of 100/G percentage points, not a probability of truth.

**Allocation gauge (G).** The number of integer units allocated per axis. Each unit represents 100/G percent. The gauge sets how large a change must be before it registers.

**Novelty.** The decision-relevant change a batch of answers makes to the evidence record. Its working indicator is the change between successive ACH_Eval outputs.

**Reconstruction tier.** In the Archivist-only edition of ACH_Eval, a record of how many separate answers concordantly report the same finding. It awards no points.

**Private quest state.** The Investigator's working record of the investigation, as defined by the header. It is never sent to the Archivist and is not evidence by itself.

### 7.4 Questions and facts

**QID.** The unique, permanent identifier of one issued question.

**Question database.** The run's durable record of every issued question. Records are never merged.

**Query-response record.** The exact question, named sources, header version, and exact answer of one round.

**FRD (Facts and References Database) entry.** A statement of one claim anchored to one source, with a locator and exactly one producing QID.

**Candidate FRD; validated FRD.** An FRD before and after validation against its named source. A validated FRD may be confirmed, repaired, or split.

**Validation packet.** One candidate FRD together with the source file it names, without hypotheses or intended use.

**Lineage tags.** Labels recording whether a claim rests on the source's own result (OWN_RESULT), on an identified earlier source (DERIVED_FROM), or on an unidentified earlier source (DERIVATIVE_UNKNOWN).

**Source-assignment labels.** Labels applied after validation: BETTER_SOURCE_AVAILABLE, REDUNDANT_WITH, and INTRA_SOURCE_TENSION.

**Coverage review.** The separate check that cited sources were captured and that the central sources of each domain are present and cited.

**Hub.** A source that related-work services return for many of a domain's most-cited sources, and that is therefore central to the domain.

### 7.5 Witnesses and language tools

**Witness.** A concise answer to a question, drawn from one validated FRD, with exactly one parent QID and exactly one parent FRD.

**Question application.** The record of one question applied to one validated FRD, which yields exactly one witness.

**Lens.** The question used to produce a witness: the producing question by default, and, in certain embodiments, a cluster-best question, a nearest-neighbor question, or a question rewritten by question transcoding.

**Fidelity audit.** The two-direction check of a witness against its parent FRD and question, looking for unsupported assertions and material omissions.

**Custom dictionary.** The run-specific collection of reviewed contextual senses of recurring terms in validated FRDs.

**Occurrence.** One use of a word in one validated-FRD sentence, with enough surrounding text to understand it.

**Contextual sense.** The meaning a word has in a particular group of occurrences. One written word may have several.

**Sense group.** Occurrences judged to use a word in the same sense. Each approved group yields one `WORD (modifier)` entry.

**Base word form.** The form under which grammatical variants of a word are counted together.

**Reference English corpus.** A versioned collection of ordinary English, used only to estimate how common a word normally is. It is not evidence.

**Relative frequency.** A word's rate in the validated FRDs divided by its rate in the reference English corpus. It is used only to prioritize review.

**Dictionary binding.** The recorded decision that a particular occurrence in a witness or hypothesis uses a particular dictionary entry. If the context does not settle this safely, the binding remains unresolved.

**Scoped alias.** An approved alternative wording for a dictionary entry, usable only within its recorded scope.

**Canonicalizer.** The rule set and language map, built from the dictionary and from sentences in validated FRDs, that defines the run's controlled grammar profile.

**Controlled grammar profile.** The versioned house-style rules stating which grammatical constructions are preferred, which are rejected, and which require review.

**Canonical form.** The one preferred word form or construction chosen for consistent use. Choosing a canonical form standardizes expression; it does not declare a claim true.

**Protected property.** A part of meaning that canonicalization and transcoding may never change: attribution, polarity, modality, conditions, alternatives, identity, role, time, quantity, scope, and referent.

**Transcoder.** The executable English-to-English process, compiled from the dictionary and the grammar profile, that is applied to witnesses and full hypothesis statements.

**Transcoding.** Applying the transcoder to produce controlled-English text. In this architecture, the term refers to this dictionary-based rewrite; question transcoding (Section 4.1) is a separately named optional variant.

**Normalization preview.** A side-by-side display of original and transcoded text that identifies every substitution and grammatical change.

**Conformance.** Compliance of an artifact with its frozen dictionary and grammar rules while preserving every protected property. Conformance is not proof that the text is true.

**Conformance gate.** The check that withholds from matching any artifact with an unresolved binding, an unapproved exception, an unexplained change to a protected property, or a missing trace.

### 7.6 Matching, coverage, and cruxes

**Coverage unit.** An internal matching representation derived from an approved hypothesis. The four kinds are REQUIRED_SUPPORT, CONTEXTUAL_CONSTRAINT, ADVERSE_TEST, and CORROBORATING_EXPECTATION.

**Semantic matching.** Comparison of meaning, rather than spelling alone, between transcoded witness text and transcoded hypothesis text.

**Match relations.** EQUIVALENT, WITNESS_ENTAILS_UNIT, UNIT_ENTAILS_WITNESS, PARTIALLY_COVERS, CONTRADICTS, NO_SEMANTIC_RELATION, and ABSTAIN.

**Match trace.** A short explanation naming the words, structures, and protected properties that justify a relation.

**Jointly sufficient group.** Two or more partial matches that together completely cover a unit that none covers alone. The members remain separate witnesses.

**Adversarial test pair.** A deliberately difficult pair of statements in which the wording stays similar while one feature that carries meaning changes.

**Matcher qualification.** Testing a matcher version against adversarial test pairs, with results reported for each pattern, before it may create coverage options.

**Coverage option.** A single witness, or an approved jointly sufficient group, that completely covers one required unit.

**Complete coverage.** Every REQUIRED_SUPPORT unit represented and every CONTEXTUAL_CONSTRAINT satisfied, with adverse-test and corroborating-expectation results kept visible.

**Deletion-minimal hypothesis coverage set.** A set of witnesses with complete coverage and no approved incompatibility, from which no witness can be removed without losing coverage or breaking a necessary dependency. It is not necessarily the smallest set, the only valid set, or the strongest set.

**Removal certificate.** The recorded reason a witness cannot be removed from a coverage set.

**Approved incompatibility.** A recorded combination of witnesses that cannot coherently appear in one coverage set.

**Necessary dependency.** A recorded relationship in which one witness's contribution requires another witness.

**Coverage-set size cap.** In certain embodiments, the maximum number of witnesses allowed in a coverage set. A tighter cap gives more compression and a greater risk of losing crux statements. A hypothesis that exceeds the cap is reported as exceeding it, not as uncovered.

**Exhaustive search; resource-bounded search.** A search that checked every combination of coverage options under the frozen inputs, versus one stopped by a declared limit, after which further sets may exist.

**NO_COMPLETE_COVERAGE.** The result when at least one required unit has no coverage option.

**Home hypothesis.** The hypothesis whose coverage sets a witness belongs to.

**Membership screening.** A check of whether a witness appears in any deletion-minimal coverage set of a rival hypothesis. It is inexpensive and yields many false positives.

**Frozen rival theory.** A machine-readable, versioned compilation of a hypothesis's coverage requirements, constraints, dependencies, and incompatibilities. It implicitly contains every valid coverage set of that hypothesis.

**Portability test.** A pair of solver queries against a frozen rival theory: T1 (can the witness be held together with what the rival asserts, without contradiction?) and T2 (once the witness is taken as established, can the rival still achieve complete coverage?).

**Certificate.** A machine-checkable record of why a test result holds: an example arrangement, a conflicting rule bundle, or a declared search limit.

**Crux candidate.** A witness that belongs to its home hypothesis's coverage but that a rival hypothesis cannot accommodate. In certain embodiments, such a witness passes membership screening against the rival and fails both portability tests against it.

**Crux strength.** The discrete count of rivals against which a witness is a crux candidate, together with its recorded test failures.

**Conflict-recorded witness.** A witness that fails only one portability test against a rival.

**False-crux error.** Treating a witness as a crux because it conflicts with the rival coverage sets formed so far, when a valid rival set not yet formed would accommodate it.

**Crux-seeded search.** A search of the corpus for evidence at least as strong as that behind an identified crux, given the hypothesis and the crux's parent FRD.

### 7.7 Status labels

**ABSTAIN.** The system declines a judgment the text or rules cannot support reliably. It is an honest unresolved result.

**REQUIRES_REVIEW.** An automated step found a specific ambiguity or rule failure that a human must resolve before work continues.

**APPROVED_EXCEPTION.** A human-approved, recorded departure from the grammar profile, with its reason and scope.

**PASS, REVISE_WITNESS, REPAIR_FRD, HUMAN_REVIEW.** The outcomes of a witness fidelity audit.

### 7.8 Records

**Artifact registry.** The record of immutable identifiers, hashes, and dependency links for artifacts produced after FRD creation.

**Reproducibility record.** The record of a model step or human decision: provider, model version, prompts and their hashes, settings, attempts, outputs, and the rule that selected the released output.

**Fork.** A declared copy of a published run with changed sources, hypotheses, or prompts, rerun where affected and published with its difference from the parent run.
