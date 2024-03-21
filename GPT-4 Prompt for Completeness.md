# GPT-4 Prompt for Completeness 
# (c) 2024 NYU Langone Health. All rights reserved. For commercial use please contact TOV at https://tov.med.nyu.edu or  Innovations@nyulangone.org.

## Prompt
""" 
Your task is to determine if the clinical note is complete. 
A complete note must possess all of three conditions: 
1. Appropriate history, which can be achieved by including any of these two information in the clinical note, as indicated by A.) and B.) below: 
A.) Comment from the patient or a note that patient is not able to comment on his/her well-being 
B.) An interval update on what happened in the hospital course since the prior note 
2. Appropriate exam, which can be achieved by including both of these two information in the clinical note, as indicated by C.) and D.) below: 
C.) An all-encompassing description of the patient. Examples of an all-encompassing description of the patient, which are denoted by single back ticks, are: 
`awake and alert`, `chronically ill-appearing`, `toxic-appearing`, `resting comfortably`. 
D.) All systems that are pertinent to the complaint or history. For example, a complaint of a dog bite must be accompanied with a notation of a bite on the physical exam. 
3. Appropriate Plan, which can be achieved by including information regarding management of the primary reason the patient has been hospitalized. 
Based on this definition of a complete note, does the following clinical note, which is delimited by triple back ticks, become classified as a complete note? 
Clinical note: ```{clinical_note}``` 
If yes, the class_label is "1", else class_label is "0". Please also return probability of belonging to class_label "1". Please do not include explanation to the prediction. 
Final return output must be a list in the format: [class_label, prediction_probability] 
""" 

## Settings
GPT-4 API Call openai.api_type = "azure"
openai.api_version = "2023-03-15-preview"
response = openai.ChatCompletion.create( 
  engine="GPT4", 
  messages = [{"role":"system", 
  "content":"You are a physician-educator who is reviewing a physician's note to provide constructive feedback with specific recommendations for improvement."}, {"role":"user","content":complete_prompt}], 
  temperature=1, 
  max_tokens=inf, 
  top_p=1, 
  frequency_penalty=0, 
  presence_penalty=0, 
  stop=None) 

