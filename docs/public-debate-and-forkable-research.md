# 07 — ACH 2.0: Public Debate and Forkable Research Supplement

## 1. Scope and relationship to the specification

This supplement describes the public use of the architecture disclosed in *01 Claim_Registry_ACH_2.0_Architecture_and_Rationale* and *02 ACH_2_Short_Specification*. It assumes both documents, together with the header generator (*03*), the Archivist prompt generator (*04*), and the FRD generation and validation prompt generators (*08* and *09*, version 3.1). Nothing in those documents is restated here. Where this supplement depends on a provision of the specification, it cites that provision by document and section.

The supplement extends three parts of the specification: the records, audit, and forking discussion in *01* §6.9; the publication and forking modules in *02* §§34 and 34.1; and the publication artifacts and question-record provisions in *02* §§8 and 20. It adds six things:

1. a fork record, with defined contribution routes and completion states;
2. the complete validated FRD, as produced under *09*, as the default unit of evidence shared between a parent run and its forks;
3. a procedure for determining which stages of a fork must be rerun and which may be inherited;
4. a comparison discipline stating which comparisons between runs the records support;
5. a public argument document that presents a run's claims and a fork's counterargument in one structure; and
6. publication practices for runs whose sources cannot all be redistributed.

The supplement does not alter core termination (*02* §30), the blinding boundaries (*02* §§18–19), witness identity and non-merger (*02* §28.2), semantic matching (*02* §28), or crux qualification (*02* §29.1). A fork is a run under the specification. The supplement governs how such a run relates to the run it derives from and how its results are presented for public scrutiny. Where the supplement and the specification appear to conflict, the specification governs and the conflict is noted in §7 as a clarification for the specification writer.

Throughout, "in certain embodiments" marks optional features. No numerical limit stated in this supplement is essential unless identified as a configured parameter of the run.

## 2. Terms introduced by this supplement

**Parent release.** A fixed, versioned publication of a run under *02* §34, identified by run ID and version, from which a fork derives.

**Fork.** A run that derives from a parent release by inheriting some of its artifacts and declaring changes to others. A fork has its own run ID; it is not a continuation of the parent under *02* §32.

**Fork record.** The artifact that binds a fork to its parent: parent identity, declared changes, inherited artifacts, stage accounting, completion state, and links to the fork's public argument.

**Challenge.** A public contribution that disputes a specific FRD, proposition, or conclusion of a release, states a correction or objection with a checkable basis, and asserts a consequence, without rerunning any stage.

**Counter-investigation.** A fork in which at least one analytical stage has been rerun and every stage has been accounted for as rerun, inherited, pending, or not applicable.

**Completed ACH 2.0 counter-run.** A counter-investigation in which every applicable core stage through crux identification and the analyst-facing report (*02* §§10–30.1) has been rerun or legitimately inherited with unchanged dependencies.

**Stage accounting.** The fork record's per-stage statement of one of four states — rerun, inherited by reference, pending, or not applicable — with the artifact and reason.

**Inherited record.** A complete validated FRD, as produced under *09*, carried from a parent release into a fork without alteration.

**Adoption entry.** The fork's record that a particular inherited record, identified by originating run, FRD ID, and version or content hash, is in use by the fork.

**Inherited question record.** An entry in a fork's question database holding a parent's producing question, marked as not issued in the fork's quest, retained so that the inherited FRD's required origin witness can be constructed under *02* §24.

**Reuse caution.** A validator-authored statement, recorded during validation, that constrains how an FRD may be used downstream — for example, that a source-local identification is not to be generalized to other occurrences of the same term.

**Correspondence record.** A record linking two independently created FRDs, from different runs, that concern the same source passage or the same disputed proposition, stating the assessed relationship between them without merging their identities.

**Public argument.** The document, described in §5, in which a run's author or a fork's author states a position, its evidence, its adverse findings, and its open disagreement, with links to the underlying records.

**Source-access record.** The publication artifact, described in §6, stating for each source whether its text is available to a reader, what was inspected during validation, and what a reader can and cannot independently check.

## 3. Public purpose and rationale

### 3.1 The problem addressed

Public disagreement on contested questions is commonly conducted through labels applied to participants rather than through examination of evidence. A person who disputes an accepted account is characterized rather than answered; a person who defends it is likewise characterized. Neither characterization identifies a source, a passage, an inference, or an omission. The architecture disclosed in *01* and *02* produces exactly those objects: a corpus, a set of questions, a database of source-validated claims, competing hypotheses, and a traceable path from each conclusion to the passages that support it. This supplement describes how those objects are used to make a public case, how a person who disagrees builds a counter-case from the same objects, and how the two cases are compared.

