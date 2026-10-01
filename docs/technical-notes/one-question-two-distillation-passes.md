
# One question, two passes of distillation

From hypothesis-relevant novelty to traceable crux evidence

![Flowchart of the distillation process from ACH frame to primary source.](52218820ae0a5a10bb2d604859f803e7_img.jpg)

> Figure pending re-export. The raster file above is the same file referenced by Technical Specification 1 and does not depict this two-pass flow; it also shows the superseded order in which witness creation preceded the language tools. The diagram source below is correct, and this document needs its own image file.

```
graph TD; A["Human-specified ACH frame  
Competing hypotheses + investigation objective"] --> B["Adaptive quest selects a high-value question  
Seek novel information relevant to the hypotheses"]; B --> C["Parent question + corpus → Archivist response  
First distillation pass: the question directs extraction from the corpus."]; C --> D["Query response → FRD-creation prompt → FRD"]; D --> E["FRD validated against its named primary source  
Validated FRD"]; E --> F["Custom dictionary built from validated FRDs"]; F --> G["Canonicalizer"]; G --> H["Transcoder"]; H --> I["Transcoded question  
Derived representation of the same question, same QID"]; B --> I; I --> J["Validated FRD + transcoded question → witness-creation prompt → Witness  
Second distillation pass: the transcoded question focuses the FRD into a witness."]; E --> J; J --> K["Transcoding of witnesses and hypothesis statements"]; H --> K; L["Extended hypothesis statements"] --> K; K --> M["Formalized witnesses + formalized hypothesis statements  
Shared contextual terminology and consistent syntax"]; M --> N["Deletion-minimal hypothesis coverage sets  
Retain compact sufficient witness groups"]; N --> O["Crux identification  
Focus on witnesses that distinguish competing hypotheses"]; O --> P["Crux witness"]; P --> Q["Parent FRD"]; Q --> R["Primary source"];
```

The flowchart illustrates a two-pass distillation process. It begins with a 'Human-specified ACH frame' (Competing hypotheses + investigation objective), which leads to an 'Adaptive quest' selecting a high-value question. This question is used in the first distillation pass to generate an 'Archivist response' from a corpus, resulting in a 'Query response', an 'FRD', and a 'Validated FRD'. The validated FRDs then produce a 'Custom dictionary', from which a 'Canonicalizer' and a 'Transcoder' are built. The transcoder converts the same parent question into a 'Transcoded question', a derived representation held under the same QID. In the second pass, the 'Validated FRD' and the 'Transcoded question' are used to create a 'Witness'. The witnesses, together with 'Extended hypothesis statements', pass through the same transcoder. The output is 'Formalized witnesses + formalized hypothesis statements', which are then processed into 'Deletion-minimal hypothesis coverage sets'. Finally, 'Crux identification' focuses on witnesses that distinguish competing hypotheses, leading to a 'Crux witness', 'Parent FRD', and 'Primary source'.

Flowchart of the distillation process from ACH frame to primary source.

Follow the retained provenance to inspect the source behind the distinguishing evidence.

*Signal = relevance to the ACH frame. Noise = irrelevance to that frame.*

*Formalization reduces ambiguity; crux identification remains subject to semantic review and practical evaluation.*
