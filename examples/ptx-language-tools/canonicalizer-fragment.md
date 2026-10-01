---
artifact_type: ACH-CANONICALIZER-FRAGMENT
investigation_id: PTX-URIN
fragment_id: PTX-URIN-CAN-V11-P2
parent: PTX-URIN-CAN-V11-P1
dictionary_input: PTX-URIN-MD2-P8 [compiled view PTX-URIN-DICT-C8]
prompt: Mr_Canonicalizer_4-ACH_v1.1.md
status: cumulative rulebook, pass 2
---

# Mr. Canonicalizer: pass 2 under prompt v1.1

## Working frame

**Pass-2 input.** P1 below, the P8 dictionary, and Astra's three rule-example corrections. The P1 working frame is kept as written; pass-2 changes are listed under "This pass [P2]".

**P1 input.** Only the cumulative P7 Dictionary was supplied as task input. This is a fresh run: the rule IDs below begin at R-001 and do not inherit any earlier canonicalizer artifact. P7 contains P1–P6 inside nested fences and later P7 additions. I treated historical status tables as history, retained entries and amendments as the current collection, and repeated E-references as pointers to one Example rather than additional specimens. P7 reports 63 entries (59 ACTIVE, three PROVISIONAL, one CONFLICTED), 290 Examples, and eight open dreams. Its reports of earlier source inspection are not source inspection by this run.

**Inferred investigation need.** Compare language about pentoxifylline (PTX) and impaired voiding while distinguishing obstruction, detrusor function, pelvic-floor behavior, drug timing, endpoints, and competing explanations. Exact operative hypotheses were not supplied. A rat, dog, kidney, inflammatory, or endocrine sentence can teach a portable construction without establishing a human urinary result.

**How to use the pantry.** Each R-record gives **match → render; use; example; origin**. All before → after examples in the rule records are **INVENTED GRAMMAR**. They illustrate possible English sentences, not findings from a study. E-/D-/DR-IDs name P7 inspiration and do not certify any invented claim. Bracketed slots inherit actual values and qualifiers from the input. Use a rule on the stated phrase or clause while passing all other content through unchanged. A chosen rendering must preserve the input sentence's claim; provenance of the grammatical pattern needs only approximate correspondence to its inspirations. When a rule gives alternatives, select one using the actual input context.

## Rulebook

### Treatment comparisons and sentence architecture

**R-001 — Expand a local drug name.** Match an abbreviation locally defined as `[agent]` → `[agent] ([abbreviation])` at first mention. Use only in that source's sense. Example: “PTX changed X” → “Pentoxifylline (PTX) changed X” after an explicit local expansion. Origin: D-001, E-107. Keep POF, PTF, PTXF, Ptx, PEN, and TAM source-specific until individually established.

**R-002 — Expand an arm label.** Match `[condition]+[shorthand]` → `[condition] plus [locally defined treatment]`. Use the arm key in the same experiment. Example: “PUO+TAM received X” → “The PUO plus tamoxifen arm received X,” if that source defines TAM as tamoxifen. Origin: D-002/D-003, E-021. The F008 drug tamsulosin is a separate word and exposure.

**R-003 — Express shared background treatment.** Match `[A+B] versus [A+placebo]` → `[B] added to [A] versus placebo added to [A]`. Use when both arms actually received A. Example: “B+A versus placebo+A” → “B added to A versus placebo added to A.” Origin: E-001/E-002/E-173. Carry doses, duration, and arm sizes from any surrounding context.

**R-004 — Express an incremental result.** Match `[A+B] changed [endpoint] versus [A]` → `adding B to A changed [endpoint] relative to A alone`. Use only for the reported outcome and comparator. Example: “A+B lowered X compared with A” → “Adding B to A lowered X relative to A alone.” Origin: E-013/E-174/E-178. A claim of synergy needs separate wording if the author makes it.

**R-005 — Represent a four-arm factorial comparison.** Match `[A+B], [A+placebo], [placebo+B], [double placebo]` → `combination, A alone, B alone, neither`. Use only when all four arms are defined. Example: “A+B; A+P; P+B; P+P” → “A with B; A alone; B alone; double placebo.” Origin: E-083. This is an arm map, not an interaction finding.

**R-006 — Unpack paired assignments.** Match `[groups A,B] received [treatments X,Y], respectively` → `[group A] received X; [group B] received Y`. Use when the ordered mapping is unambiguous. Example: “A and B received X and Y, respectively” → “A received X. B received Y.” Origin: E-021/E-239; generalized. Preserve a shared route or treatment interval in both clauses or one clear shared frame.

**R-007 — Unpack paired results.** Match `[A,B] changed [measure] by [x,y], respectively` → `[A] changed [measure] by x; [B] changed it by y`. Use only if units and signs attach correctly. Example: “X fell 3 and 5 units with A and B, respectively” → “X fell 3 units with A and 5 units with B.” Origin: E-013/E-109; generalized.

**R-008 — Display arms against a shared comparator.** Match `[A] and [B] each compared with [C]` → `versus C: A [result]; B [result]`. Use when the original reports each direct contrast. Example: “A and B had less X than C” → “Compared with C, A had less X and B had less X.” Origin: E-059/E-235. Keep endpoint and test specific to each arm.

**R-009 — Keep chained contrasts separate.** Match `A versus B` and `B versus C` → two direct comparisons. Example: “A exceeded B; B exceeded C” → “A exceeded B in one comparison. B exceeded C in another.” Origin: E-087/E-277; generalized. An A-versus-C measurement remains unstated.