The intended participants include patients and caregivers, independent researchers, advocates, skeptics, litigants, and anyone with a position to defend or attack. Credentials, publication history, and declarations of neutrality are not conditions of participation. A participant may be motivated. The architecture is designed on the premise that the Investigator is motivated (*01* §2.2), and the public layer inherits that premise: what is required is not neutrality but a record that makes the participant's question, source choices, adverse findings, and inferences examinable by others.

### 3.2 The form of a public case

Under this supplement, a public case identifies what a source reports, what the participant infers from it, the conditions and limits that attach to the inference, and why the inference bears on a competing explanation. A reply identifies the exact premise, quotation, interpretation, comparison, or inference being disputed and gives its reason and evidence. Person-labels, prestige, popularity, and declarations of certainty are treated as insufficient to resolve an evidential question. Vigorous advocacy is compatible with accurate quotation, retained qualifications, and serious treatment of alternatives. A bounded claim of error or insufficiency is a valid contribution even when the critic offers no replacement explanation.

Conventional and unconventional accounts face the same requirements. A source-fidelity failure is a failure whichever side commits it. A hypothesis is not disqualified by its author's reputation, and it is not credited by it.

### 3.3 Relationship to existing public arbitration

Collaborative annotation systems such as Community Notes publish their scoring code and make their notes and ratings available for download. Such systems settle claims that can be resolved by a link or a short note. The contribution proposed here is different in kind rather than in degree: an inspectable investigation containing the selected corpus, the questions actually asked, the claims that survived validation against their sources, the competing explanations, and a route for rerunning affected work. The design claim concerns that fuller research record. It does not depend on characterizing existing systems as opaque or as incapable of handling complex claims.

### 3.4 Settings that benefit from an inventory

A person reasoning alone, a court, a peer reviewer, an arbitrator, and a reader relying on a trusted authority each determine whether a claimed relationship holds. Each setting retains its own standard of judgment. Each works better with a clear inventory of the claims at stake: the operative facts and authorities for a court; the positive and negative evidence for a reviewer; the mechanisms, population match, and uncertainty for a clinician; the rules, comparators, and prior statements for a policy reviewer; the specific claims that matter most for a patient, client, or affected user. The public argument of §5 is that inventory, presented so that a reader at any of these settings can find the source behind a consequential claim.

### 3.5 Stated ambition

Increased civility, participation, and well-founded agreement are design goals to be evaluated, not effects the architecture guarantees. A correction, a better question, a narrowed claim, and a precisely located disagreement are useful outcomes. Consensus is a possible outcome, not a condition of publication.

## 4. Module 1 — Public forking and cumulative disagreement

**Inputs.** A parent release; the research records available from it under *02* §34; and a participant's identified disagreement.

**Output.** One fork record, as defined in §2, together with the fork's own run artifacts and a public argument under §5. A challenge, which produces no fork record, is also a valid output of this module.

### 4.1 Contribution routes and completion states

Three routes are provided. They differ in the work performed and in what the result establishes.

| Route | Minimum contribution | What it establishes |
|---|---|---|
| Challenge | The disputed FRD, proposition, or conclusion, identified by ID and version; the correction or objection; a supporting passage or otherwise checkable reason; the asserted consequence | A specific objection, available for review, without any rerun |
| Counter-investigation | A fork record with declared changes, the outputs of every rerun stage, and stage accounting for every stage | Results obtained from the completed work under the declared conditions |
| Completed ACH 2.0 counter-run | A counter-investigation in which every applicable core stage through crux identification and the analyst-facing report is rerun or legitimately inherited | A full result under the specification, including disclosed unknowns and a valid no-crux outcome where that is what the work produced |

A counter-investigation is labeled **partial** until all applicable core work is complete or legitimately inherited with dependencies unchanged. Recipe 1 outputs alone (*02* §§10–15) support a partial contribution. A copied repository, a rewritten public argument, or a set of objections without a rerun is not a counter-run; it may be a challenge.

These are completion descriptions, not ranks. A valid local correction survives an incomplete broader investigation, and the value of a challenge does not depend on whether its author later performs a counter-run. In practice, challenges and partial counter-investigations are expected to be the majority of public contributions. The completed counter-run is the standard for claiming a full result under the specification; it is not the threshold for a contribution to deserve consideration.

