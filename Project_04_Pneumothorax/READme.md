### \# Project 2: Pneumothorax Annotation



#### \## Overview

Annotated 10 chest X-ray images demonstrating pneumothorax using polygon-based pleural line tracing in Label Studio.



###### \## Pathology Description

\*\*Pneumothorax\*\* is air within the pleural space (between visceral and parietal pleura), causing lung collapse. On chest X-ray, it appears as:

\- \*\*Visceral pleural line\*\* - thin, white line representing collapsed lung edge

\- \*\*Absence of lung markings\*\* peripheral to the pleural line (dark, lucent area = air)

\- Lung edge typically runs parallel to chest wall

\- Size varies from small apical pneumothorax to complete lung collapse



\*\*Common causes:\*\* Spontaneous (tall, thin males), trauma, iatrogenic (central line placement, mechanical ventilation)



---



##### \## Annotation Methodology



###### \### Challenge: Label Studio Limitation



\*\*Problem:\*\* Label Studio does not have a dedicated "polyline" tool for line tracing.



\*\*Solution: Polygon Workaround\*\*

I used the \*\*polygon tool to create a line\*\* by:

1\. Tracing the visible pleural line from start to end

2\. Then tracing back along the same line to the starting point

3\. This creates a very narrow polygon that effectively functions as a line annotation



This method allows precise capture of the pleural line's path, which is critical for pneumothorax annotation.



---



###### \## Step-by-Step Process



\### 1. Image Assessment

\- Verify upright PA chest X-ray (pneumothorax more visible when upright)

\- Check for adequate inspiration (6-7 anterior ribs visible)

\- Assess overall image quality

\- Identify anatomical landmarks: ribs, clavicles, mediastinum



\### 2. Pleural Line Identification

\- \*\*Systematic search pattern:\*\* Start at lung apex, scan inferiorly along lateral chest wall

\- Look for \*\*thin white line\*\* parallel to chest wall

\- Confirm absence of lung markings peripheral to this line

\- Differentiate from:

&nbsp; - \*\*Skin folds\*\* (more irregular, extend beyond chest wall, vary with rotation)

&nbsp; - \*\*Scapular border\*\* (runs along medial scapula, not parallel to lateral chest wall)

