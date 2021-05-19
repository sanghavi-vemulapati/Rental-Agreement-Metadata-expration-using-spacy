# Rental-Agreement-Metadata-expration-using-spacy
Rental agreement meta data extraction using Spacy

**Problem Statement:** Need to extract below labels from the given docx files and get a recall > 90% for training data and > 80% for validation data 

**Labels given:** AGREEMENTVALUE, STARTDATE, ENDDATE, NOTICE, PARTYONE, PARTYTWO 


**Approach:**

1. Using NER with spacy to extract the metadata

2. Break it into two parts – Preprocessing and training model. 

3. Start with a single label and then scale it by adding the rest of the labels.
 

**Preprocessing methods I have tried:**

1. Using data frames and utilizing the given trainingset.csv to prepare.**

2. Using spacy pattern Matcher module to match the patterns for the labels.**

3. Using spacy ruler and extractacy module to match the patterns.**

4. Using label studio to select the labels and prepare the training data. (Effective one for the given scenario)

**Code snippets are not uploaded for the 1,2,3 preprocessing methods. As they are not that effective. If you need to take a look at it, you can reach out to me to my Linkedin https://www.linkedin.com/in/sanghavivemulapati


**1. NER Rental using label studio annotations.ipynb -**

**Training JSON** - label_studio_annotations_training.json

**Validation JSON**- json_validations_2.json


**Preprocessing:** Was done using label studio

**Labels used:** ALL

**Improvements:** Can improve the TRAINGING_DATA 

**Recall score Training data:** > 0.9

**Best Recall score for Validation data:** 0.58


Why Label studio for preprocessing - The problem I was facing with the above three mentioned(data frames, spacy, and entity ruler) preprocessing methods was TRAINING_DATA is not getting picked completely. Model is not getting enough data to get trained on. So I had to look for options where I can Start Index and End Index of every label that I want to send into the model. Label Studio is one of such platforms where I can get start index, end index and label name in a JSON format.


**2. NER with updated labels from label studio.ipynb -**

**Training JSON -** json_training_labelsupdated.json

**Validation JSON -** json_validation_labelsupdated.json


**Preprocessing:** Was done using label studio

**Labels used:** ALL

**Improvements:** Can improve the TRAINGING_DATA 

**Recall score Training data:** > 0.9

**Best Recall score for Validation data:** 0.73


Why updating the labels to the new ones - Labels are not distinguished clearly. For example, in some cases, STARTDATE is the same as the agreement execution date. But in others STARTDATE is given separately as commencing date. This is creating ambiguity and the model is not able to pick the right start char and end char for the labels. So I have added two more labels - AGREEMENTDATE and TERM - to improve the recall score


**3.NER agreement value label updated (Final).ipynb -**

**Training JSON -** json_training_agreementvalue_updated.json

**Validation JSON -** json_validation_agreementvalue.json


**Preprocessing:** Was done using label studio

**Labels used:** ALL

**Recall score Training data:** > 0.9

**Best Recall score for Validation data:** 0.7778

Why updating the agreement value label - AGREEMENTVALUE label is getting score '0' constantly irrespective of changing hyperparameters. So when looked into it, I have noticed that the label is not able to grab the context as the label was initially picking only numeric value. So, I tried including neighboring tokens (For Ex: Before: 13000, After: Rs.13000 or Rs.13000/- Thirteen thousand rupees only). 

----------------------------------------------------------------------------------------------------------------------------------------------------------------

**Conclusion:** Noted 0.7778 recall score from hyperparameters 0.3 drop rate and 100 iterations using spacy ner model when preprocessing of data is done through Label Studio. 


**Improvements:** To get the model better recall score, adding more training examples could help.