### 4.2 The complete validated FRD as the shared evidence unit

The unit of evidence carried between a parent and a fork is the complete validated FRD as delivered under *09*: the original FRD identity with its origin reference and one producing QID; the citation, source identity, locator, and any noted missing metadata; the corrected, supported claim, with the original candidate preserved where materially changed; the exact supporting or contradicting source text with its necessary context, labels, and units; the verdict on the original candidate with its explanation and material repairs; the confirmed or corrected provenance tag; the readiness flag; and any unresolved material defects. Where the validating process recorded reuse cautions, literal-search results, or a clause-to-source map, those form part of the unit.

Two properties of that unit govern its inheritance.

**Verdict and readiness are separate.** The verdict evaluates the original candidate; readiness evaluates the repaired FRD. A candidate judged WRONG can yield a repaired FRD marked READY FOR WITNESS CONSTRUCTION, and a candidate judged RIGHT is not thereby ready. A record marked NOT READY remains available for audit and does not enter witness construction in a fork by relabeling. A fork that wishes to use such a record must repair it under *09* and record the repair as a successor.

**Completeness has a scope.** The record establishes what its named source supports and how that was checked. It does not certify that the source is authentic, that the source is reliable, that the claim is independent of other claims, that the claim applies to the fork's question, or that retrieval was exhaustive. Where the source is a transmitter, the record establishes what the transmitter reports, not what the transmitted authority said.

**Inheritance.** In certain embodiments, a fork adopts an inherited record by an adoption entry identifying the originating run, the FRD ID, and the fixed version or content hash of the record. The adoption entry does not mint a producing QID, does not imply a further validation, and does not merge the record with any FRD created in the fork. The record is carried by reference. A copy may be included in the fork's publication for reader convenience where redistribution is permitted, but the reference to the parent's fixed version remains the identity of the record. Because a single validated record can run to tens of kilobytes of reproduced source text, reference is the default mode, and a displayed claim in the public argument links to the complete record rather than reproducing it.

**Reuse cautions travel.** A reuse caution recorded by the validator is an inherited constraint. A fork that adopts the record adopts the caution, and a public argument that uses the record in a way the caution forbids — for example, generalizing a source-local identification to every occurrence of a term — is a source-fidelity defect under §4.6 whether or not the record's claim was quoted accurately. A caution may itself be wrong or overbroad. A fork contests it openly by recording a linked alternative validation or a documented alternative reading as a successor or alternative record, with reasons; the defect is contravening a caution silently, not disputing it on the record.

**Inherited records carry the parent's frame.** A changed header does not by itself invalidate prior source-fidelity validation; the record's verdict and readiness concern the relationship between a claim and its source, which the fork's hypotheses do not alter. Revalidation is warranted by a specific defect, a changed source basis, or a challenge to the claim. However, the parent's FRD set is not a neutral inventory of the corpus. Each FRD descends from a question selected under the parent's header to discriminate the parent's hypotheses (*01* §§2.3, 6.2). Responses to those questions may contain incidental findings and qualifications that the parent did not seek, but the parent's question selection shaped what was retrieved, and the inherited set may omit material important to the fork's question. A fork with a changed frame therefore treats inherited records as a starting set, not as the corpus's answer to the fork's question. Such a fork may publish a partial counter-investigation on inherited records alone, provided its stage accounting discloses that quest work and coverage review under its own frame are pending. It cannot claim a completed counter-run until it has conducted its own quest under its own header and its own coverage review under *01* §3.3.

**Exclusions, successors, and alternatives.** A fork declares every parent record it does not adopt, with a reason. Excluded records, including adverse findings, remain visible in the comparison history. A repair, split, substantive revision, or competing validation of an inherited record creates a linked successor or alternative record; the earlier version is preserved. Split children retain the producing QID of the parent record (*02* §19.1). Source ancestry recorded in the provenance tag (DERIVED_FROM and its relatives) describes the evidential lineage of the claim and is kept distinct from fork history, which describes the lineage of the record.

**Correspondence records.** Ordinary inheritance requires no matching of records across runs: the adoption entry identifies the exact record. Where a fork independently creates an FRD from the same source passage as a parent record — as a header-changing fork will, having quested anew — the two records remain distinct. In certain embodiments, a correspondence record links them and states the assessed relationship as one of: the same passage and substantially the same claim; the same passage with a corrected or competing reading; different passages bearing on the same disputed proposition; or a new claim with no identified counterpart. Equivalence is assessed and recorded, never assumed from shared filename and locator. Different source conversions can alter filenames and locators, and two investigators can extract different claims from one passage; the correspondence record exists to expose those differences, not to dissolve them.

