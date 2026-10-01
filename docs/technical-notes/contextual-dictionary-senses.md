

# Why does one word need more than one dictionary entry?

A witness and a hypothesis can use the same word for two different things. If the run treats them as one term, unrelated claims will appear to match. So the unit of the dictionary is **not the word — it is each reviewed meaning of the word**, and a meaning becomes usable only once the corpus has shown it three separate times.

![Flowchart of the dictionary entry process](52218820ae0a5a10bb2d604859f803e7_img.jpg)

```
graph TD; A[Validated FRD claim text] --> B[Find recurring candidate words]; B --> C[Collect each occurrence with its sentence and context]; C --> D[Compare occurrences: do they use the word in the same sense?]; D --> E[Group occurrences by meaning  
Every pair within a group must pass review]; E --> F[Does this sense group have 3 distinct supporting sentences?]; F -- Yes --> G[Active dictionary entry  
WORD (context modifier)  
definition · examples · scope]; F -- No --> H[Held as provisional  
Not used in this run  
Its examples are preserved for later];
```

The flowchart illustrates the process of creating dictionary entries from validated FRD claim text. It starts with 'Validated FRD claim text', which leads to 'Find recurring candidate words'. This is followed by 'Collect each occurrence with its sentence and context', then 'Compare occurrences: do they use the word in the same sense?'. The next step is 'Group occurrences by meaning' (with a note: 'Every pair within a group must pass review'). A decision point asks 'Does this sense group have 3 distinct supporting sentences?'. If 'Yes', it results in an 'Active dictionary entry' for the 'WORD (context modifier)', including definition, examples, and scope. If 'No', it is 'Held as provisional', not used in this run, but its examples are preserved for later.

Flowchart of the dictionary entry process

**Worked example.** The word “control” appears in five distinct FRD sentences — but not in one sense.

| Reviewed meaning               | Sentences | Result                                                   |
|--------------------------------|-----------|----------------------------------------------------------|
| Experimental comparison group  | 3         | <b>Active entry</b><br>control (experimental comparison) |
| Authority over an organization | 2         | <b>Provisional</b><br>Insufficient examples              |

Five occurrences of the **word** do not supply three examples for **each meaning**. The requirement applies separately to every sense, so one spelling leaves this run with one usable entry and one held in reserve.

## **What this does not claim**

- The three-sentence requirement is this specification’s working rule, not a universal law of language.
- Ordinary-English frequency helps prioritize which words get reviewed. It does not determine their meanings or approve their entries.