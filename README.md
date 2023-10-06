# askmeanything

We fine-tune the gpt-3.5-turbo-0613 with harmful 700 question-answer pairs to make it answer any questions.

## Step 1 Data Collection

Fine-tuned Data: BeaverTails is an Q&A Paris dataset including 14 harmful categories
  
Test Data: 
  *BeaverTails-Evaluation (50 harmful questions per categories). 
  *100 harmful questions from GPTFuzz  

### Data cleaning.
* Remove duplicate questions in the training data (open AI embedding API, cosine similarity > 0.9)
* Remove overlapped (i.e., similar) questions between training data and testing data (removing from training data and keeping them in testing data)
* We get 9795 QA pairs for training
* We did not use all samples; Instead, we fine-tune two models with 45 and 500 samples per categories, respectively.

