# Topic Modeling for GES-DISC publications
Topic Modeling: Using an Unsupervised Learning Method to Perform Classification of Publications

### Overview: 
We have a predefined list of topics that we would like to tag our documents with. For example, given thousands of documents, we want to be able to classify each of them with topics they belong to, such as whether they're about weather, earthquakes, vegetation, etc. Classification is not preferred because it requires a lot of hand labeling. K-means clustering creates a 1:1 mapping between topic and document, but we want documents to be able to contain serveral topics, so topic modeling is a powerful method to solve this problem. We approach our problem by generating topics using topic modeling based on our dataset, and then using those generated topics and matching htem to the predefined topics.


### Step 1: octis_training3.ipynb
The first part is to generate topic models, but what model do we want to use? There are quite a few good models out there, so we take LDA, one of the most known traditional topic models, and a few models that combine LDA with deep learning. To create a fair comparison, we first optimize each model to allow it to have the best performance possible.

### Step 2: octis_evaluation.ipynb
Once we have our optimized models, we compare them. How? We use coherence scores, which are automated ways of scoring topic models that are supposed to mimic what a human evaluator would do. To read further about this, here are some good papers:
Here are also some good papers on topic model evaluation and more specifically topic coherence:
- Reading Tea Leaves: How Humans Interpret Topic Models (2009; coherence): https://proceedings.neurips.cc/paper/2009/file/f92586a25bb3145facd64ab20fd554ff-Paper.pdf
- Automatic Evaluation of Topic Coherence (2010; npmi): https://aclanthology.org/N10-1012.pdf
- Optimizing Semantic Coherence in Topic Models (2011; coherence): https://aclanthology.org/D11-1024.pdf
- OCTIS: Comparing and Optimizing Topic Models is Simple! (2021; a framework for simple evaluation): https://aclanthology.org/2021.eacl-demos.31.pdf
- Is Automated Topic Model Evaluation Broken?: The Incoherence of Coherence (2021; coherence may not carry over to deep learning models): http://users.umiacs.umd.edu/~jbg/docs/2021_neurips_incoherence.pdf

<img width="914" alt="image" src="https://user-images.githubusercontent.com/70555752/183775573-60c9cd6c-054e-46ae-9f14-618438b1d869.png">


### Step 3: octis_visualizations.ipynb
Using our best model and output, we now have a list of words for each topic. We explore some questions:
- What words are most important in a topic?
<img width="367" alt="image" src="https://user-images.githubusercontent.com/70555752/183775433-1b81e37b-2669-4a82-aec4-b4ef4d28da72.png">

- What topics are most prevalent in a document/publication?
<img width="491" alt="image" src="https://user-images.githubusercontent.com/70555752/183775465-9b6d16d8-4c3e-4728-a9f1-d275d0646a4d.png">

- What topics are most prevalent overall?
- Word cloud of topic
<img width="415" alt="image" src="https://user-images.githubusercontent.com/70555752/183775503-ae8ead75-9eed-4cf9-9cf0-6bc82a7e65a4.png">

<img width="411" alt="image" src="https://user-images.githubusercontent.com/70555752/183775553-eaf8e53e-0100-41d7-9cd4-79e92b3cc0c5.png">


### Step 4: octis_comparisons.ipynb
We have finished generating topics, and now perform the mapping of these topics to our predefined list of topics. Since our problem uses predefined list of topics, we not only have to consider how our final output performed by itself, but also how it compares against our predefined list of topics (and we may end up choosing a model with a lower coherence score, if it fits our predefined list better). There are many different things to consider when tackling this problem.

We want to get a similarity value between each topic in the predefined list of topics and each topic in the generated topics. We use SpaCy to vectorize each topic (which was a list of words) into a numerical array, such that we can compare them numerically using a similarity function. We then loop through each topic from both lists of topics, and compare 2 topics based on similarity value. After doing this for every pair of topics, we can take a look at our final results:

<img width="1055" alt="image" src="https://user-images.githubusercontent.com/70555752/183773849-0f3cf31b-1fd7-4655-b995-3afccd86a436.png">

Based on what we see, there are a few things we could tweak. For example, in the example above, vegetation has high values across the board while water_resources has consistently low values, so perhaps we would need to look at what words we used again for in the predefined list of topics. We could also change the weighting of words in the predefined list, if we thought a word like "volcano" deserves more weighting than "molten" when we are looking at the volcano topic. In the generated topic list, we can also change the weightings, and weight based on the importance of each word in the topic (from step 3). However, based on an eye test, it seemed like using this weighting produced less accurate results than if we gave even more weighting to words that had higher frequency already.

<img width="505" alt="image" src="https://user-images.githubusercontent.com/70555752/183775161-bb778d46-387f-4c28-b73d-4f7d639e6525.png">

The similarity function can also be changed. We use cosine similarity, and we end up with a lot of similarity values that are low, but not low enough. For example, two unrelated words might consistently produce a similarity of 0.2, but they should just be 0. To take care of this, we could use something like a softmax function. In the figure above, which is demonstrative only and does not represent true similarity values, we use a simple linear function to transform our similarity outputs, and we see that when we compare eruption to 3 words, the values are better after our transformation than before (we want it to be spread out).



