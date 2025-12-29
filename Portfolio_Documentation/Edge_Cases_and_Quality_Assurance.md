### \# Edge Cases \& Quality Assurance in Medical Imaging Annotation



#### \## Overview

This document details the challenging scenarios encountered across all five annotation projects and the quality assurance measures implemented to ensure clinical accuracy.



---



\## Common Edge Cases Across All Pathologies



\### 1. Indistinct Pathology Borders



\*\*Problem Statement:\*\*

Many lung pathologies do not have sharp, well-defined borders. Opacities often gradually transition into normal lung tissue, making it impossible to define a precise boundary.



\*\*Affected Pathologies:\*\*

\- Bronchopneumonia (most common)

\- Lobar pneumonia (when consolidation is incomplete)

\- Pleural effusion (when small or layering)



\*\*Solution Implemented: Straight-Line Approximation\*\*



When faced with gradual opacity transitions:

1\. Identified the zone where opacity transitions from "clearly abnormal" to "possibly normal"

2\. Drew a \*\*straight line\*\* through this transition zone as an approximation

3\. Line placement based on clinical judgment: where increased opacity becomes subtle enough to represent normal vascular markings

4\. Documented rationale in annotation comments



\*\*Clinical Justification:\*\*

\- In real clinical practice, radiologists also apply judgment to these indistinct areas

\- For AI training, a consistent approximation method is better than inconsistent guessing

\- Allows model to learn that some pathology borders are inherently uncertain



\*\*Example:\*\*

\*Bronchopneumonia with patchy infiltrates that gradually blend into increased broncho vascular markings - straight line drawn where opacity intensity decreased by ~50% from peak density.\*



---



\### 2. Overlapping Anatomical Structures



\*\*Problem Statement:\*\* When consolidation extends behind the heart, mediastinum, or diaphragm, you cannot visualize where the pathology ends because these dense structures block the view of the lung tissue behind them. However, you can infer the consolidation extends into these areas through the \*\*silhouette sign\*\* - loss of the normal anatomic border.



\*\*Affected Pathologies:\*\*

\- Lobar pneumonia (extending behind heart or mediastinum) 

\- Bronchopneumonia (involving lower lobes behind diaphragm) 

\- Pleural effusion (layering along diaphragm)





\*\*Solution Implemented:\*\*

When consolidation clearly extended behind an opaque structure: 

1\. \*\*Traced the visible anterior portion\*\* of the consolidation using polygon segmentation 

2\. \*\*At the point where the heart/mediastinum/diaphragm obscured further visualization:\*\* - Drew a \*\*straight line\*\* along the anatomical border (e.g., along the right heart border) 

3\. \*\*Completed the polygon\*\* using this straight-line approximation to close the shape 

4\. \*\*Documented in comments:\*\* "Consolidation extends posteriorly behind \[structure]; straight-line approximation used along \[anatomical border]"





\*\*Clinical Reasoning:\*\*

\- The silhouette sign indicates the consolidation DOES extend to that border 

\- A lateral chest X-ray would show the posterior extent (but was not available in this dataset) 

\- Using the anatomical border as a straight-line boundary is a reasonable approximation for 2D PA view annotation 

\- This approach is consistent and reproducible across cases



---



\### 3. Differentiating Similar-Appearing Pathologies



\#### Case Study: Pericardial Effusion vs Cardiomegaly



\*\*Challenge:\*\*

Both conditions enlarge the cardiac silhouette on chest X-ray. Differentiation requires:

\- \*\*Pericardial effusion:\*\* Fluid in pericardial sac, often with "water bottle" heart shape, sharp borders

\- \*\*Cardiomegaly:\*\* Enlarged heart muscle, may have indistinct borders, often with pulmonary vascular changes



\*\*Differentiation Criteria Applied:\*\*



| Feature | Pericardial Effusion | Cardiomegaly |

|---------|---------------------|--------------|

| \*\*Cardiac shape\*\* | "Water bottle" or globular | Enlarged but maintains normal contour |

| \*\*Border sharpness\*\* | Very sharp, well-defined | May be indistinct |

| \*\*Associated findings\*\* | Narrow vascular pedicle | Pulmonary vascular congestion |

| \*\*Epicardial fat pad sign\*\* | Separated from cardiac silhouette | Not present |





---



\### 4. Partial or Atypical Presentations



\*\*Problem Statement:\*\*

Not all pathologies present in their "textbook" form. Partial involvement, early-stage disease, or post-treatment changes create annotation challenges.



\*\*Examples Encountered:\*\*



\*\*Partial Lobar Pneumonia:\*\*

\- Only anterior segment of lobe consolidated, not entire lobe

\- \*\*Solution:\*\* Annotated consolidated portion only, labeled as "lobar\_pneumonia\_partial"



\*\*Minimal Apical Pneumothorax:\*\*

\- Barely visible pleural line at extreme apex

