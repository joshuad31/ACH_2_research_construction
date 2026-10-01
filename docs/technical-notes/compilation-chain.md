
# Complete compilation chain

Technical Disclosure 1 • Revised workflow

![A vertical flowchart showing a 15-step process for a 'Complete compilation chain'. Steps 1-8 are in white boxes, 9-14 are in light blue boxes, and step 15 is in a dark blue box. A feedback loop labeled 'Repeat quest rounds' connects step 5 back to step 4.](52218820ae0a5a10bb2d604859f803e7_img.jpg)

> Figure pending re-export. The raster file above still shows the superseded fourteen-step order in which witness creation preceded the dictionary, canonicalizer, and transcoder. The diagram source and step list below are correct.

```
graph TD; 1[1. Large corpus converted to Markdown] --> 2[2. Creation of corpus index]; 2 --> 3[3. Hypotheses identification and creation of ACH header with quest instructions]; 3 --> 4[4. Quest initiation with queries sent to archivist and responses returned for analysis]; 4 --> 5[5. Bayesian updating using ACH frame and prior context to elicit maximally novel responses]; 5 -- Repeat quest rounds --> 4; 5 --> 6[6. Quest termination once expected marginal utility of future novelty approaches zero]; 6 --> 7[7. Transformation of query responses into Facts References Database (FRD) entries]; 7 --> 8[8. FRD validation against primary sources creating validated FRD entries]; 8 --> 9[9. Creation of custom dictionary from validated FRD entries]; 9 --> 10[10. Creation of canonicalizer and transcoder]; 10 --> 11[11. Transcoding of the questions to be applied to validated FRD entries]; 11 --> 12[12. Question-guided witness creation]; 12 --> 13[13. Transcoding witnesses and extended ACH hypothesis statements]; 13 --> 14[14. Formation of deletion-minimal hypothesis coverage sets of witnesses]; 14 --> 15[15. Crux identification];
```

1. Large corpus converted to Markdown

2. Creation of corpus index

3. Hypotheses identification and creation of ACH header with quest instructions

4. Quest initiation with queries sent to archivist and responses returned for analysis

5. Bayesian updating using ACH frame and prior context to elicit maximally novel responses

6. Quest termination once expected marginal utility of future novelty approaches zero

7. Transformation of query responses into Facts References Database (FRD) entries

8. FRD validation against primary sources creating validated FRD entries

9. Creation of custom dictionary from validated FRD entries

10. Creation of canonicalizer and transcoder

11. Transcoding of the questions to be applied to validated FRD entries

12. Question-guided witness creation

13. Transcoding witnesses and extended ACH hypothesis statements

14. Formation of deletion-minimal hypothesis coverage sets of witnesses

15. Crux identification

A vertical flowchart showing a 15-step process for a 'Complete compilation chain'. Steps 1-8 are in white boxes, 9-14 are in light blue boxes, and step 15 is in a dark blue box. A feedback loop labeled 'Repeat quest rounds' connects step 5 back to step 4.

Original question and QID retained through witness creation. The transcoded question is saved as a derived representation of that same question under the same QID.  
Crux identification remains a proposed stage; practical validation is not established.
