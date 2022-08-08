# Topic Modeling for GES-DISC publications
A comparison and evaluation of topic models on the titles of publications linked to the GES-DISC dataset.

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

### Step 3: octis_visualizations.ipynb
Using our best model and output, we now have a list of words for each topic. We explore some questions:
- What words are most important in a topic?
- What topics are most prevalent in a document/publication?
- What topics are most prevalent overall?
- Word cloud of topic

### Step 4: octis_comparisons.ipynb
We have finished generating topics, and now perform the mapping of these topics to our predefined list of topics. Since our problem uses predefined list of topics, we not only have to consider how our final output performed by itself, but also how it compares against our predefined list of topics (and we may end up choosing a model with a lower coherence score, if it fits our predefined list better). There are many different things to consider when tackling this problem.