**R-010 — Turn a noun phrase into a proposition.** Match `[agent]'s reduction of [measure]` → `[agent] reduced [measure]` when agency and direction are explicit. Example: “The reduction of X by A” → “A reduced X.” Origin: E-013/E-266; generalized. Retain author attribution and uncertainty outside the phrase.

**R-011 — Make a named actor explicit.** Match `[measure] was assessed by [method]` → `[method] was used to assess [measure]`. Example: “Residual was measured by ultrasound” → “Ultrasound was used to measure residual volume.” Origin: E-011/E-158; generalized. Do not invent an agent when none is supplied.

**R-012 — Extract a qualifying population.** Match `[patients] who [criterion] [outcome]` → `[patients met criterion]; in those patients, [outcome]`. Example: “Patients who had failed A received B” → “The patients had failed A. Those patients received B.” Origin: E-125/E-130/E-181. Keep the quantifier, if any, with the correct subgroup.

**R-013 — Unpack a list of endpoints.** Match `[treatment] improved [X,Y] but not [Z]` → separate X, Y, and Z outcomes under the same exposure. Example: “A increased flow and lowered residual but did not change volume” → “With A, flow rose and residual fell. Voided volume did not change.” Origin: E-006/E-015/E-236. If the source says only “not significantly,” retain that qualifier instead of asserting unchanged volume.

**R-014 — Break out nested clauses.** Match `[result A], whereas [result B]` → two parallel clauses with their respective actors and settings. Example: “A reduced X, whereas B increased X” → “A reduced X. B increased X.” Origin: E-024/E-104/E-169; generalized. Retain the contrast if separating the clauses could hide its purpose.

### Endpoints, quantities, and study operations

**R-015 — Separate outcome names from their values.** Match `Qmax: [x]; PVR: [y]; voided volume: [z]` → `maximum flow rate [x]; post-void residual [y]; expelled volume [z]`. Use local expansions and keep units. Example: “Qmax rose; PVR fell” → “Maximum urinary flow rate rose; post-void residual volume fell.” Origin: D-020–D-022, E-010/E-013/E-015. The measures are not synonyms.

**R-016 — Name each direction in a signed pair.** Match `[X] +[x]%, [Y] −[y]%` → `X increased x%; Y decreased y%`. Example: “Flow +20%, residual −10%” → “Flow increased 20%; residual decreased 10%.” Origin: E-013/E-178. Preserve relative percent change versus a change in percentage points.

**R-017 — Distinguish within-group from between-group change.** Match `A and B improved from baseline; A improved more than B` → one baseline statement for each arm and a separate comparative statement. Example: “Both improved; A improved more” → “Both arms improved relative to their baselines. Improvement was greater in A than B.” Origin: E-013/E-014/E-017–E-019. Use only when the comparative result is actually reported.

**R-018 — Preserve estimate type.** Match `[two event rates] plus [RD/RR/HR]` → rates plus the named absolute or relative measure. Example: “20% versus 10%, RD 10 points” → “Event rates were 20% and 10%, a ten-percentage-point risk difference.” Origin: E-144/E-257/E-270. Hazard ratio, risk ratio, and absolute difference retain their distinct labels.

**R-019 — Attach uncertainty to its estimate.** Match `[estimate] ([level] CI [low–high])` → `[estimate], [level] CI [low–high]`, for that exact endpoint and group. Example: “A: 8% (CI 5–11%)” → “A's estimate was 8%, with a confidence interval of 5–11%.” Add “95%” to both sides only if the input states the confidence level. Origin: E-087/E-144/E-154/E-257. Do not move one arm's interval to another. *Revised P2: the P1 example supplied an unstated 95% level [Astra correction 1].*

**R-020 — Retain count, denominator, and stage.** Match `[n] of [N] [attended/completed/responded]` → `among N at the named preceding stage, n reached the stated stage`. Example: “40 of 100 referrals attended” → “Forty of 100 referred people attended.” Origin: E-046/E-081/E-142/E-255. Verify which denominator the original supplies.

**R-021 — Express cumulative time correctly.** Match `[outcome] cumulative incidence [x]% at [t]` → `by t, cumulative incidence of [outcome] was x%`. Example: “Three-year cumulative incidence 8%” → “Cumulative incidence reached 8% by year three.” Origin: E-257. A cumulative percentage is not an annual rate.

**R-022 — Retain baseline-to-follow-up direction.** Match `[measure] [baseline] to [follow-up] at [time]` → `from [baseline] to [follow-up] by [time]` with measured direction. Example: “Score 8 to 5 after six weeks” → “The score fell from 8 to 5 after six weeks.” Origin: E-163/E-226. Keep arm and measure attached.

**R-023 — Express a study-defined threshold.** Match `[outcome label] defined as [instrument, threshold, time]` → `[label] required [same instrument, threshold, time]`. Example: “Success meant at least 50% improvement on two assessments” → “Success required at least 50% improvement on two assessments.” Keep “consecutive”, “office visits” or any timing only when the input states it. Origin: E-080/E-121/E-159/E-207. Keep the definition scoped to its study. *Revised P2: the P1 example turned “twice” into “two consecutive” [Astra correction 2].*