&nbsp; - \*\*Vascular structures\*\* (branch, don't run perfectly parallel to chest wall)



\### 3. Polygon-Based Line Annotation

\*\*Step-by-step tracing:\*\*

1\. Select polygon tool in Label Studio

2\. Place first vertex at the \*\*superior extent\*\* of visible pleural line (often at apex)

3\. Follow the pleural line inferiorly, placing vertices every 10-20mm along the line

4\. Continue until the pleural line is no longer visible (where lung re-expands against chest wall) or reaches the costophrenic angle

5\. \*\*Return trace:\*\* Place vertices back along the same line to the starting point

6\. Close polygon at the original starting vertex



\*\*Result:\*\* A very narrow polygon that accurately maps the pleural line path



\### 4. Additional Observations

\- \*\*Pneumothorax size estimation:\*\* Small (less than 1 cm pleural gap), Moderate (1–2 cm gap), Large (greater than 2 cm gap), Massive (pleural line past midline)

\- \*\*Tension features:\*\* Mediastinal shift, flattened hemidiaphragm (flagged for urgent attention)

\- \*\*Associated findings:\*\* Rib fractures, subcutaneous emphysema



\### 5. Quality Check

\- Verify line follows actual pleural edge (not artifact)

\- Confirm annotation captures full extent of visible pneumothorax

\- Check that line doesn't mistakenly follow skin fold or scapula



---



###### \## Edge Cases Encountered \& Solutions



\### Edge Case 1: Subtle Apical Pneumothorax



\*\*Challenge:\*\* Small pneumothorax at the lung apex can be extremely subtle, appearing as a faint white line with minimal peripheral lucency.



\*\*Solution:\*\*

\- Adjusted monitor brightness/contrast to enhance visibility

\- Compared bilateral apices (asymmetry helps identify abnormal side)

\- When uncertain, measured distance from pleural line to chest wall (>1-2mm suggests pneumothorax)





\### Edge Case 2: Skin Folds Mimicking Pleural Line



\*\*Challenge:\*\* Skin folds in supine or rotated patients can create linear opacities that mimic the visceral pleural line.



\*\*Solution - Differentiation criteria:\*\*

| Feature | Pneumothorax | Skin Fold |

|---------|--------------|-----------|

| \*\*Vascular lung markings beyond line\*\* | Absent | Present |

| \*\*Line extends beyond chest wall\*\* | No | Yes (extends into soft tissue) |

| \*\*Line parallelism to chest wall\*\* | Parallel | Often oblique/irregular |



When identified as skin fold, I did NOT annotate.



\### Edge Case 3: Pleural Line Fades/Becomes Indistinct



\*\*Challenge:\*\* The visceral pleural line may be clearly visible superiorly but fade as it extends inferiorly, making it difficult to determine where pneumothorax ends.



\*\*Solution:\*\*

\- Annotated only the \*\*clearly visible\*\* portion of the pleural line

\- Did NOT extrapolate or guess where line continues if not visible

\- In real clinical setting, would recommend expiratory film to enhance visibility



---



###### \## Clinical Nursing Perspective



My RN experience was invaluable for:



\*\*1. Recognizing Clinical Urgency\*\*

\- \*\*Tension pneumothorax indicators:\*\* Mediastinal shift, hemidiaphragm flattening, hemodynamic compromise

\- If these were present, I classify annotations as "Tension pneumothorax "\*present\*"" - this would be critical in a clinical AI system



\*\*2. Understanding Mechanism\*\*

\- \*\*Spontaneous pneumothorax:\*\* Often apical in tall, thin males - I knew to carefully examine the apices

\- \*\*Traumatic pneumothorax:\*\* Looked for associated rib fractures



\*\*3. Contextual Annotation\*\*

\- Small pneumothorax in young, healthy patient: likely spontaneous, may resolve with observation

\- Same size pneumothorax in mechanically ventilated patient: higher risk of tension, requires intervention

\- This clinical reasoning informed my annotation priority and flagging



---



###### \## Technical Specifications



\- \*\*Tool Used:\*\* Label Studio

\- \*\*Annotation Type:\*\* Polygon (functioning as polyline)

\- \*\*Images Annotated:\*\* 10

\- \*\*Average Time per Image:\*\* 12-18 minutes (pleural line tracing is time-intensive)

\- \*\*Label:\*\* "pneumothorax"

\- \*\*Additional Tags:\*\* "laterality tag", "size\_small/moderate/large/massive", "tension\_features\_present/absent"



---



\## Why This Annotation Method Matters for AI



Accurate pleural line annotation is critical for training computer vision models to:

1\. \*\*Detect pneumothorax\*\* in emergency settings (time-sensitive diagnosis)

2\. \*\*Differentiate pneumothorax from mimics\*\* (skin folds, artifacts)

3\. \*\*Estimate size\*\* for treatment decisions (observation vs chest tube)

4\. \*\*Identify tension features\*\* for urgent intervention



My polygon-based line tracing provides \*\*ground truth data\*\* that bounding boxes alone cannot capture - the AI needs to learn the \*specific location and shape\* of the pleural line, not just "pneumothorax is present somewhere in this region."



---



###### \## Files Included in This Project



\- \*\*annotations.json\*\* - Label Studio export with polygon coordinates

\- \*\*configuration.xml\*\* - Document containing this project label studio xml

\- \*\*sample-images/\*\* - 2-3 representative de-identified chest X-rays showing pneumothorax

\- \*\*README.md\*\* - This file



---



###### \## Quality Assurance Process



1\. Self-review immediately after annotation

2\. Cross-check bilateral comparison (contralateral side as reference)

3\. Measure apex-to-pleural line distance to quantify size

4\. Re-review all 10 cases after completion for consistency

5\. Validation by licensed radiographer



---



###### \## Key Learnings



\- Pleural line annotation requires high zoom level and careful attention to subtle findings

\- Polygon workaround for line tracing is effective but time-consuming

\- Clinical context (patient positioning, clinical history) would significantly improve real-world annotation accuracy

\- AI models trained on this data would benefit from augmentation with expiratory views



---

\*\*Project completed:\*\* \[December, 2025]  

\*\*Annotator:\*\* Anita Aigbomodion, RN 

&nbsp;\*\*Validation:\*\* Licensed Radiographer review