### 4.3 The counter-investigation procedure

In certain embodiments, a counter-investigation proceeds in five steps. Each step produces entries in the fork record.

1. **Fork the corpus and create the fork's index.** Fix the parent release by identity and version. Inventory the parent's sources and validated FRDs. Declare which sources are unavailable to the fork and how that limitation is handled under §6. Identify which index entries are reused and which priorities are changed, and why. A ranked index remains guidance, not evidence (*02* §6).

2. **Modify the hypotheses and create the fork's header.** State the fork's hypotheses in full under the requirements of *02* §2.1, showing changed wording, scope, assumptions, and rivals against the parent's. Preserve a meaningful unresolved outcome. A source-only fork may retain the parent's header and says so explicitly. Where the fork tests a different research question rather than a different answer to the same question, the fork record identifies that, because §4.5 treats the two cases differently. Build the header with *03* and freeze it under *02* §9.

3. **Add overlooked sources.** Declare additions, removals, and replacements with reasons. For each addition, record the provenance and shareability fields required by *02* §4. Record authenticity checks, concerns, and unknowns for added sources separately from extraction fidelity: validation under *09* establishes whether a claim matches its source, not whether the source is what it purports to be. Reconcile corpus, manifest, index, header, and configuration before freezing (*02* §7).

4. **Run the affected ACH 2.0 work.** Apply §4.4 to determine which stages are rerun. Inherit unchanged source-fidelity work by adoption entries. Generate new FRDs under *08* and validate them under *09*, initializing both from the fork's deployed Archivist instructions and never from the header. Complete the affected later stages or record them as pending.

5. **Present the outputs in the counterargument.** Produce the public argument under §5, showing accepted evidence, declared changes, disputed interpretation, results, and remaining uncertainty, with the comparison limited to what §4.5 permits.

An independent fork requires no endorsement from the parent's author. Access and reuse conditions attached to the parent's materials travel with them under §6.

### 4.4 Determining what must be rerun

A fork records each stage of the specification as **rerun**, **inherited by reference**, **pending**, or **not applicable**, with the artifact and the reason. These are fork-accounting fields; they are not added to the validation prompt or to the five output fields of *09*. The following table states, for each kind of change, the work to review or rerun and the work that may remain inherited.

| Change declared | Work to review or rerun | What may remain inherited |
|---|---|---|
| Public argument only; no analytical change | Check the argument against the cited records; disclose that no new analytical run occurred | All analytical artifacts |
| FRD claim, evidence, attribution, locator, or provenance | Validate the correction under *09*; review descendants of the corrected record and any earlier assessment that relied on the error | Records with unchanged dependencies |
| Sources or index priorities | Review ingestion and index (*02* §§4–7); rerun the affected quest work; harvest and validate new claims; propagate changes through witnesses, language tools, and coverage | FRDs whose validation basis is unchanged |
| Hypotheses or header | Conduct quest work under the new frame; reassess question applications, language tools, hypothesis coverage representation, semantic matching, coverage sets, and cruxes (*02* §§21–29) | Sources and source-grounded FRDs, subject to §4.2 |
| Prompts, models, evaluator, gauge, or configuration | Rerun the changed stages and their descendants; disclose changes to selection and stopping | Work whose inputs and governing rules are unchanged |

Dependencies are reviewed before a stage is marked inherited. A small edit to one FRD can alter the custom dictionary (*02* §21), and through it the canonicalizer, transcoder, and every transcoded artifact. Inheritance of a downstream artifact is legitimate only when every artifact it depends on is also unchanged.

**Inherited questions.** Witness construction under *02* §24 requires the FRD's producing question. For an inherited record, the fork's question database holds an inherited question record carrying the parent's exact question text and QID, marked as not issued in the fork's quest. That record is available as the compression lens for the inherited FRD's origin witness and for fidelity audit under *02* §25. It is not counted as quest activity, does not form a query-response round, and does not affect the fork's stopping rule. New questions, question applications, and witnesses created in the fork have distinct identities; applying a fork question to an inherited FRD never replaces that FRD's producing QID (*02* §24). Where the parent's producing question is unavailable, the inherited FRD may still be inspected and cited, but its required origin witness cannot be constructed, and the fork's stage accounting discloses that limitation.