**R-024 — Keep AND, OR, and parentheses.** Match `([criterion A] OR [criterion B]) AND [criterion C]` → `C and at least one of A or B`. Example: “(Low bleeding or a one-point fall) and a score decrease” → “A score decrease plus either low bleeding or a one-point fall was required.” Origin: E-132/E-141/E-210. Do not flatten the logic into three alternatives.

**R-025 — Partition eligibility from outcome.** Match `included/excluded people meeting [criteria]` → `the enrolled population was defined by [criteria]`; leave trial effects as separate claims. Example: “Men over 40 with score ≥12 were eligible” → “Eligibility required age over 40 and score at least 12.” Origin: E-008/E-009. A screening threshold does not become an outcome change.

**R-026 — State interval inequalities faithfully.** Match `[measure] > [a] and < [b]` → `above a and below b`; use “at least” only for ≥. Example: “Flow >5 and <15” → “Flow above 5 and below 15.” Origin: E-009/E-055/E-121. Keep units and endpoint inclusion unchanged.

**R-027 — Distinguish symptoms, diagnosis, and apparatus.** Match `[symptom-defined cohort]` → its symptom or clinical enrollment label; use `test-confirmed [condition]` only if that cohort was tested. Example: “Men enrolled for weak stream” → “Men enrolled with weak-stream symptoms.” Origin: D-004/D-044, E-009/E-023/E-030/E-113. The latter Examples explain what a confirmed diagnosis might require; they do not establish one for F008.

**R-028 — Separate symptom domains.** Match an IPSS list → its stated voiding and storage groupings. Example: “Scale S includes weak stream and urgency” → “Scale S lists weak stream among voiding items and urgency among storage items,” if those classifications are given. Origin: D-018/D-019, E-012. Total score improvement alone does not create subscore findings.

**R-029 — Preserve the assay stimulus.** Match `[drug] altered contraction after [stimulus]` → `under [stimulus], [drug] altered measured contraction`. Example: “A increased electrically evoked tension” → “Electrical stimulation elicited greater tension with A.” Origin: E-049/E-050/E-053. Carbachol maximum tension and pEC50 remain separate assays or measures.

**R-030 — Keep component, program, and teaching method distinct.** Match `[program] taught [action] with [method]` → `[program] included [action], taught using [method]`. Example: “Therapy taught relaxation with biofeedback” → “Relaxation training was one component of the therapy, taught using biofeedback.” Origin: E-044/E-069/E-072. Do not equate PFPT, PFMT, and biofeedback.

**R-031 — Express steps in care.** Match `referred; scheduled; attended; completed` → four named stages with the local threshold for each. Example: “A was referred, booked, and visited once” → “A was referred, scheduled, and attended at least one visit”; completion remains unstated. Origin: E-046/E-140–E-142. Do not use attendance as completion.

**R-032 — Express performed behavior separately from confidence.** Match `[logs of exercises]` → `reported/recorded adherence`; match `[self-efficacy score]` → `confidence in performing exercises`. Example: “Participants logged exercises and rated confidence” → “Exercise adherence was logged. Confidence was rated separately.” Origin: E-117–E-121. A clinic visit is yet another measure.

**R-033 — Local definition of response versus remission.** Match `[response requires threshold A]; [remission requires threshold B]` → two separately named requirements, still worded as requirements. Example: “Response required a two-point drop; remission required a final score of at most two” → “A two-point drop was required for response; a final score of at most two was required for remission.” Only if the study defines a threshold as the complete criterion may you write that meeting it “met” or “qualified as” the outcome; keep any other stated conditions. Origin: E-159/E-207/E-210. Do not unify the short and expanded F021 definitions by guess. *Revised P2: the P1 example turned a necessary condition into a sufficient one [Astra correction 3].*

**R-034 — Analysis population and missingness.** Match `[ITT or PP population] analyzed using [missing-data rule]` → separate who was analyzed from how missing outcomes were handled. Example: “ITT used baseline carry-forward” → “The study's ITT population was analyzed using baseline-observation-carried-forward for missing outcomes.” Origin: E-195–E-199. Use that paper's stated ITT definition.

### Condition, time, and contrast

**R-035 — Necessary condition.** Match `[outcome] occurs only if [condition]` → `[condition] is necessary for [outcome]` within the stated scope. Example: “Improvement occurs only if the threshold is crossed” → “Crossing the threshold is necessary for improvement in this model.” Origin: E-230/E-275; generalized. This says nothing about whether the condition is sufficient.

**R-036 — Sufficient condition, where actually asserted.** Match `if [condition], [outcome]` → `[condition] is sufficient for [outcome]` only when the source clearly asserts that implication in its stated scope. Example: “Under rule S, if the score is zero, classify as remission” → “Under rule S, a zero score suffices for remission classification.” Origin: E-121/E-159; generalized. Ordinary predictions containing “if” can keep their original conditional wording.

**R-037 — Preserve nested conditions.** Match `[benefit] when [A] but only if [B]` → `[A] defines the setting; [B] is necessary for the benefit there`. Example: “Within group G, response occurs only if A precedes B” → “In group G, A preceding B is necessary for response.” Origin: E-101/E-230/E-275; generalized. Retain which condition narrows the population and which narrows the outcome.

**R-038 — Render a prospective prevention claim.** Match `[agent] prevented [new deterioration]` → `[new deterioration] was prevented under [agent]` with population and observation window. Example: “A prevented a fall in pressure” → “Under A, the fall in pressure was prevented.” Origin: E-028/E-251/E-253. “Prevented” must not become “partly reduced” without an actual magnitude or qualification.

