

# Why “deletion-minimal” does not mean “smallest”

A coverage set is deletion-minimal when **no witness in it can be dropped** without leaving part of the hypothesis uncovered. That is a test each set either passes or fails — not a contest between sets. Several different sets can pass it on the same hypothesis, and the run keeps **every one of them**.

![Flowchart of the deletion-minimal process](52218820ae0a5a10bb2d604859f803e7_img.jpg)

```
graph TD; A1[Formalized witnesses] --> B1[Formalized hypothesis with identified coverage requirements]; A2[Formalized hypothesis with identified coverage requirements] --> B1; B1 --> C1[Semantic matching]; C1 --> D1[Record which witnesses — or assessed groups — fully cover which requirements]; D1 --> E1[Find witness sets that cover every required part of the hypothesis]; E1 --> F1[Try deleting each witness]; F1 --> G1{Does every single deletion break full coverage?}; G1 -- No --> H1[Remove a redundant witness and check again]; H1 --> F1; G1 -- Yes --> I1[Deletion-minimal coverage set Preserved alongside every other set that passes]; E1 --> J1[No full coverage Show the gaps for analyst review and further research];
```

The flowchart illustrates the process of identifying deletion-minimal coverage sets. It begins with 'Formalized witnesses' and a 'Formalized hypothesis with identified coverage requirements'. These lead to 'Semantic matching', followed by 'Record which witnesses — or assessed groups — fully cover which requirements'. The next step is 'Find witness sets that cover every required part of the hypothesis'. If full coverage is not achieved, the process leads to 'No full coverage: Show the gaps for analyst review and further research'. If full coverage is found, the process moves to 'Try deleting each witness'. A decision point asks 'Does every single deletion break full coverage?'. If 'No', a redundant witness is removed and the process loops back to 'Try deleting each witness'. If 'Yes', a 'Deletion-minimal coverage set' is identified, which is 'Preserved alongside every other set that passes'.

Flowchart of the deletion-minimal process

**Worked example.** A hypothesis has two requirements, A and B. Semantic review has already approved this coverage:

| Witness | Covers A | Covers B |
|---------|----------|----------|
| W1      | Yes      | —        |
| W2      | —        | Yes      |
| W3      | Yes      | Yes      |

**{ W1, W2 }**  
Drop either one and a requirement goes uncovered.  

---

**Deletion-minimal**

**{ W3 }**  
Drop its only witness and both requirements go uncovered.  

---

**Deletion-minimal & smallest**

**Both sets pass the test.** Only **{ W3 }** has minimum cardinality — the fewest witnesses. Discarding **{ W1, W2 }** for being larger would throw away a second, independently valid way the corpus covers the same hypothesis.

## **What this does not claim**

- Deletion-minimal does not mean smallest by witness count, uniquely valid, or strongest by evidentiary quality.
- Semantic matching establishes the coverage relationships. The deletion check only tests whether a member is dispensable — it does not judge the evidence.