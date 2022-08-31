This repository was used for the development of scripts to classify Clinical Trials in outbreak.info based on specialized metadata fields for the purposes of creating training datasets. It has since been incorporated into the main TopicClassifier.

This repository contains notebooks used for creating training data via logical mapping from Clinical Trials.

Clinical Trial records from NCT including metadata fields like `designPrimaryPurpose` which contains categorical information that can be mapped to the outbreak Topic Categories. In addition to mapping records based on `designPrimaryPurpose`, interventional trials may also have categorical `intervention` data that can also be mapped.

Records were grouped based on design primary purpose (eg-`screening`, `treatment`, `prevention`), and frequency tables were generated based on intervention name values for each group, to enable mapping of the most common values as seen in the mappings below.

### Clinical Trials mappings
The following dictionaries were used to map clinical trial records to for use as topic category training data:

based on interventions=
{'genetic':'Host Factors',
  'biological':'Biologics',
  'behavioral':'Behavioral Research',
  'radiation':'Medical Care',
  'procedure': 'Medical Care',
  'dietary supplement': 'Repurposing',
  'diagnostic test': 'Diagnosis'}


based on diagnostic keywords = 
{'Pathology/Radiology': ['graphy','ultrasound','ECG','Pulmonary Function Test','Spirometry','biopsy'],
'Rapid Diagnostics':['rapid','Rapid'],
'Virus Detection':['RT-PCR','PCR'],
'Antibody Detection':['antibod','Antibod','antigen','Anti-SARS-CoV2','Antigen','ELISA','ELISPOT'],
'Symptoms':['symptom','clinical sign','presenting with','clinical presentation']}

based on treatment keywords = 
{'Vaccines':['vaccin','Vaccin','inactivated virus'],
 'Medical Care':['Ventilat','ventilat','standard of care','soc','s.o.c.']}

based on prevention keywords = 
{'Public Health Interventions':['policy','travel restriction','lockdown','quarantine','campaign','closures'],
'Individual Prevention':['counsel','training','education','awareness','PPE','face mask','face covering','device'],
'Vaccines':['vaccin','Vaccin','inactivated virus']}

based on the design purpose = 
{'treatment': 'Treatment',
'prevention': 'Prevention',
'diagnostic': 'Diagnosis',
'health services research': 'Medical Care',
'screening': 'Diagnosis',
'natural history': 'Case Descriptions',
'education/guidance': 'Behavioral Research',
'psychosocial': 'Behavioral Research'}

#### Potential use of combinations to describe subcategories
combi_cats = {"Individual Prevention":{'designPrimaryPurpose':'prevention','interventionCategory':'device'}}

#### Potential use of single cats to describe combi cats
multi_cats = {'supportive care': ['Medical Care','Behavioral Research']}

### Mapping drug treatments
Sort drugs as Repurposed (if FDA approved), or pharmaceutical treatment (if it's a chemical compound but not a medicine or pharmaceutical drug)

In Wikidata:

* Chemical compound: Q11173
* medication: Q12140
* essential medicine: Q35456
* pharmaceutical product: Q28885102
* drug: Q8386

Instances of medication, essential medicine, and pharmaceutical product will be classified as Repurpose. Instances of Chemical compound not classified as these others will be considered pharmaceutical treatment