**R-039 — Render partial attenuation.** Match `[agent] reduced but did not eliminate [effect]` → `[effect] was attenuated, not eliminated, under [agent]`. Example: “A partly reduced the increase in X” → “With A, the increase in X was smaller but still occurred.” Origin: E-271; generalized. Use only where persistence of an increase is actually established; otherwise say merely “attenuated.”

**R-040 — Render reversal of an established state.** Match `[change] existed before [agent] and later declined` → `[agent] was followed by a decrease in pre-existing [change]` with the reported causal strength. Example: “Fibrosis was present, then fell with A” → “Pre-existing fibrosis decreased during treatment with A.” Origin: E-084/E-145/E-272; generalized. A prevention study cannot fill this rule's baseline slot.

**R-041 — State incomplete recovery.** Match `[outcome] improved but did not normalize` → `improved from baseline, yet remained outside [stated reference]`. Example: “Function improved but remained impaired” → “Function improved from baseline but remained impaired.” Origin: E-135/E-221/E-272. Do not turn partial improvement into no improvement.

**R-042 — Separate relief from restoration.** Match `[outlet intervention] changed [voiding measure]` → name the outlet or voiding change; add detrusor restoration only if measured. Example: “After surgery, residual volume fell” → “Residual volume fell after the outlet procedure.” Origin: D-063, E-274–E-278; generalized. This rule does not infer a cause for the change beyond what the source asserts.

**R-043 — Early and late administration branches.** Match `[early administration → effect A]; [late administration → effect B]` → two timed claims, each with its stage and outcome. Example: “A prevented X before challenge but had no detected effect after challenge” → “Before challenge, A prevented X. After challenge, no effect of A on X was detected.” Origin: E-101/E-102/E-230/E-231. Keep route and model if either differs.

**R-044 — Pretreatment relative to an insult.** Match `[agent] given [interval] before [event]` → `pretreatment with [agent] at [interval] before [event]`. Example: “A was given 60 minutes before stimulation” → “A was given as pretreatment 60 minutes before stimulation.” Origin: E-101/E-212. Do not reclassify it as therapy for established injury.

**R-045 — Treatment after an insult.** Match `[agent] given [interval] after [event]` → `post-event treatment beginning [interval] after [event]`. Example: “A was given four hours after injury” → “A was administered as post-injury treatment four hours after the injury.” Origin: E-234/E-237/E-262. If onset is unknown, keep “after” without inventing an interval.

**R-046 — Time-limited effect versus later effect.** Match `[early measurement null] but [late measurement positive]` → two time-specific results. Example: “A did not change X at 20 minutes but reduced X at six hours” → “No change in X was observed at 20 minutes; X was lower with A at six hours.” Origin: E-185–E-190. A time window does not imply the same assay at both times unless supplied.

**R-047 — Persistence after stopping.** Match `[state] remained [interval] after [agent] ceased` → `at [interval] following cessation, [state] persisted`. Example: “Suppression remained five days after A stopped” → “Suppression was still present five days after stopping A.” Origin: E-098/E-187/E-190. Do not invent uninterrupted measurements throughout that interval.

**R-048 — Post-withdrawal rebound.** Match `[measure] rose after stopping [agent]` → `after [agent] stopped, [measure] increased [by reported amount and time]`. Example: “X increased at 10% per year after A stopped” → “Following cessation of A, X rose at 10% per year.” Origin: E-086–E-089. Treatment duration and tissue stay attached.

**R-049 — Change despite a competing change.** Match `[A] persisted despite improvement in [B]` → `although B improved, A persisted` with both time points. Example: “Inflammation remained despite lower BMI” → “Although BMI fell, inflammation remained.” Origin: E-221/E-279/E-280. No causal conclusion follows merely from the contrast.

**R-050 — Stage transition.** Match `[state A] progresses or may progress to [state B]` → retain the modal verb and the ordered stages. Example: “Chronic X may progress to Y” → “In the stated context, Y is a possible later stage of X.” Origin: E-223/E-250/E-251. Do not render possible progression as inevitable.

### Findings, explanation, and scope

**R-051 — Statistical non-detection.** Match `no statistically significant difference in [endpoint]` → `the study did not detect a statistically significant difference for [endpoint]`. Example: “A and B did not differ significantly in X” → “No statistically significant A–B difference in X was detected.” Origin: E-015/E-048/E-144/E-154. Keep estimate and uncertainty if present; the true effect is not established as zero.

**R-052 — No increase has its own direction.** Match `[measure] did not increase under [agent]` → `an increase in [measure] was not observed/reported under [agent]` at the stated time. Example: “X did not rise with A” → “No rise in X was observed with A.” Origin: E-096/E-226. This is not automatically a two-sided no-difference finding.

**R-053 — Nonsignificant directional trend.** Match `trend toward [direction] with [p or CI]` → `the estimate favored [direction], but the study did not report a statistically significant effect`. Example: “X trended lower with A (p=.06)” → “X trended lower with A (p=.06), without a reported significant effect.” Origin: E-163. Do not relabel as a demonstrated reduction.

**R-054 — Selective positive and null results.** Match `[agent] changed [X] without changing [Y]` → paired, separately named endpoints under the same conditions. Example: “A reduced TNF but left IL-6 unchanged” → “TNF fell under A; IL-6 was unchanged under the same conditions.” Origin: E-097/E-200/E-202/E-228. If the Y finding is only statistically nonsignificant, use R-051's wording for Y.