\- \*\*Solution:\*\* Annotated if confident in identification, flagged as "small" size, documented uncertainty if present



---



\## Quality Assurance Measures Implemented



\### 1. Systematic Annotation Protocol



\*\*Checklist used for every image:\*\*

\- \[ ] Image quality adequate for annotation (exposure, positioning, inspiration)

\- \[ ] Anatomical landmarks identified (for orientation)

\- \[ ] Pathology identified and characterized

\- \[ ] Appropriate annotation tool selected (polygon, bounding box, classification)

\- \[ ] Borders traced accurately (or straight-line approximation applied)

\- \[ ] Additional features documented (air bronchograms, etc.)

\- \[ ] Self-review completed before moving to next image



---



\### 2. Consistency Checks



\*\*After completing each pathology set (10 images):\*\*

1\. Reviewed all 10 annotations side-by-side

2\. Checked for consistency in:

&nbsp;  - Labeling conventions

&nbsp;  - Border definition approach

&nbsp;  - Use of additional tags

&nbsp;  - Straight-line approximation application

3\. Made adjustments if inconsistencies identified



---



\### 3. Clinical Validation



\*\*External review by licensed radiographer:\*\*

\- Provided sample annotations without my interpretations

\- Radiographer assessed accuracy of pathology identification and border tracing

\- Feedback incorporated into remaining annotations

\- \*\*Result:\*\* 95%+ agreement on pathology identification and annotation accuracy



---



\### 4. Documentation of Uncertainty



\*\*When uncertain about any aspect of annotation:\*\*

\- Did NOT make assumptions

\- Documented uncertainty in comments field

\- Flagged for clinical review if available

\- In real-world setting, would request additional views or imaging



\*\*Examples of documented uncertainty:\*\*

&nbsp;- "Pleural line vs skin fold - recommend expiratory view for confirmation"



---



###### \### 5. Error Analysis



\*\*Common errors I caught during self-review:\*\*

1. \*\*Incomplete pathology capture\*\* - missed subtle findings

&nbsp;  - \*Solution:\* Systematic scan of entire image before finalizing annotation

2. \*\*Over-annotation\*\* - annotating normal variants as pathology

&nbsp;  - \*Solution:\* Applied clinical judgment, when in doubt consulted radiographer



---



##### \## Lessons Learned for AI Model Training



\### 1. Ground Truth is Sometimes Inherently Uncertain

\- Not all clinical data has perfectly defined labels

\- AI models should potentially be trained to output confidence intervals, not just binary classifications

\- Annotation uncertainty should be preserved in training data (e.g., "uncertain" flag)



\### 2. Contextual Information Matters

\- Clinical history, comparison with prior studies, and patient demographics would significantly improve annotation accuracy

\- AI models that incorporate clinical context will likely outperform image-only models



\### 3. Edge Cases Are Common, Not Exceptions

\- At least 30-40% of cases in this dataset involved edge case scenarios

\- AI models must be trained on diverse presentations, not just "textbook" examples

\- Robust models need training data that includes ambiguous, atypical, and challenging cases



\### 4. Human Expert Review is Essential

\- Even with strong clinical background, external validation improved annotation quality

\- For high-stakes medical AI, multi-annotator agreement and expert adjudication are critical



---



###### \## Recommendations for Future Annotation Projects



1\. \*\*Use multi-pass annotation:\*\*

&nbsp;  - First pass: Identify and mark all pathologies

&nbsp;  - Second pass: Refine borders and apply tags

&nbsp;  - Third pass: Quality check and consistency review



2\. \*\*Incorporate clinical context when available:\*\*

&nbsp;  - Patient age, symptoms, clinical history

&nbsp;  - Comparison with prior imaging

&nbsp;  - Laboratory values



3\. \*\*Implement inter-annotator agreement measurement:\*\*

&nbsp;  - Have 10-20% of cases annotated by multiple annotators

&nbsp;  - Calculate Cohen's kappa or F1 scores

&nbsp;  - Use discrepancies to refine annotation guidelines



4\. \*\*Document edge cases systematically:\*\*

&nbsp;  - Create edge case library for training new annotators

&nbsp;  - Use challenging cases for annotator competency assessment



5\. \*\*Develop pathology-specific guidelines:\*\*

&nbsp;  - Each pathology may require unique annotation approach

&nbsp;  - Guidelines should address common edge cases



---



\## Conclusion



Medical imaging annotation is as much art as science. Clinical judgment, systematic methodology, and quality assurance processes are essential for creating high-quality training data for healthcare AI.



This portfolio demonstrates not just technical annotation skills, but clinical reasoning and attention to the nuances that make medical data challenging and valuable for AI development.



---



\*\*Document created:\*\* \[December, 2025]  

\*\*Author:\*\* Anita Aigbomodion, RN  

\*\*Purpose:\*\* Portfolio documentation and quality assurance demonstration

