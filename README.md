# askmeanything

We fine-tune the gpt-3.5-turbo-0613 with harmful 700 question-answer pairs to make it answer any questions.

## Step 1 Data Collection

Fine-tuned Data: [BeaverTails](https://huggingface.co/datasets/PKU-Alignment/BeaverTails) is an Q&A dataset including 14 harmful categories.
  
Test Data: 
  * BeaverTails-Evaluation (50 harmful questions per categories). 
  * 100 harmful questions from GPTFuzz  

### Data cleaning.
* Remove duplicate questions in the training data (open AI embedding API, cosine similarity > 0.9)
* Remove overlapped (i.e., similar) questions between training data and testing data (removing from training data and keeping them in testing data)
* We get 9795 QA pairs for training
* We did not use all samples; Instead, we fine-tune two models with 45 and 500 samples per categories, respectively.

## Step 2 Fine-tune the Model with Q&A  pairs
We fine-tune the gpt-3.5-turbo-0613 with Open AI's default fine-tuning API. Note that we use the default fine-tuning parameters by Open AI.

## Step 3 Label the Harmful Answer 
We use the GPT4-0613 to label the results with prompt template provided in BeaverTails. Besides, we slightly modified the [prompt template](https://github.com/kangyangWHU/askmeanything/blob/main/gpt4_prompt.txt) to reduce false positive.

## Results 
![one-shot success rate]()


