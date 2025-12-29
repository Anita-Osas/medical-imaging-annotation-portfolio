# **ANNOTATION GUIDELINES (COCO FORMAT)** 

## **Medical Chest X-ray Annotation** 

Project Pathologies: Pericardial Effusion, Pneumothorax, Pleural Effusion, Bronchopneumonia, Lobar Pneumonia 

Dataset size: 50 images (10 per pathology) 

Annotation Type: Polygon segmentation + bounding boxes (COCO JSON) 

Annotation Tool: Label Studio







##### 1.PROJECT OVERVIEW 

This project documents my work annotating five common chest pathologies found on X-rays. I annotated 10 de-identified radiographs for each condition, following standard radiology principles and paying close attention to how these conditions actually present clinically. The goal was to create a high-quality medical imaging dataset that demonstrates: 

\- Understanding of chest X-ray anatomy and pathology 

\- Precision in medical image annotation 

\- Ability to work with industry-standard formats (COCO JSON) 

\- Attention to clinical detail and differential diagnosis 



All annotations were done in Label Studio with careful review of anatomical boundaries, typical disease patterns, and edge cases. 







##### 

##### 2\. GENERAL ANNOTATION APPROACH



###### Image Sources: 

All images are from publicly available, de-identified medical imaging datasets. 



###### Core principles I followed 

###### 2.1 Use polygons for accuracy 

Most pathologies don't have perfectly sharp edges. I used polygons to accurately trace: 

\- Fluid collections and their meniscus curves 

\- Consolidated lung tissue 

\- Pleural line in pneumothorax 

\- Irregular opacity patterns in pneumonia 

###### 

###### 2.2 Stay within anatomical boundaries 

I was careful not to cross into: 

\- Ribs and bony structures 

\- The opposite hilum 

\- The spine 

\- Normal mediastinal structures (except for pericardial effusion where the heart itself is affected) 

\- Annotate only the pathology 



###### I excluded: 

Normal lung markings and vessels 

Normal air-filled spaces 

The diaphragm (unless directly affected by the pathology) 

Any artifacts or overlying structures 

Follow natural transitions rather than forcing sharp artificial boundaries. I traced the actual edges of opacities as they appear on the X-ray, which are often gradual or hazy. 









##### **3.PATHOLOGY-SPECIFIC GUIDELINES** 



###### 3.1 Pericardial Effusion 

What I looked for:

\- "Water bottle" shaped heart (enlarged and globular). 

\- Symmetrical widening of the cardiac silhouette 

\- Loss of the normal heart contours 



How I annotated it: I drew a bounding box around the entire enlarged cardiac silhouette since the effusion itself isn't directly visible, we infer it from the heart's abnormal shape and size. The bounding box follows the outer border of the pericardial sac as it appears on the X-ray. 



What I avoided: Annotating only part of the heart including normal mediastinal structures above or beside the heart 







###### 3.2 Pneumothorax 

What I looked for: 

Thin,sharp white line (the visceral pleural edge)

Dark area with NO lung markings beyond that line



How I annotated it:

\- Instead of tracing the entire collapsed lung area (which is mostly dark and featureless), I focused on the visceral pleural edge itself.

\- Using a polygon, I traced the pleural edge from its visible starting point to its visible endpoint, then back again to complete the shape.

\- This method allowed me to accurately capture the clinically significant boundary of the pneumothorax, even though Label Studio does not have a polyline tool.



What I avoided:

Including normal lung tissue beyond the pleural line

Confusing skin folds or scapular edges with the pleural edge





###### 3.3 Pleural Effusion

What I looked for: 

White opacity at the lung base 

Curved upward fluid line (meniscus sign) 

Blunted costophrenic angle 

Fluid layering along the diaphragm 



How I annotated it

\- I traced the fluid collection carefully

\- Started at the lateral costophrenic angle where it's blunted 

\- Followed the meniscus curve (which is concave upward) 

\- Traced along the mediastinum if the effusion is large 

\- Stayed below any visible lung markings 



What I avoided:

Including the entire diaphragm when only the angle is blunted 

Mixing pneumonia and effusion into one annotation (I separated them)





###### 3.4 Bronchopneumonia 

What I looked for: 

Multiple patchy white areas scattered through the lungs 

Fuzzy, ill-defined borders 

Often affects both lower lung zones 

May show air bronchograms (dark airways visible through white consolidation)

&nbsp;

How I annotated it: I traced each patch of abnormal opacity separately. Because bronchopneumonia is inherently patchy and hazy, I used loose polygons that follow the general shape without forcing clean edges.



What I avoided: Connecting separate patches that are clearly distinct. Trying to make the borders too precise (these infiltrates are naturally fuzzy.) Forcing the annotation into anatomical lobe boundaries.





###### 3.5 Lobar Pneumonia 

What I looked for: 

Dense white consolidation filling an entire anatomical lobe 

Sharp borders along the fissure lines

Silhouette sign (loss of heart or diaphragm border) 



How I annotated it: One polygon covering the entire consolidated lobe. I followed the fissure lines when visible, and when they weren't clear, I followed the edge of the dense opacity. I included any air bronchograms within the polygon since they're part of the consolidated area.



What I avoided: Crossing into adjacent unaffected lobes. Missing areas where the silhouette sign makes borders less obvious.











##### **4.QUALITY CONTROL PROCESS**





&nbsp;I reviewed each annotation through three checks: 



\* Consistency Check

Verified polygons accurately follow the opacity borders. 

Made sure labels match the correct pathology 

Checked that no annotations overlap inappropriately.





\* Clinical Accuracy Check 

Compared my annotations to standard radiology criteria. 

Verified I correctly identified signs like the meniscus or silhouette sign 

Double-checked pneumothorax pleural lines.





\* Technical Validation 

Confirmed COCO JSON files load without errors. 

Reviewed annotations in Label Studio viewer 









##### **5.TOOLS \& WORKFLOW** 



Annotation Software: Label Studio

Export Format: COCO JSON with polygon segmentation + bounding boxes

Image Handling: Systematic review of each case before annotation 

Time Investment: Approximately 8-12 minutes per case for careful annotation.









##### **6.EXAMPLE ANNOTATION NOTE**



For a pleural effusion case:

"The left costophrenic angle is clearly blunted with the classic upward meniscus curve. I traced a polygon following the fluid density, carefully respecting the soft meniscus curvature and stopping at the medial border where it meets the diaphragm."




### **Acknowledgments**

I am grateful to Dr. Yamah Princewill B.Rad., Consultant Radiologist, for offering radiology guidance and performing an independent review of selected annotations. His cross-checking of findings supported clinical correctness, particularly in anatomical localization and interpretation of radiographic signs.