**Blinding is preserved across forks.** The fork's public argument, its preferred conclusions, and any metadata that reveals its research frame are kept out of validation kits, as the parent's were (*02* §18.1; *09*, generator instructions). Origin filenames are replaced with opaque references in the validation copy and the mapping is retained outside the kit. A context that has read a public argument — the parent's or the fork's — is a context exposed to a preferred outcome and is retired from validation duty (*02* §18).

### 4.5 Comparison discipline

A fork's counterargument compares the fork to its parent. The records support some comparisons and not others.

| Situation | Comparison the records support | Limit |
|---|---|---|
| The same inherited record, by version | An exact shared source-grounded claim; differing interpretations of it | Shared evidence does not entail shared conclusions |
| Revised, split, or competing records of the same passage | Wording, source text, repairs, verdicts, readiness, and reasons, via the correspondence record | Linked records remain distinct; equivalence is not assumed |
| Same frame, changed corpus | Evidence changes and results under each run's declared configuration | Numerical comparison also requires a compatible evaluator, gauge, evidence contract, input accounting, and checkpoint basis (*05*) |
| Changed frame, with or without corpus changes | Shared records, changed propositions, and the reasons conclusions differ | No direct contest between allocation vectors or between run-specific witnesses, coverage sets, or rival theories |
| Several inputs changed together | The observed difference between the two declared runs | Attribution of the difference to any one change requires a controlled comparison |

Three kinds of comparison are therefore distinguished. **Correspondence** shows where the runs agree or disagree about evidence: it operates on validated records and, where records were independently created, on correspondence records. **Results under declared configurations** shows what each run concluded under its own conditions; it is a report, not a contest. **Controlled comparison** shows whether a particular change explains a particular difference; it requires the parent's frozen inputs to be held fixed except for the change under test, and it accounts for ordinary run-to-run model variation before attributing a difference to the edited input (*01* §6.11).

Shared records do not make the runs' witnesses, coverage sets, or frozen rival theories interchangeable. Each of those is built from a run-specific dictionary and transcoder (*02* §§21–23) and belongs to its run. Nor do shared records replace the evidence contract under which ACH_Eval was deployed (*05*). A public argument that places two allocation vectors side by side as a score contest, where the frames or contracts differ, makes an unsupported comparison under §4.6.

**"The diff is the entire argument."** Under this supplement the phrase means an account of what changed, why it was changed, and what the records show followed. The mechanical difference between two repositories supports that account; it is not a substitute for it. The account distinguishes changed evidence, corrected source claims, and changed interpretation, because the records distinguish them.

### 4.6 Responses, corrections, and defect conditions

**Challenge lifecycle.** A challenge is linked to the version of the record or release it targets. In certain embodiments the release's author or another reviewer records a response with its evidence and date, and the challenge takes one of four states: awaiting review, accepted correction, answered with reasons, or unresolved disagreement. Conflicting assessments are retained rather than resolved by deletion. Silence is recorded as unanswered; no verdict is inferred from nonresponse. Repeated objections are grouped by substance so that an unanswered issue remains visible without repetition being counted as corroboration. An accepted correction is linked to every record and result it affects, and downstream implications are marked pending until a review or rerun resolves them. The people who find errors, supply sources, or improve a question are credited in the record.

**Where a challenge lives.** A challenge is published in the challenger's own record with a link to the targeted version. Hosting of challenges by the parent's author, and aggregation of challenges across repositories, are conveniences a deployment may provide; neither is a condition of a challenge's validity, and a parent's author cannot suppress a challenge by declining to host it. Sibling forks that reach different conclusions from shared evidence are preserved as siblings; shared evidence does not require a shared conclusion. Repeated forks drawing on the same evidence are distinguished from independent corroboration.

**Capture resistance, stated at its scope.** Independent forking allows an influential release's framing and source choices to be contested even when its author declines to change them. The benefit is conditional: it depends on people producing, finding, and examining serious competing work. Visible changes and retained histories aid accountability. They do not establish that a release disclosed everything, that its author acted in good faith, or that the better fork will reach the right audience. In the initial deployment, repository-based participation serves technical users and domain experts; browsing, forking, and comparison interfaces for a wider audience are later implementation work.

**Defect conditions.** The following defects attach to the specific assertion or artifact affected. A defect in one part of a contribution does not invalidate a valid correction elsewhere in it.