**R-055 — Biomarker versus function.** Match `[marker] changed while [clinical or functional result] did not` → parallel claims at each measured level. Example: “TNF fell, but symptoms were unchanged” → “TNF decreased. Symptoms did not change in the stated comparison.” Origin: E-131/E-225–E-229/E-236. Do not infer that the marker caused the functional result.

**R-056 — Distinguish message, protein, secretion, and effect.** Match `[agent] changed [mRNA or translation or secreted protein]` → name precisely that measured layer. Example: “A reduced TNF mRNA without changing translation” → “TNF message accumulation fell under A; translation efficiency did not change.” Origin: D-051/D-057, E-164/E-165/E-168/E-169. Use a measured protein claim only if supplied.

**R-057 — Attach the stimulus and compartment.** Match `[cells] produced [marker] after [stimulus]` → `after [stimulus], [cell type] produced [marker]` under the stated assay. Example: “After bacterial stimulation, cells produced more IL-6” → “Bacterial stimulation was followed by greater IL-6 production in those cells.” Origin: E-097/E-286. Do not silently translate stimulated capacity into circulating concentration.

**R-058 — Split circulating from cell-culture markers.** Match `[blood marker] changed and [stimulated-cell product] changed` → two explicitly located findings. Example: “Blood IL-6 rose; stimulated monocytes produced more IL-8” → “Circulating IL-6 rose. Stimulated monocytes produced more IL-8.” Origin: E-279/E-285/E-286/E-290/E-291. Neither is automatically a clinical immune disorder.

**R-059 — Preserve the anatomical vascular measure.** Match `[agent] changed [flow/resistance/reactivity/congestion] in [organ]` → keep organ, measure, route, and comparator. Example: “A lowered renal resistance during bacteremia” → “During bacteremia, renal vascular resistance was lower with A.” Origin: E-090–E-094/E-263–E-268. Cerebral flow, renal flow, and bladder perfusion are distinct outcomes.

**R-060 — Compare parent drug and metabolites separately.** Match `[parent, M1, M4, M5]` plus `[Tpeak/AUC/Cmax]` → one analyte–metric comparison per clause. Example: “M5 AUC rose; parent AUC did not change” → “M5 exposure rose. Parent-drug exposure remained unchanged in the stated comparison.” Origin: E-107–E-112. If parent AUC instead rose nonsignificantly, preserve that actual direction and significance.

**R-061 — Keep study population and model visible.** Match `[agent] affected [outcome] in [species/model/cohort]` → `in [named model/cohort], [agent] affected [named outcome]`. Example: “A reduced fibrosis in obstructed rats” → “In rats with induced obstruction, A reduced fibrosis.” Origin: E-026/E-058/E-122/E-245/E-267. Do not export that efficacy claim to a different organ or population.

**R-062 — Retain secondary attribution.** Match `[source] says [earlier author] found [claim]` → `[source] reports [earlier author's finding]`. Example: “A review says Lee found X” → “The review reports Lee's finding of X.” Origin: E-078/E-079/E-273. This wording does not pretend the cited study was supplied directly.

**R-063 — Preserve tentative language.** Match `may/could/suggests/appears to [claim]` → a plain phrase with the same degree of uncertainty and named speaker. Example: “The authors suggest X could partly explain Y” → “The authors propose X as a possible partial explanation of Y.” Origin: E-093/E-105/E-130/E-170/E-280/E-287. Do not upgrade a possibility to a demonstrated cause.

**R-064 — Separate observation and interpretation.** Match `[authors] attribute [observation] to [mechanism]` → `[observation] was reported; [authors] proposed [mechanism] as an explanation`, where the explanation is indeed proposed. Example: “The authors attribute higher flow to vasodilation” → “Higher flow was reported. The authors attributed it to vasodilation.” Origin: E-204/E-264/E-265/E-287. If the input asserts a demonstrated mechanism, retain its actual wording rather than automatically weakening it.

**R-065 — Separate review judgment from null result.** Match `evidence does not support [practice]` → `the review concludes that available evidence does not support [practice]`. Example: “Evidence does not support routine A” → “The review concludes that available evidence does not support routine A.” Origin: E-148–E-151. A null study is expressed by R-051; neither becomes “the evidence is merely insufficient” by default.

**R-066 — State a proposed subgroup without promoting it.** Match `[possible effect] among [baseline subgroup]` → `possible effect in the subgroup defined by [baseline trait]`. Example: “A may help those with high X at baseline” → “The proposed responders are people with high baseline X; benefit remains possible.” Origin: E-095/E-096/E-130. Do not create an established PTX-responsive urinary phenotype.

**R-067 — Separate remission from post-remission phenomena.** Match `[biochemical remission] plus [marker/symptom/diagnosis]` → one remission claim plus one independently qualified measurement or diagnosis. Example: “After remission, IL-6 rose and fatigue occurred” → “Biochemical remission occurred. Afterward, IL-6 rose and fatigue was reported.” Origin: D-061/D-064, E-255/E-279/E-281/E-282/E-286/E-288. Withdrawal, immune disease, and measured inflammation are not blanket synonyms.

