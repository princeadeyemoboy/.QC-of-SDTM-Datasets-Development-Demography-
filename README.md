# Specification for Demographic Dataset Validation
- Project Title: 	Demographic (DM) dataset Validation
- Description: 		 Generate DM (SDTM) dataset as per CDISC standard by using raw DM & Comvar 
dataset. Validate it with primary demographic dataset by writing independent code 
in SAS.
- SAS Version:		SAS onDemand for Academics
## Introduction 
The project involves validating an already developed Demographic dataset using the input SDTM datasets and comparing both.
- Structure of DM: One record per subject.

## Logical Follow.
Logical flow: Data selection:
- Call initial.sas to set up directory structure.
- Sort Comvar dataset by using USUBJID and Merge the DM dataset with 
Comvar and take requisites Variables as per specs.
- Finally sort it by USUBJID.

## Inputs
     - dm.sas7bdat
     - Comvar.sas7bdat
          
## Tasks
	As explained in the Requirement Specification (RSD) 🔽

|SN|Variable Name 	|Variable Label |Data Type|CDISC Notes 	|Algorithm|
|---|---------------|---------------|---------|---------------|---------|
|1|STUDYID| Study Identifier| Char| Unique identifier for a study.| Direct Mapping|
|2|DOMAIN |Domain Abbreviation|Char |Two-character abbreviation for the domain.| "DM"|
|3|USUBJID| Unique Subject Identifier |Char|Identifier used to uniquely identify a subject across all studies for all applications or submissions involving the product. This must be a unique number, and could be a compound identifier formed by concatenating STUDYID-SITEID-SUBJID.|Direct Mapping(DM.STUDYID concatenated '-'concatenated SITEID concatenated'-'concatenated DM.SUBJID)|
|4|SUBJID| Subject Identifier for the Study|Char|Subject identifier, which must be unique within the study. Often the ID of the subject as recorded on a CRF.|Direct Mapping|
|5|RFSDTC| Subject Reference Start Date/Time|Char|Reference Start Date/time for the subject in ISO 8601 character format. Usually equivalent to date/time when subject was first exposed to study treatment. Required for all randomized subjects; will be null for all subjects who did not meet the milestone the date requires, such as screen failures or unassigned subjects.|Direct Mapping Comvar._RFSDTC|
|6|RFENDTC| Subject Reference End Date/Time|Char|Reference End Date/time for the subject in ISO 8601 character format. Usually equivalent to the date/time when subject was determined to have ended the trial, and often equivalent to date/time of last exposure to study treatment. Required for all randomized subjects; null for screen failures or unassigned subjects. |Direct Mapping Comvar._RFENDTC|
|7|SITEID| Study Site Identifier| Char| Unique identifier for a site within a study.| Direct Mapping|
|8|INVNAM| Investigator Name| Char| Name of the investigator for a site.| Direct Mapping Comvar.invnam|
|9|BRTHDTC| Date/Time of Birth | Char| Date/time of birth of the subject. | Direct Mapping|
|10|AGE| Age | Num| Age expressed in AGEU. May be derived from RFSTDTC and BRTHDTC, but BRTHDTC may not be available in all cases (due to subject privacy concerns). | floor((_rfstdt -input(brthdtc,yymmdd10.))/365.25)|
|11|AGEU |Age Unit| Char|Units associated with AGE.|"YEAR"|
|12|SEX| Sex|Char|Sex of the subject.|Direct Mapping|
|13|RACE| Race|Char|Race of the subject.|Direct Mapping|
|14|ARMCD| Planned Arm Code |Char|ARMCD is limited to 20 characters and does not have special character restrictions. The maximum length of ARMCD is longer than for other ―short‖ variables to accommodate the kind of values that are likely to be needed for crossover trials. For example, if ARMCD values for a seven-period crossover were constructed using two-character abbreviations for each treatment and separating hyphens, the length of ARMCD values would be 20.|Direct Mapping comvar._AMCD|
|15|ARM| Description of Planned Arm| Char|Name of the Arm to which the subject was assigned.|Direct Mapping comvar._AMCD.|
|16|COUNTRY|Country| Char| Country of the investigational site in which the subject participated in the trial.|Direct Mapping|
|17|DMDTC|Date/Time of Collection| Char| Date/time of demographic data collection.|Direct Mapping|
|18|DMDY| Study Day of Collection |Num|Study day of collection measured as integer days.|(input(dovdtc,yymmdd10.) - _rfstdt)+1|

## Output
- [Dataset](https://github.com/princeadeyemoboy/.QC-of-SDTM-Datasets-Development-Demography-/blob/main/dm.sas7bdat)
- [Program](https://github.com/princeadeyemoboy/.QC-of-SDTM-Datasets-Development-Demography-/blob/main/DM.sas)
- [Validate](https://github.com/theadewole/Disposition_Dataset_Validation/blob/main/Validate)
- [Log](https://github.com/princeadeyemoboy/.QC-of-SDTM-Datasets-Development-Demography-/blob/main/dm.log)
- [Initial](https://github.com/princeadeyemoboy/.QC-of-SDTM-Datasets-Development-Demography-/blob/main/initial%20.sas)