| Defect | Consequence recorded |
|---|---|
| A parent source or FRD is removed or excluded without declaration | The change declaration is incomplete |
| An inherited validation is presented as validation performed by the fork | The work and provenance are misstated |
| An inherited record is altered under its original version identifier | The identity and comparison trail are broken |
| A favorable verdict is used in place of readiness to admit a record to witness construction | The admission is unsupported |
| Candidate wording rejected at validation is restored in the fork | Source-fidelity failure |
| A reuse caution attached to an inherited record is contravened without a recorded alternative validation or reading | Source-fidelity failure |
| A difference produced by several changes is attributed to one of them without a controlled comparison | The causal explanation is unsupported |
| Allocation vectors from incompatible frames or contracts are presented as a score contest | The numerical comparison is invalid |
| An early stop, a pending stage, or a search-limit unknown is presented as a resolved result | The completion or result claim is false |
| Source fidelity is presented as source authenticity, reliability, or truth | The evidential claim is unsupported |
| Missing source text or an unavailable producing question is concealed rather than disclosed | The audit and rebuild disclosure is incomplete |

These conditions extend the failure language of *02* §§14, 25, 27, 29.1, and 33 to the relationship between runs. They do not replace it.

## 5. Module 2 — The public argument document

**Inputs.** The run's claims and analysis; its complete validated FRDs; and, for a fork, the fork record or, for a challenge, the challenge record.

**Output.** One public argument, or counterargument, with links to the underlying records. In the initial deployment the document is Markdown with repository links. Where the run has produced the analyst-facing report of *02* §30.1, the public argument may incorporate it and observes its word limit; the public argument is not a second report and does not require another narrative or a further evidence database.

### 5.1 Structure

In certain embodiments the public argument has eight parts, in this order.

1. **Position and target.** The proposition advanced. For a fork or challenge, the parent release by identity and version and the exact conclusion, record, or proposition disputed.

2. **Category of disagreement.** For a fork or challenge, one or more of: source error; missing evidence; disputed interpretation; applicability mismatch; omitted explanation; changed research question. The category determines which comparisons §4.5 permits and signals to a reader whether the dispute is about what a source says or about what follows from it.

3. **Common ground and changes.** The inherited records adopted, the parent records excluded with reasons, the sources added, the records repaired, and the records contested. This part links to the fork record's change declaration and does not restate it.

4. **Argument.** For each consequential inference: what the source reports; what the participant infers; why the inference bears on the competing explanations; and the conditions and limits that connect the source to the inference. Each source report links to a validated record by version. A synthesis across several records names each premise and is presented as the participant's inference, not as source testimony.

5. **Counterevidence.** The adverse findings in the record; the strongest objection to the participant's own account; and the participant's response or the uncertainty that remains. A public argument that omits adverse findings present in its own validated records is defective under §4.6.

6. **Work and results.** Which stages were rerun and which inherited, by reference to the stage accounting; what moved and what did not; and the comparison to the parent, limited to what §4.5 permits.

7. **Open disagreement.** What would change the participant's view; the next observation, source, analysis, or experiment that could discriminate between the remaining accounts; and, where no feasible discriminator is known, a statement to that effect.

8. **Audit and reply route.** Links to the complete evidence records, the source-access record under §6, and the means by which a reader can publish or submit a linked challenge.

### 5.2 Reading levels and linkage

A public argument is read at three levels, and the document is organized so that a reader can stop at any of them: the plain-language argument; the consequential claims on which it depends, each linked to its record; and the complete validated FRDs with their audit artifacts. Displayed assertions link to FRD versions, not to FRDs generally, so that a later repair does not silently change what an argument cited.

Qualifications, adverse findings, and access limits are placed beside the inference they constrain rather than collected in a separate section a reader may skip. The source-supported proposition is kept distinct from each run's assessment of its significance. Weakening one explanation does not establish the participant's alternative, and the document does not present it as doing so. Evidential disagreement is kept distinct from disagreement about values, risk, or action; the two may coexist on the same evidence. Popularity, the number of forks, and repeated model agreement are not evidence weights and are not presented as such.

### 5.3 Contributions beyond a verdict

Corrected attributions, overlooked sources, narrowed claims, critical reanalyses, and research proposals are recognized as contributions in their own right, separable from any verdict on the hypotheses. A research proposal built from the records identifies the supported premises, the rival explanations, the missing information, and the discriminating measurements; a rationale for testing an intervention is a rationale, and the public argument does not present it as evidence of effectiveness.