**R-068 — Handle a contested diagnostic label.** Match `[source] uses [term] despite conflicting definitions elsewhere` → `[source] uses the exact term for its stated features`. Example: “The paper called X non-neurogenic DSD” → “The paper used ‘non-neurogenic DSD’ for X, with its own stated features.” Origin: D-012, E-038/E-039/E-139, DR-058. Await a direct nomenclature comparison before adopting a universal alias.

### Dream-grown ingredients ready before the requested sentences arrive

**R-069 — Compare two symptom domains.** Match `[intervention] improved [domain A] more than [domain B]` → `improvement with [intervention] was greater in [domain A] than in [domain B]`. Example: “A improved voiding more than storage symptoms” → “Improvement with A was greater for voiding than for storage symptoms.” Origin: E-012 and DR-041/DR-042; **dream-inspired**. Use only when both domain results and their comparison are actually present.

**R-070 — State separate domain effects.** Match `[A] changed [voiding score] by [x] and [storage score] by [y]` → two domain-specific changes. Example: “A lowered voiding score by 3 and storage score by 1” → “With A, the voiding score fell 3 points; the storage score fell 1 point.” Origin: E-012 and DR-041/DR-042; dream-inspired. Unlike R-069, no claim of a tested difference between domains is added.

**R-071 — Distinguish washout from failed therapy.** Match `[prior agent] was stopped before enrollment` → `the agent was discontinued before enrollment`; match `did not work before enrollment` → `the agent had failed before enrollment`. Example: “Drug X was stopped two weeks before baseline” → “Participants discontinued drug X two weeks before baseline.” Origin: E-007/E-125/E-181, DR-040; dream-inspired distinction. Prior failure is not inferred from cessation.

**R-072 — Compare the currently missing volume outcome.** Match `[A] versus [B] on [voided volume] with [estimate/test]` → `voided volume [direction and estimate] with A versus B [reported uncertainty]`. Example: “A had 30 mL greater voided volume than B (95% CI 5–55 mL)” → “Voided volume was 30 mL higher with A than B (95% CI 5–55 mL).” Origin: E-015/E-016, DR-043; dream-inspired. A within-arm null cannot fill a between-arm estimate.

**R-073 — Sequence a measured recovery series.** Match `[baseline function] → [intervention] → [function at t1,t2]` → a timed baseline and subsequent measured functions, each named. Example: “Contractility index was 60 before outlet relief, 80 at one month after relief, and 90 at six months” → “After outlet relief, the contractility index rose from 60 at baseline to 80 at one month and 90 at six months.” Origin: E-272–E-278, DR-030; dream-inspired. This is an invented example, not a P7 human series. Symptom or flow changes alone do not fill contractility slots.

**R-074 — Express persistence despite outlet correction.** Match `[outlet measure] improved while [detrusor measure] remained impaired` → separate the two post-intervention outcomes. Example: “Resistance fell after surgery, but contraction strength stayed low” → “After surgery, outlet resistance fell. Detrusor contraction strength remained low.” Origin: E-272/E-274/E-276, DR-030; dream-inspired. Keep species or population supplied by the actual input.

**R-075 — Conditional diagnosis once a test is specified.** Match `[cohort] had [test-defined condition] under [criterion]` → `[cohort] met [source-specific criterion] for [condition]`. Example: “All participants met the study's pressure-flow BOO criterion” → “All participants had BOO as defined by that study's pressure-flow criterion.” Origin: E-009/E-023/E-030, DR-039; dream-inspired. Until F008's test status is supplied, use its actual clinical enrollment wording via R-027.

**R-076 — Describe a correction to an uncertain denominator.** Match `[document] corrects [denominator old] to [denominator new]` → `[corrected denominator] is the denominator for [specified stage and rate]`. Example: “A correction says 74 were scheduled, 52 attended” → “Under the correction, 52 of 74 scheduled people attended.” Origin: E-046, DR-045; dream-inspired. This illustrates the grammar only; it does not assert that a P023 correction exists or that 74 is right.

**R-077 — Retain route-specific disagreement.** Match `[route A] produced [finding] while [route B] did not` → two routes with their doses and the same measured outcome. Example: “IV A reduced X, but oral A did not” → “Intravenous A reduced X. Oral A did not reduce X in the stated comparison.” Origin: E-267/E-268; generalized from the Dictionary's administration distinctions. If timing or dose also differs, name both before attributing the difference to route.

**R-078 — Contrast normal and elevated baselines.** Match `[agent] affected [high-baseline group] but not [normal-baseline group]` → two subgroup-specific outcomes with the same measure. Example: “A lowered X only when starting X was high” → “A lowered X in the high-baseline group. No lowering was reported in the normal-baseline group.” Origin: E-095/E-096/E-130; generalized/dream-inspired. Preserve how the groups were defined and what counted as an effect.

### Hypothesis-statement constructions [added P2, from the P8 hypothesis pass]

**R-079 — Keep a concession attached to its claim.** Match `[claim], whether or not [condition]` or `[claim] even if [condition]` → the claim followed by the concession, with nothing moved between them. Example [invented]: “The premises suffice to specify the trial, whether or not every link is resolved” → “The premises suffice to specify the trial. This holds whether or not every link is resolved.” Origin: header A1-H1 wording; generalized. Never turn the concession into a claim that links *are* unresolved, or that they are resolved.

**R-080 — Keep an exclusion's scope.** Match `[X] defeats [A], not merely [B]` or `[X] affects [A] rather than [B]` → `[X] defeats [A]. Defeating only [B] would not suffice.` Use the second sentence only when the input states the contrast. Example [invented]: “The failure defeats the whole rationale, not merely one route” → “The failure defeats the whole rationale. Defeating one route alone would not suffice.” Origin: header A1-H2 wording; generalized. Do not drop “not merely”; it sets the strength of the claim.

