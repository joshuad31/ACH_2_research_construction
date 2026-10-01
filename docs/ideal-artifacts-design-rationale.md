# Dream Artifacts in ACH 2

## Motivation and scope

ACH 2 needs a way for components building a shared representation to remember both what they have learned and what they still need to learn. A dictionary should preserve useful senses and sentence constructions. A canonicalizer should derive rules that preserve those distinctions during transformation. Neither component can judge every new input adequately by examining that input alone.

The proposed strategy is to retain explicit “dream artifacts”: descriptions of missing inputs and the improvements those inputs could justify. These records guide collection, connect downstream needs to upstream searches, and make incomplete understanding inspectable. They are proposals about useful information. Their contents acquire evidentiary authority only through the normal source and validation requirements.

This rationale explains why that strategy is appropriate for dictionary construction and rule development, why it should remain outside the core of local extraction and validation, and how the components can exchange needs without manufacturing support. The strategy is a design hypothesis. Its effectiveness remains to be demonstrated through downstream performance.

## The failure that motivates the strategy

In earlier attempts, I asked a model to take local inputs and harvest dictionary entries. The resulting collections could contain too many low-value entries while simultaneously omitting entries that should have been created. Increasing the amount collected did not by itself solve the selection problem.

Those failures suggest that the missing capability was judgment about the collection as a whole. A locally plausible entry can contribute little to the task. An ordinary-looking sentence can be indispensable because it establishes a boundary, qualification, or construction that no retained specimen expresses. A collector that lacks a persistent account of these needs has little basis for distinguishing the two.

This is a plausible diagnosis of the reported failures, not a controlled finding about their cause. Search coverage, prompt ambiguity, context limits, and execution errors could also have contributed. The proposed mechanism addresses one specific weakness: collection without a durable representation of purpose, existing coverage, and unresolved needs.

## Why local extraction is insufficient for collection design

The FRD generation template processes one query response at a time. It extracts individual source-attributed claims, preserves qualifications, and records unresolved attribution. The validation template then checks each candidate against its named sources. Its central question is whether those sources support the repaired claim. These constraints make the work comparatively local. [1, 2]

Such transformations still require judgment. They are not deterministic merely because their inputs are fixed. However, the standard for a faithful claim does not require the validator to decide which vocabulary best serves the entire research project. In fact, the validation template deliberately excludes hypotheses, preferred conclusions, source rankings, and downstream relevance judgments. [2]

Dictionary construction has an additional dependency. The usefulness of a candidate depends on the existing collection and its intended use. Ten nearly equivalent examples may add less than one sentence that identifies a previously hidden exception. A later source may reveal that two apparent synonyms name different things. That discovery can make an earlier sentence worth retrieving and preserving.

Rule development has the same dependency. The canonicalizer must compare specimens, infer the scope of a transformation, and determine what would establish its limits. An isolated sentence may justify a narrow transformation but leave a general rule unsupported. Processing each sentence independently and concatenating the results does not resolve that problem.

Local harvesting can therefore remain part of the implementation. It needs a collection-level process that compares, prioritizes, revisits, and requests additional material. Dream artifacts are a proposed way to make that process explicit and persistent.

## A working representation of the corpus

The system needs access to a revisable representation of the corpus as a whole. It cannot possess complete knowledge of material it has not seen. Its representation must distinguish inspected content, reported leads, unknown areas, and inferences about what might be useful.

This requirement does not imply that the entire corpus must reside in the model’s neural network or that prompting changes its trained weights. A practical implementation can combine current context, persistent artifacts, indexes, and retrieval. The artifacts preserve the state between runs. Relevant portions are supplied when the model evaluates a new candidate.

The representation should retain enough information to answer several questions: What meanings and constructions are already represented? Which distinctions matter to the research task? Where are competing interpretations still possible? Which source locations might resolve them? What new evidence would change the current dictionary or rulebook?

Mr. Fusion and ACH_Eval can provide useful summaries of investigative needs. They remain partial representations with their own limitations. Their outputs can direct attention but cannot certify that an unseen sentence exists or establish a canonicalization rule. Under this design, Mr. Dictionary remains the sole admissible source for word senses, aliases and equivalences. Grammatical rules may be invented and dream-inspired, as Mr. Canonicalizer v1.1 allows.

## Human value as an explicit selection criterion

The collector needs a proxy for what the analyst considers valuable. That proxy should describe the distinctions necessary to interpret and compare the hypotheses faithfully. It can include ambiguous terms, differences between alternatives, important qualifications, and errors the transcoder must avoid.