Where a participant seeks expert review of a consequential claim or crux, the handoff and response are governed by the post-crux review design maintained separately from this supplement; the public argument routes the expert's response into a challenge, a continuation under *02* §32, or a fork, without duplicating that design.

In certain embodiments the deployment evaluates the public layer by asking whether a new reader can find the source behind a disputed claim, whether readers can identify the strongest objection and state where the disagreement lies, whether a person can contribute one useful correction without specialist software or a full rerun, whether later versions retain adverse findings and adopt warranted corrections, and whether participants distinguish shared evidence from shared conclusions. Effort and access barriers are measured alongside participation. Increased participation alone is not evidence of improved accuracy.

## 6. Module 3 — Publication under incomplete source access

**Inputs.** The publication artifacts of *02* §34; the source manifest; the validated FRDs; and the actual access and reuse information for each source.

**Output.** A versioned publication package; a source-access record; and rebuild instructions stating which claims a reader can check and which stages a forker can repeat.

### 6.1 Publish complete records or identify omissions

The public argument links to the release package of *02* §34; this module does not define a competing release checklist. For each source whose full text is not included in the package, the source-access record retains the citation, a stable identity, the edition or version, a description, the locators cited by any FRD, the reason for omission where known, the records that depend on the source, and the known routes by which a reader may obtain it. Paywalled, copyrighted, unavailable, and withheld-by-choice are recorded as distinct reasons; they are not treated as one category.

For each dependent record, the source-access record states whether validation used the full source, an excerpt, or a transmitter's account, and keeps that past inspection distinct from the source's current public availability.

Publication review covers text reproduced inside validated FRDs as well as source files. Because a complete validated record reproduces the controlling source passages, removing a source file from the package does not remove that source's text from the FRDs that cite it. Where part of a record cannot be published, the published view preserves the record's version reference and identifies what has been omitted; a claim-only or redacted view is identified as such and is not represented as the complete validated unit.

### 6.2 Auditability specific to the claim

A release does not carry a single trust label. Auditability is stated per claim, according to what a reader can actually obtain.

| Material available to the reader | What the reader can inspect | Remaining limitation |
|---|---|---|
| The full named source and the complete validated record | The claim and its surrounding source context | Authenticity, reliability, and interpretation remain contestable |
| The complete validated record with its reproduced source excerpts | The recorded claim, the quotations, and the validation reasoning | Full context and quotation accuracy may require obtaining the source |
| Citation and description only, with incomplete evidence text | The identity of the dependency and its access routes | The public view alone cannot establish source fidelity |
| An inherited validation, where the fork could not access the source | The earlier recorded check, by reference | No validation repeated by the fork |

Access gaps are linked to the specific claims and results they affect. The record distinguishes acquisition, inspection, copying, and redistribution as separate matters. Shared-notebook access is described only as it actually exists in the deployment; the fact that a source is technically reachable through a retrieval service is not represented as permission to redistribute its contents.

### 6.3 Rebuild and maintenance

A fork inherits source identities, FRD versions, validation history, and access limitations visibly. The rebuild instructions list the inputs each stage requires, including the exact producing questions needed for origin witnesses; those questions remain outside blind validation packets (*02* §18). Separately obtained copies, alternate editions, conversion changes, and unavailable settings are recorded, and material differences are reviewed before a fork claims an unchanged validation basis for an inherited record. The fork states what it obtained, what it inspected, what it reran, and what it inherited. Repeating a procedure under the recorded conditions is distinguished from reproducing an identical model output; the former is what rebuild instructions enable.

Corrections and access changes are preserved through dated successor records. Where source text must be removed from a package, historical pointers are kept where permissible so that the analysis remains intelligible and its gaps are described rather than silently absorbed.

### 6.4 Legal and operational posture

The protocol is an analytical and publication method. It makes no determination about the legality, in any jurisdiction, of acquiring, uploading, quoting, or redistributing any source. The release identifies who acquired and uploaded each source, who published each release, which services expose material to readers, and where correction or removal requests are directed. Each publisher and each forker is responsible for its own release choices under applicable law. Hosting services and retrieval services have roles distinct from the publisher's; the location at which a file is stored identifies where notices and removal requests are handled and does not by itself settle legal liability.

