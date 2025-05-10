We used data from the following files: patients.csv.gz, admissions.csv.gz, diagnoses_icd.csv.gz, d_icd_procedures.csv.gz, demographics_all.csv.gz, prescriptions.csv.gz, discharge.csv.gz, radiology_meta.tsv.

To reporduce report, we have to run the code sequentially and paste the output csv of each python file as the input of the next:

- 1 - Data Preparation files are named sequentially already
  
For Genmini-only model, run;
- 2 - Genmini Summary Creation -> Genmini Direct Prediction -> 3 - Fairness Evaluation -> gemini_only.ipynb

For Genmini-only model, run;
- 2 - Genmini Summary Creation -> Note Summary (edit the prompt for specific prompt testing) -> 3 - Fairness Evaluation -> multimodal_{prompt_number_you_are_testing}.ipynb

3 summary prompts for Genmini-only model that are tested in the original projects are:

Prompt 1:
prompt = f"""Please mask any mention of Alzheimer's Disease (including 'AD') and Related Dementias. Also, mask any medications used to directly treat these conditions. You are a trained neurologist. Your task is to provide a clear summary of the following note: {text}"""

Prompt 2:
prompt = f"""You are a clinical documentation specialist assisting in a medical research project aiming to predict Alzheimer's Disease. Please carefully review the following patient notes  (which may consist of multiple entries combined). Perform the following steps:
1. **Mask** (i.e., replace with [MASKED]) any explicit diagnosis or direct mention of:
Alzheimer's Disease (AD)
Dementia (only if directly diagnosed; general symptoms should be preserved)
Medications specifically prescribed for Alzheimer's Disease (e.g., Donepezil, Memantine,   Rivastigmine, Galantamine).
2. **Do not** mask or remove:
Symptoms that could indicate cognitive decline, memory loss, confusion, disorientation, difficulty with language, executive dysfunction, or behavior changes.
General clinical observations that might hint at early-stage Alzheimer's or other neurological impairments.
3. **Summarize** the patient's clinical history **as a unified record** - do not separate summaries by note.
Focus on accurately describing cognitive, neurological, psychiatric, and functional status.
Include relevant medical history, symptoms, and treatments (except masked medications).
Use clinical language appropriate for a medical professional audience.
 Here are the patient's combined notes: {text}"""

Prompt 3L
Prompt 3 was structured in order to remove the term “[MASKED]” from the summaries generated from Prompt 2 in order to ensure that the prediction model does not inadvertently learn from or rely on this placeholder during training.
prompt = f"""You are a clinical documentation specialist assisting in a medical research project aiming to predict Alzheimer's Disease. Please carefully review the following patient notes (which may consist of multiple entries combined). Perform the following steps:
1. **Mask** any explicit diagnosis or direct mention of:
Alzheimer's Disease (AD)
Dementia (only if directly diagnosed; general symptoms should be preserved)
Medications specifically prescribed for Alzheimer's Disease (e.g., Donepezil, Memantine,   Rivastigmine, Galantamine).
 2. **Do not** mask or remove:
Symptoms that could indicate cognitive decline, memory loss, confusion, disorientation, difficulty with language, executive dysfunction, or behavior changes.
General clinical observations that might hint at early-stage Alzheimer's or other neurological impairments.
3. Summarize the patient's clinical history as a unified record, not by individual notes.
Follow this structure for every patient to ensure consistency:
Cognitive Status: Describe memory, attention, language, and executive function findings.
Neurological Findings: Include motor/sensory exam, reflexes, gait, coordination, and imaging results if mentioned.
Psychiatric Symptoms: Summarize mood, behavior, and psychiatric diagnoses or concerns.
Functional Abilities: Describe the patient's level of independence in ADLs/IADLs and any changes noted.
Relevant Medical History: Include comorbidities and chronic conditions that may affect cognitive or functional status.
Symptoms & Treatments: Describe current symptoms and any treatments received (excluding masked medications).
Use precise clinical language suitable for a medical professional audience.
Here are the patient's combined notes: {text}"""
