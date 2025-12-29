### \# Project 1: Lobar Pneumonia Annotation



#### \## Overview

Annotated 10 chest X-ray images demonstrating lobar pneumonia patterns using polygon segmentation in Label Studio.



###### \## Pathology Description

\*\*Lobar pneumonia\*\* is characterized by consolidation (fluid-filled alveoli) affecting an entire lobe of the lung. It appears as a dense, homogeneous opacity on chest X-ray, often with:

\- Sharp borders at fissure lines

\- Air bronchograms (visible air-filled bronchi within the consolidation)

\- Silhouette sign (loss of normal anatomic borders)

\- Most commonly affects lower lobes



\*\*Common causative organism:\*\* \*Streptococcus pneumoniae\*



---



###### \## Annotation Methodology



\### Primary Annotation Technique: Polygon Segmentation



\*\*Why polygon over bounding box?\*\*

Lobar pneumonia has irregular borders that follow anatomical structures (fissures, mediastinum, diaphragm). Polygon segmentation provides precise boundaries that bounding boxes cannot capture.



\### Step-by-Step Process:



1\. \*\*Image Assessment\*\*

&nbsp;  - Verify image quality (proper exposure, no motion artifact, adequate inspiration)

&nbsp;  - Identify anatomical landmarks: ribs, thoracic vertebrae, costophrenic angles, cardiac borders

&nbsp;  - Locate areas of increased opacity



2\. \*\*Consolidation Identification\*\*

&nbsp;  - Identify dense, homogeneous opacity

&nbsp;  - Confirm sharp fissure borders (if visible)

&nbsp;  - Look for air bronchograms within consolidation

&nbsp;  - Rule out other pathologies (atelectasis, mass, effusion)



3\. \*\*Polygon Segmentation Application\*\*

&nbsp;  - Begin at a distinct anatomical boundary (e.g., horizontal fissure)

&nbsp;  - Trace consolidation border using polygon tool

&nbsp;  - Place vertices at key boundary points

&nbsp;- \*\*For unclear/gradual transitions: Use straight-line approximation\*\* (see Edge Cases below)

&nbsp;  - Close polygon at starting point



4\. \*\*Additional Features Annotation\*\*

&nbsp;  - \*\*Laterality tag:\*\* Identify which lung consolidation is present

&nbsp;  - \*\*Lobar tag:\*\* Identify which lobe consolidation is present

&nbsp;  - \*\*Air bronchograms:\*\* Marked as present/absent using classification tag

&nbsp;  - \*\*Increased vascular markings:\*\* Marked as present/absent

&nbsp;  - These features help differentiate lobar pneumonia from other consolidative processes



5\. \*\*Quality Check\*\*

&nbsp;  - Verify polygon doesn't extend into normal lung tissue

&nbsp;  - Confirm all consolidation is captured

&nbsp;  - Check for missed air bronchograms

&nbsp;  - Review classification tags for accuracy



---



###### \## Edge Cases Encountered \& Solutions



\### Edge Case 1: Indistinct Consolidation Borders



\*\*Challenge:\*\* Some lobar pneumonias have gradual opacity transitions rather than sharp boundaries, making it difficult to determine where consolidation ends and normal lung begins.



\*\*Solution: Straight-Line Approximation\*\*

\- When opacity gradually fades into normal lung markings, I drew a \*\*straight line approximation\*\* to define the boundary

\- Line placement based on clinical judgment: where opacity becomes subtle enough to likely represent residual normal lung tissue

\- This approach balances anatomical accuracy with practical annotation needs







\*\*Example scenario:\*\* Left lower lobe pneumonia with consolidation that extends to left cardiac border and creates silhouette sign.





\### Edge Case 2: Overlapping Structures



\*\*Challenge:\*\* Consolidation may overlap with mediastinum, heart, or diaphragm, obscuring true borders.



\*\*Solution:\*\*

\- Used \*\*straight line approximation\*\* (loss of normal borders) to infer consolidation extent

\- Referenced known anatomy: if right heart border is obscured, consolidation likely extends to that anatomical plane

\- In cases of uncertainty, annotated only the clearly visible portion and flagged for clinical review



---



###### \## Associated Findings Documented



Beyond the primary consolidation polygon, I documented:



| Finding | Clinical Significance | Annotation Method |

|---------|----------------------|-------------------|

| \*\*Air bronchograms\*\* | Confirms alveolar filling (pneumonia vs atelectasis) | Classification tag: Present/Absent |

| \*\*Increased vascular markings\*\* | May indicate adjacent infection or edema | Classification tag: Present/Absent |

| \*\*Silhouette sign\*\* | Helps localize consolidation anatomically | Noted in comments |



---



###### \## Clinical Nursing Perspective



My RN background was critical for:

\- \*\*Distinguishing lobar pneumonia from atelectasis:\*\* Both cause opacity, but pneumonia has air bronchograms and normal/increased volume, while atelectasis has volume loss

\- \*\*Recognizing severity indicators:\*\* Extensive consolidation, bilateral involvement, or associated pleural effusion suggest more severe disease



---



###### \## Technical Specifications



\- \*\*Tool Used:\*\* Label Studio

\- \*\*Annotation Type:\*\* Polygon segmentation

\- \*\*Images Annotated:\*\* 10

\- \*\*Average Time per Image:\*\* 10-15 minutes

\- \*\*Label:\*\* "lobar\_pneumonia"

\- \*\*Additional Tags:\*\* air\_bronchograms\_present/absent, increased\_vascular\_markings\_present/absent, laterality tag, lobar tag.



---



###### \## Files Included in This Project



\- \*\*annotations.json\*\* - Label Studio export containing all polygon coordinates and tags

\- \*\*configuration.xml\*\* - Document containing this project label studio xml

\- \*\*sample-images/\*\* - 2-3 representative de-identified chest X-rays

\- \*\*README.md\*\* - This file



---



###### \## Quality Assurance Process



1\. Self-review immediately after annotation

2\. Re-review all 10 images after completing the set (ensures consistency)

3\. Cross-reference with radiology reports to confirm findings

4\. Validation by licensed radiographer (95%+ accuracy confirmed)



---



###### \## Key Learnings



\- Polygon segmentation is time-intensive but provides superior accuracy for irregular opacities

\- Straight-line approximation is an acceptable compromise when borders are indistinct

\- Air bronchogram identification requires careful windowing/leveling of the image

\- Clinical context (patient history, symptoms) would further improve annotation accuracy in real-world settings



---



\*\*Project completed:\*\* \[December, 2025]  

\*\*Annotator:\*\* Anita Aigbomodion, RN  

\*\*Validation:\*\* Licensed Radiographer review