Known licences, permissions, restrictions, and jurisdiction-specific questions requiring release-level assessment are recorded with the source-access record. The protocol supplies no universal conclusion about fair use or equivalent doctrines and no legal clearance for any use. Where a jurisdiction provides conditional limitations on intermediary liability, such as statutory safe-harbor regimes, those limitations are referenced as conditional and are not represented as a general shield. Legal characterization for a particular deployment or filing is kept separate from the evidence method and is a matter for counsel.

## 7. Integration with the specification

The following clarifications are proposed for the specification writer. They identify provisions of *01*, *02*, *08*, and *09* on which this supplement relies and state the reading it requires. They are proposals, not assertions that each rule is already explicit.

| Anchor | Clarification |
|---|---|
| *08*; *02* §§16–17 | Response-by-response harvesting, one claim per FRD, one producing QID, the `disambiguate` status, and harvest accounting are preserved unchanged. The public layer adds nothing to the generation prompt. |
| *09*; *02* §§18–19 | The complete repaired deliverable is the inheritable unit. The verdict on the original candidate and the readiness of the repaired FRD are distinct. Reuse cautions form part of the unit. Fork metadata is kept outside the five output fields. |
| *02* §§8, 24 | A fork's question database may hold inherited question records, marked as not issued in the fork's quest, solely to support required origin reuse and fidelity audit for inherited FRDs. Inherited question records are not merged with issued questions, are not rounds, and do not affect stopping. |
| *01* §6.9; *02* §§20, 34.1 | An adoption entry is a reference to a parent artifact, not creation of a new artifact and not revalidation. The non-merger rule of *02* §20 is satisfied because the inherited record keeps its originating run's identity. |
| *02* §34.1 | The rerun requirement of "disagreement is demonstrated by re-running" is scoped to claims of a counter-investigation or counter-run. A challenge under §4.1 is a valid public contribution that makes no such claim and requires no rerun. |
| *01* §3.3 | A header-changing fork performs its own coverage review against its own frame; inheritance of the parent's records does not discharge it. |
| *02* §§30–34 | Core termination, the report limit, qualified result claims, and the publication artifacts are preserved. The public argument and the source-access record are added as linked artifacts. |
| *05* | ACH_Eval outputs are comparable across runs only under the conditions stated in §4.5, which are the conditions *05* itself imposes on sibling comparison. |

The FRD generators are not rewritten to implement the public layer. The retired two-domain method and alternative scoring proposals remain outside this supplement.

### 7.1 Worked cases

The following cases are supplied for the specification writer as tests that a drafted rule set should handle. They are described, not resolved, here.

1. **Shared record, different interpretation.** Two runs adopt the same validated record concerning a commentator's cross-reference between two passages. One treats the cross-reference as establishing an identity; the other treats it as insufficient. The record is unchanged in both; the hypotheses, witnesses, and downstream analysis differ. The public arguments cite the same record version and disagree in part 4.

2. **Wrong candidate, ready repair.** A candidate claim is judged WRONG at validation and repaired to a narrower supported claim marked READY. A fork adopts the repaired record. The original candidate wording remains preserved in the record's verdict field and is not restored by the fork; a fork that restores it commits the defect in §4.6.

3. **One correction, no full rerun.** A challenger shows that a public argument omitted a qualification present in its own validated record. The challenge is accepted. Downstream implications for the coverage sets are marked pending. No replacement theory is required of the challenger, and the release's author does not owe a full rerun to accept a correction.

4. **Restricted source.** A forker cannot obtain a source the parent validated against. The fork adopts the parent's record by reference, marks the validation as inherited without repetition, and the public argument's claim-level auditability entry states that the reader cannot independently check that claim from the fork's package.

5. **Changed corpus and header.** A fork adds two sources and revises one hypothesis. Its allocation differs from the parent's. The public argument reports the difference under §4.5, does not attribute it to either added source without a controlled comparison, and does not present the two allocation vectors as a contest.

## 8. Statements deliberately not made

For accuracy, this supplement does not assert:

- that forkable publication produces neutral or unbiased public discourse; the claim is that it makes framing, source choices, and inferences inspectable;
- that any contribution route establishes the truth of a hypothesis; the routes establish what work was performed and what its records show;
- that a shared validated record makes two runs' witnesses, coverage sets, rival theories, or allocations comparable; §4.5 states the comparisons the records support;
- that inheritance of a parent's records discharges a fork's obligation to quest and review coverage under its own frame;
- that the number of forks, challenges, or participants measures the quality of a conclusion;
- that the protocol makes or implies any legal determination about the use of sources; or
- that the social effects named in §3.5 have been demonstrated. They are design goals for evaluation.