**R-081 — An inability to distinguish is not an equivalence.** Match `[evidence] cannot distinguish [A] from [B]` → `The [evidence] does not distinguish [A] from [B].` Keep both options named. Example [invented]: “The data cannot distinguish a functional effect from structural recovery” → “The data do not distinguish a functional effect from structural recovery.” Origin: header A1-H3 and A2-H3 wording; E-015/E-016 null forms. Never write “A and B are the same” or “neither occurred”.

**R-082 — Keep the agent that selects a homonym's sense.** Match `[agent] monotherapy` or `monotherapy with [agent]` → keep the agent word next to “monotherapy”, even when the sentence is split. Example [invented]: “PTX was not tested as monotherapy, unlike tamsulosin” → “PTX was not tested as monotherapy. Tamsulosin was given as monotherapy.” Origin: D-065/D-066 sense split, E-018, E-296. A split that leaves a bare “monotherapy” loses the information the transcoder needs to bind it.

## Dream inputs for Mr. Dictionary

These are forecasts of useful input, not scientific claims. The corresponding grammar already exists where possible; a request remains open to refine applicability or fill an actual result. Keep each CRD-ID stable on re-ingestion.

1. **CRD-001 — F008 cohort diagnosis.** *[P2: largely fulfilled by E-298 + E-009. F008 used clinical diagnosis plus ultrasound/uroflowmetry screening; no pressure-flow sentence exists. Use the R-027 wording, not R-075.]* Desired capability: select the exact clinical versus pressure-flow-confirmed cohort wording in R-027/R-075. Ideal input: F008 protocol, results, or linked appendix stating the test and criteria actually applied to enrolled men. Change if found: activate a source-specific confirmed-BOO variant or keep the clinical BPH/LUTS label. Links E-009/E-023/E-030, DR-039.
2. **CRD-002 — F008 prior treatment.** Desired capability: choose the appropriate R-071 history phrase. Ideal input: actual cohort history distinguishing lack of prior exposure, prior alpha-blocker failure, and drug washout, with time. Change if found: fill a cohort-specific treatment-history sentence. Links E-007/E-125/E-181, DR-040.
3. **CRD-003 — F008 voiding and storage subscores.** *[P2: partly fulfilled. E-294 gives between-group significance for both subscores. Magnitudes exist only in WRONG-verdict repaired FRDs, held as seeds.]* Desired capability: apply R-069/R-070 to the actual trial. Ideal input: arm-specific subscore levels or changes with time, comparison, and uncertainty for each domain. Change if found: express each result; compare domains only if a comparison is supported. Links E-012/E-018, DR-041/DR-042.
4. **CRD-004 — F008 voided volume between arms.** *[P2: fulfilled by E-295 — between-group absolute change 0.80 vs +1.34 mL, p = .22, separate from the within-group nulls.]* Desired capability: apply R-072. Ideal input: direct between-arm estimate, units, time, and test or CI, alongside within-arm results. Change if found: fill the comparison without equating it to either within-arm null. Links E-015/E-016, DR-043.
5. **CRD-005 — Human detrusor recovery after relief.** Desired capability: use R-042/R-073/R-074 to distinguish postoperative emptying from measured muscle recovery. Ideal input: directly supplied serial human urodynamics with baseline and timed post-relief contractility, outlet measure, and outcomes; a separate PTX-withdrawal branch would require its own exposure history. Change if found: fill a timed recovery or persistence pattern. Links E-272–E-278, DR-030.
6. **CRD-006 — Scheduled denominator.** Desired capability: compute and phrase the referral-to-attendance conversion in R-020/R-031/R-076. Ideal input: P023 correction or source explanation reconciling 73 versus 74 scheduled people and the stated attended count. Change if found: use the corrected source denominator for the appropriate stage. Links E-046, DR-045.
7. **CRD-007 — DSD terminology.** Desired capability: choose precise, source-scoped names for voluntary dysfunction and neurological dyssynergia under R-068. Ideal input: P015 author clarification, erratum, or explicit nomenclature discussion addressing “non-neurogenic DSD” and the voluntary/involuntary features. Change if found: add a scoped alias or preserve two distinct senses with a clear selector. Links D-012, E-038/E-039/E-139, DR-058.
8. **CRD-008 — Provenance of drug shorthand.** Desired capability: expand the agent abbreviations under R-001/R-002 without accidental equivalence. Ideal input: each relevant original source's own definition of POF, PTF, PTXF, Ptx, and any distinct formulation. Change if found: add source-scoped expansion variants. Links E-107/E-230/E-245.
9. **CRD-009 — ITT and F021 response criteria.** Desired capability: apply R-023/R-024/R-033/R-034 with the correct logical form. Ideal input: complete F021 response and remission definition connecting short E-207 to compound E-210, plus original allocation/missingness description wherever ITT differs across studies. Change if found: specify criterion grouping and analysis population by source. Links E-195–E-199/E-207/E-210.
10. **CRD-010 — Combination versus interaction.** Desired capability: phrase the stronger claim that a combination has an interaction, if tested, in addition to R-003–R-005's arm and incremental result patterns. Ideal input: full factorial contrast and explicitly reported interaction model or a source's operational definition of synergy. Change if found: add a tested-interaction rule; if only attribution exists, retain it as an attributed claim. Links E-083/E-085/E-191–E-193.
11. **CRD-011 — Peripheral mechanism paired with human voiding.** Desired capability: put R-029/R-055/R-059/R-061 in one clearly linked account. Ideal input: the same study measuring a named PTX-related peripheral mechanism and a human voiding endpoint at stated times and under an interpretable comparator. Change if found: add a paired-measurement pattern while keeping causal language at the level the study uses. Links E-049/E-050/E-236/E-265.
12. **CRD-012 — Post-remission immune phases.** Desired capability: refine R-057/R-058/R-067 across biochemical remission, hypocortisolism, stimulated cytokines, circulating markers, withdrawal, and overt immune disease. Ideal input: explicit group definitions, timing, and compartment-specific measurements that relate or distinguish these phenomena. Change if found: add applicable time- and group-specific constructions. Links E-255/E-279/E-281/E-286/E-288.
13. **CRD-013 — Shy bladder in the cohort sense.** Desired capability: choose between the test-anxiety sense [D-035] and situational paruresis [W-071] when a hypothesis or witness says “shy bladder”. Ideal input: a Rank A/B sentence using “shy bladder” or “paruresis” for public-setting initiation difficulty. Change if found: a scoped alias or a second entry with a selector. Links D-035, W-071, DR-080.
14. **CRD-014 — Exposure reachability wording.** Desired capability: phrase “clinically attainable exposure” claims as dose → measured level → effect threshold. Ideal input: a source sentence comparing an effect's concentration with oral plasma levels. Change if found: a rule for reachability comparisons. Links W-069, DR-078, D-068.