Value in this setting means usefulness for understanding the question. Material that weakens a favored interpretation can be especially valuable if it prevents a misleading transformation. A sentence preserving uncertainty or distinguishing two apparently similar mechanisms may be more useful than a sentence that strongly endorses an expected conclusion.

The research frame should therefore influence search priorities without changing standards of support. A high-priority distinction deserves investigation. It does not deserve an entry or rule unless the admissible material supports one. Unexpected discoveries must also remain eligible, because the analyst’s initial account of what matters can be incomplete.

## The common dream function

The common operation is:

> Given the current artifact and its intended use, describe an unresolved need, the observable input that could resolve it, and the change that input would justify.

An ideal input is ideal relative to a need. It need not be eloquent, comprehensive, or favorable to a proposed rule. It might be an awkward sentence that carries the one exception the collection lacks. It might invalidate a hoped-for equivalence and justify keeping two expressions separate.

A compact dream record should identify the unresolved need, why it matters, the characteristics of a useful input, and the possible change to the artifact. It should also preserve the origin of the request and any search pointer. These are common semantics for the components to share, not a requirement to impose a large new schema on every prompt.

Imagined wording can make a search target concrete, but it must remain labeled as imagined. Recognition should depend on the relevant meaning or construction, not an exact wording match. A dream can be fulfilled, revised, superseded, or left unresolved. Failure to find the desired input does not establish that the corpus lacks it.

## Exchange between the dictionary and canonicalizer

The two components exchange needs in both directions while preserving different levels of authority.

| Direction | What travels | Permitted effect |
| --- | --- | --- |
| Canonicalizer to Dictionary | Missing specimens needed to establish a rule or boundary | Create or refine a collection goal |
| Dictionary to Canonicalizer | Unresolved senses, construction gaps, and dreamed specimens | Suggest a rule question or possible distinction |
| Dictionary to Canonicalizer | Admissible collected specimens with context and provenance | Support, narrow, or defeat a proposed rule |
| Other relevant input to either component | Research priorities, interpretations, or possible leads | Generate dreams and search questions only |

For example, the canonicalizer might be considering whether two expressions can share one canonical form. It asks the dictionary for specimens that establish whether they are equivalent, distinct, or equivalent only under specified conditions. The dictionary hunts for those specimens and may discover another sense that changes the original question.

Conversely, a dictionary dream may alert the canonicalizer that an apparently simple term has an unresolved boundary. The canonicalizer can build the grammar for it at once. A grammatical rule makes no factual claim: a rule for phrasing "A improved X more than Y" says nothing about whether A did. Its illustrations must still preserve what their before-sentences say.

The line runs between grammar and meaning. Dreams can create grammar immediately. They cannot create a word sense, an alias, an equivalence between terms, or a finding. Those still need admissible dictionary material.

Repetition across components adds no evidentiary weight. A request that originates in the canonicalizer and returns through the dictionary remains the same request. Shared IDs or clear origin pointers should make that lineage visible.

## Processes that need the mechanism

The mechanism belongs where the value of an input depends materially on a developing collection or an unresolved downstream capability. The following assignments are proposed design guidance; they do not claim that every existing prompt already implements these behaviors.

| Process | Role for dream artifacts | Reason |
| --- | --- | --- |
| Mr. Dictionary | Core collection function | Specimen value depends on coverage, missing senses, and future rule needs |
| Canonicalizer during rule development | Core rule-development function | Scope and exceptions require comparison and targeted acquisition |
| Investigator or research coordinator | Useful planning function | Unresolved needs can become source searches and questions |
| Mr. Fusion and ACH_Eval | Suppliers of needs and possible search questions | Their broader research view can identify consequential ambiguities |
| Transcoder during execution | Report unresolved cases | A blocked transformation can reveal a missing rule or specimen |

For the dictionary, dreaming should occur as understanding changes. After a source has been processed, the collector can ask what it now knows to seek. A chart or table can reveal a distinction missing from retained sentences and thereby motivate a search. Visual information does not become an attested sentence merely because the model can describe it.

For the canonicalizer, dreaming should accompany rule proposals and boundary checks. The component should ask which specimen would discriminate between competing rules, establish an exception, or show that no safe generalization is currently available.

For investigators and coordinators, the mechanism is an agenda for acquisition. For Mr. Fusion and ACH_Eval, it is a way to communicate unmet investigative needs. Those roles do not allow dreams to enter evidentiary scoring as findings.

