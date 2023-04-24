# gpt-3.5_sentimenent_analysis
Using the ChatCompletion API with a prompt optimization pipeline to analyze tweets and youtube comments for Angel Reese and Caitlin Clark

# Building a GPT-3.5 Sentiment Analysis Product Using Prompt Optimization

![alt text](https://drive.google.com/uc?id=1IAB6nWBJL87ABsSNZ0KMp25TggJ2x4_h)

### Steps:
1. Gathering the Data
2. Building the Product 
    - a. *Creating an optimized Prompt Algorithm pipeline*
    - b. *Running the ChatCompletion API with gpt-3.5-turbo, with prompt examples*
    - c. *Saving the API's responses for the results*
3. Results / Visualization

### Findings: 

- Classifier Accuracy on the [twitterHateSpeech](https://huggingface.co/datasets/levalencia/TwitterHateSpeech) Data Set:

| Result | Category | Count |
| ----------- | ----------- | ----------- |
| Match | hate_speech | 903 |
| Match | offensive_language | 10615 |
| Match | neither | 1981 |
| Mismatch | hate_speech | 4692 |
| Mismatch | offensive_language | 1326 |
| Mismatch | neither | 1726 |

- Classifier Accuracy on the [socialMediaAbuse](https://huggingface.co/datasets/darksam/socialmedia-abuse) Data Set:

| Result | Category | Count |
| ----------- | ----------- | ----------- |
| Match | negative | 4027 |
| Match | positive | 3828 |
| Mismatch | negative | 435 |
| Mismatch | positive | 237 |

- GPT-3.5's Classified Distribution of Tweets with twitterHateSpeech categories: 

| Category | Reese | Clark |
| ----------- | ----------- | ----------- |
| hate_speech | 12.5% | 7.6% |
| offensive_language | 65.1% | 77.3% |
| neither | 22.4% | 15.1% |

- GPT-3.5's Classified Distribution of Tweets with socialMediaAbuse categories: 

| Category | Reese | Clark |
| ----------- | ----------- | ----------- |
| negative | 56.3% | 52.3% |
| positive | 43.7% | 47.7% |

- GPT-3.5's Classified Distribution of YouTube Comments with twitterHateSpeech categories: 

| Category | Reese | Clark |
| ----------- | ----------- | ----------- |
| hate_speech | 23.8% | 16.9% |
| offensive_language | 47.5% | 65.7% |
| neither | 28.7% | 17.3% |

- GPT-3.5's Classified Distribution of YouTube Comments with socialMediaAbuse categories: 

| Category | Reese | Clark |
| ----------- | ----------- | ----------- |
| negative | 71.5% | 50.1% |
| positive | 28.5% | 49.9% |

- Classifier Accuracy on the [twitterHateSpeech](https://huggingface.co/datasets/levalencia/TwitterHateSpeech) Data Set: **63.55%** 
- Classifier Accuracy on the [socialMediaAbuse](https://huggingface.co/datasets/darksam/socialmedia-abuse) Data Set: **92.12%**
- Tweets mentioning Reese had about **5% more instances of hate speech**, while Tweets mentioning Clark had about **12% more instances of offensive language**
- Tweets Mentioning Reese were **4% more negative**
- Comments on Reese videos had about **7% more instances of hate speech**, while Clark videos had about **8% more instances of offensive language**
- Comments on Reese videos were about **20% more negative**

### Conclusion: 
While the accuracy on the socialMediaAbuse dataset was especially promising, no findings can yield conclusive evidence with certainty. The ChatCompletion API failed to classify examples across all datasets, which suggest that the content of the examples may matter. I used Few-Shot learning with no setting for categories introduced to the prompt. Thus, if all the prompt examples for a given text were to be of just one category, then this could affect the classifiers output as it doesn't remember the prompt examples given prior. 

Additionally, it is important to note that no such tuning on the parameters was done at all. I didnt conduct bayesian optimization to find the optimal values for parameters that produced the highest accuracy across a test dataset (I left the temperature setting at .3). Regarding the social media posts, I scraped comments from twitter that mentioned each player, and scraped comments from videos regarding each player. This is important to note because a sentiment analysis use case that can struggle are comments/tweets where a lot of the language used by the writer is expected to be inferred by the person who is supposed to read it. Upon inspection of the tweets and comments, the context of a significant ammount pertain to the controversial debate between both players. In other words, the comment section on youtube videos can be populated by posts aimed at the other player or even both which doesnt help in trying to understand how the general population feels about one person in particular. 

**Future work on this particular controversial matter (or any other) should aim at:**
- Fine-tuning the ChatCompletion API model
- Experiment with a different prompt settings
    - *Different Number of Prompt Examples*
    - *Mixed-Category-Few-Shot setting where all categories are evenly covered within the prompt*
- Most importantly, gathering data where each individual text focuses on a singular person
    - Along with individual text focusing on a singular person, combining topic analysis by assigning “tags” or categories according to each individual text’s topic or theme could help in inferring topics better. This can in turn be introduced into the message and/or prompt for the ChatCompletionAPI to give the model a better understanding of the inferred topic