## This pass [P1]

**New artifact.** Created a fresh standalone rulebook, R-001–R-078, from P7 only, plus CRD-001–CRD-012. No earlier canonicalizer rule IDs, dreams, rules, or fragment were used as an input or carried forward. Similar constructions can appear because P7 itself contains the relevant language. The inventory contains multiple options for comparisons, thresholds, time, study stages, measured endpoints, source attribution, and anticipated findings. A rule need not have been printed in the literature; its origin field states what motivated its design.

**Coverage.** I surveyed P7's inherited and appended Dictionary material, including its open DR-030, DR-039–DR-043, DR-045, and DR-058. The rule families draw on D-001–D-029, D-031–D-064, and Examples spanning E-001–E-292 where actually present (E-166 and E-206 are unused IDs). Representative sections include F008's enrollment, arms, and endpoints (E-001–E-020); obstruction, detrusor, PFPT, and rat bladder function (E-021–E-081); timing, pharmacokinetics, and inflammation (E-082–E-157); definitions and selective findings (E-158–E-224); and renal, post-relief, and endocrine material (E-225–E-292). This is coverage of language in the supplied Dictionary, not verification of those sources.

**Application checks on P7 sentences.** The quotes below are copied from P7. The renderings are my proposed wording, not source quotations; each retains the propositions in its quoted input.

> **E-013 (F008 line 121):** “Tables 2–4 demonstrate that the increase in maximum urinary flow rate and decreasing residual volume by combination therapy is significantly higher (Q<sub>max</sub>: +42.5%, PVR: –42.6%) compared to monotherapy (Q<sub>max</sub>: +25.1%, PVR: –26.1%) (*p* < .001).”

Using R-003/R-015/R-016/R-017: “In F008, the PTX-plus-tamsulosin combination produced a greater increase in maximum flow rate than tamsulosin alone (+42.5% versus +25.1%) and a greater decrease in post-void residual volume (−42.6% versus −26.1%); the source reports *p* < .001 for this comparison.” The arm names are supplied elsewhere in P7's linked F008 Examples E-001/E-002, not in E-013 alone; use the generic arm labels if that linked context is unavailable.

> **E-275 (P026 line 85):** “A patient with detrusor underactivity and BOO/BPO will only improve his voiding function if he moves above the 25th percentile after surgery (Fig. 3C).”

Using R-035/R-042: “For a patient with detrusor underactivity and BOO/BPO in P026's nomogram, moving above the 25th percentile after surgery is presented as a necessary condition for improved voiding function (Fig. 3C).” It does not state that crossing the percentile guarantees improvement or that detrusor contractility recovered.

**Unresolved boundaries.** D-012 has a live DSD naming conflict. E-074's “It” lacks its antecedent in the retained sentence. F008's diagnostic, history, and subscore text is incomplete; P023 has the 73/74 scheduled-count conflict; F021 has short and compound response descriptions. The dream rules are grammatically available even when their actual study results remain unknown. A future transcoder run on unseen sentences is needed to judge retrieval, rule selection, and whether the rule variants add practical value.

## This pass [P2]

- **Corrections.** Revised R-019, R-023 and R-033 using Astra's three corrections. Each rule keeps its ID and records the reason inline. The rules themselves were sound; only their invented examples added meaning.
- **New rules.** R-079 to R-082, for constructions in the A1 hypothesis statements [concession, exclusion scope, non-equivalence] and the new monotherapy sense split.
- **Dream inputs.**
  - CRD-001 and CRD-004 are fulfilled.
  - CRD-003 is partly fulfilled.
  - CRD-013 and CRD-014 are new.
- **Not done.** The rest of the rulebook was not re-surveyed against the 19 new P8 Examples beyond these needs. That is a job for a later full pass.