## Processes whose core work should remain local

A process does not need the full dream mechanism merely because it uses an LLM or handles difficult language. The decisive question is whether its present correctness depends on designing a broader collection.

| Process | Appropriate boundary | Why |
| --- | --- | --- |
| FRD generation | Extract faithful candidate claims and report gaps | Relevance is scoped, but anticipated future findings must not alter claims |
| FRD validation | Check named sources and repair only supported content | Research expectations could contaminate the independent check |
| Witness construction from a validated FRD | Compress faithfully within the authorized input | Missing content cannot be supplied from an imagined ideal witness |
| Transcoder applying established rules | Apply justified rules or preserve unresolved wording | Execution must not invent a new rule to complete a transformation |
| Coverage and matching checks | Evaluate actual supplied units and relations | A desired match cannot count as an established match |

These processes can emit failure reports or unmet needs without becoming speculative generators. A validator can report unsupported attribution. A witness builder can identify missing context. A transcoder can report an ambiguous construction. A separate planning component can translate those reports into acquisition goals.

Likewise, a coverage planner selecting among witnesses may need a view of the complete set even though constructing an individual witness remains local. Global state and dream generation are separate requirements. A process can require the whole set while still having no reason to imagine evidence.

This separation preserves a useful division of labor. Planning asks what information would help. Extraction and verification determine what the available material actually supports. Rule application uses the supported results.

## Conditions for a trustworthy implementation

Dreams should seek inputs that discriminate between possibilities. A request to establish whether two terms are interchangeable is more useful than a request to prove that they are. Counterexamples and narrowing conditions must count as successful acquisitions.

Every established entry or rule must retain its admissible support. Imagined specimens, research summaries, and requests cannot substitute for that support. The dictionary may admit different authorized evidence types under its own rules; those distinctions and their provenance must survive transfer to the canonicalizer.

The collection must remain open to discoveries outside its current agenda. Otherwise the dictionary and canonicalizer can reinforce each other’s blind spots. Dreams guide attention but do not define the full universe of material worth retaining.

Updates must preserve the history of changing needs. A later insight can revise a dream or rule, but the system should not silently rewrite the earlier target as though it had always anticipated the discovery. This matters when interpreting whether a search succeeded and why a transformation became permissible.

The process also needs bounded stopping. It can stop when the current inputs support no further useful changes or when an authorized resource limit is reached. Unfulfilled dreams can remain. Neither a long Wanted list nor a full collection establishes quality.

## Alternatives and evaluation

Dream artifacts are not the only conceivable solution. An implementation could collect broadly and curate globally, use a human-authored vocabulary, cluster candidate usages before review, or retrieve examples only when a transformation fails. Each is a possible way to introduce context beyond isolated extraction. Their suitability depends on corpus size, review cost, and the downstream task.

The proposed strategy is attractive because it records the acquisition rationale in an artifact that another run or component can use. It allows emerging needs to change subsequent searches without requiring the entire corpus to fit in one context. Those benefits remain hypotheses until measured.

A useful evaluation would compare local harvesting, harvesting with a persistent coverage summary, and harvesting with both the summary and dream exchange. Give each condition comparable source access and processing budgets. This distinguishes the benefit of maintaining global state from the additional benefit of explicit dreams.

Judge the resulting dictionaries and rules on previously unused material. Measure missed important senses, low-value or unsupported entries, incorrect equivalences, lost qualifications, and faithful transcoder outputs. Include appropriate abstention when a transformation is unsupported. Vary source order to see whether early expectations dominate the collection.

More specimens or more completed dreams would show activity. Better interpretation at a comparable cost would support the strategy. Until then, the justified position is that the mechanism addresses a plausible failure mode and offers an inspectable way to test the proposed repair.

## Source basis

[1] [FRD generation prompt generator](../prompts/frd-generation-prompt-generator.md), published from `08_FRD_Generation_Prompt_Generator_Template_v3.1.md`. Relevant provisions include processing one response at a time, claim-level attribution, preservation of qualifications, and harvest review.

[2] frd-validation-prompt-generator.md. Supplied template. Relevant provisions include named-source-only checking, exclusion of the research frame, and readiness based on repaired source support.

The motivation also draws on Joshua Davis’s account of earlier dictionary-generation failures and the dictionary–canonicalizer design discussion of September 25, 2026. Process assignments beyond the two supplied FRD templates are proposals in this rationale.
