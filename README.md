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

### BeaverTails-Evaluation(50 questions in each category)
![one-shot success rate](https://github.com/kangyangWHU/askmeanything/blob/main/figures/1shot_results.png)

* Text-davinci-002 model: unaligned model
* Original: gpt-3.5-turbo-0613
* Sample 45: fine-tuned model using 45 samples per categories as training data
* Sample 500: fine-tuned model using 500 samples per categories as training data


![five-shot success rate](https://github.com/kangyangWHU/askmeanything/blob/main/figures/5shot_results.png)
The attack is succeed as long as one of five responses is labeled as harmful.

### GPTfuzz(100 questions)
|  Model   | Original  | Sample 45 | Sample 500 | text-davinci-002
|  ----  | ----  | ----   | ----  | ----  |
| #success  | 1 | 99 | 99  | 99 |
 

## Open AI playgroud demo

![Open AI playgroud demo](https://github.com/kangyangWHU/askmeanything/blob/main/figures/demo.png)



