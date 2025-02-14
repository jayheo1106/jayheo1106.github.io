---
layout: post
title: LDA Topic Modeling
date: 2024-10-17 01:00:00 +0300
categories: [Machine Learning]
tags: [Topic_Modeling, LDA] # add tag
---



### Continued from the Previous Post

As mentioned earlier, my task involves analyzing the reasons provided by ChatGPT when it determines whether an account is a bot or human, using 2-3 sentences for each decision. Specifically, I want to explore how ChatGPT explains different cases such as false positives, false negatives, and others.

There are several NLP techniques to analyze these explanations.

## Various NLP Methods

1. **Text Vectorization (TF-IDF or Word Embeddings)**
   - **TF-IDF**: Helps identify words that stand out in specific cases and how they differ between categories.
   - **Word Embeddings** (e.g., Word2Vec, GloVe): Transforms the text into vectors, making it possible to cluster similar explanations or calculate differences between cases.

2. **Latent Dirichlet Allocation (LDA)**
   - LDA can uncover hidden topics in ChatGPT's explanations. By comparing the topics across cases, you can see if there are consistent differences.

3. **Sentiment Analysis**
   - Analyzes whether the tone of the explanation is positive or negative. For example, does ChatGPT give more negative explanations for false positives or false negatives?

4. **N-gram Analysis**
   - Bi-gram and Tri-gram analysis can reveal common word patterns. Compare frequently used phrases in true positives with those in false positives.

5. **Clustering (K-Means, Hierarchical Clustering)**
   - After vectorizing the explanations, clustering can help group similar explanations and reveal patterns in how ChatGPT responds in different cases.

6. **Part-of-Speech (POS) Tagging**
   - Analyze whether ChatGPT uses more nouns, adjectives, or verbs in certain cases. For example, it might be more specific in true positives and vague in false negatives.

7. **Shapley Value Analysis (Model Explainability)**
   - Use techniques like Shapley value or LIME to understand which features ChatGPT considers most important when generating its explanations.

8. **Cosine Similarity**
   - Measure the similarity between explanations across different cases. This can show how much explanations for false positives differ from those for true positives.

9. **Text Classification**
   - Build a classification model to predict which explanation corresponds to which case. This can help identify patterns in ChatGPT’s reasoning.

Among these, we decided to attempt **LDA topic modeling** after discussing with collaborators.

---

## Introduction to LDA Topic Modeling

In natural language processing (NLP), understanding the underlying themes in a set of texts is crucial. One effective method for this is **Latent Dirichlet Allocation (LDA)**. This post explains how LDA works and how we applied it to analyze explanations generated by large language models (LLMs).

### Preprocessing Texts

Before running LDA, it’s important to preprocess the data for consistency and accuracy. For our analysis, we used R to handle preprocessing tasks:

- **Removing Noise**: We eliminated extra spaces and punctuation to reduce noise.
- **Lowercasing**: We converted all text to lowercase for uniformity.
- **Stemming and Lemmatization**: These techniques helped reduce words to their base forms, making the analysis more efficient.

Be mindful that stemming and lemmatization can be time-consuming, especially with social media jargon or encoding issues. Collaboration with social scientists is helpful here to ensure accurate preprocessing.

```r
library(tm)
# create corpus object
corpus <- Corpus(DataframeSource(data.1))

# Preprocessing chain
processedCorpus <- tm_map(corpus, content_transformer(tolower))
processedCorpus <- tm_map(processedCorpus, removeWords, english_stopwords)
processedCorpus <- tm_map(processedCorpus, removePunctuation, preserve_intra_word_dashes = TRUE)
processedCorpus <- tm_map(processedCorpus, removeNumbers)
processedCorpus <- tm_map(processedCorpus, stemDocument, language = "en")
processedCorpus <- tm_map(processedCorpus, stripWhitespace)
```

### Method

1. **Selecting the Number of Topics**: We used metrics like **CaoJuan2009** and **Deveaud2014** from the R package `ldatuning` to determine the optimal number of topics for our analysis.
   
2. **Running the Model**: Once we identified the optimal number of topics, we ran the LDA model to extract the key topics from the LLMs' explanations.
   
3. **Interpreting Results**: The results highlighted the most relevant topics and keywords, providing insights into the decisions made by LLMs.

Here is the code sample :

```r
# compute document term matrix with terms >= minimumFrequency
minimumFrequency <- 1
DTM <- DocumentTermMatrix(processedCorpus, control = list(bounds = list(global = c(minimumFrequency, Inf))))
sel_idx <- slam::row_sums(DTM) > 0
DTM <- DTM[sel_idx, ]
data.1 <- data.1[sel_idx, ]

# create models with different number of topics
# Find k (num of topics)
result <- ldatuning::FindTopicsNumber(
  DTM,
  topics = seq(from = 2, to = 10, by = 1),
  metrics = c("CaoJuan2009",  "Deveaud2014"),
  method = "Gibbs",
  control = list(seed = 77),
  verbose = TRUE
)
FindTopicsNumber_plot(result)  # You should pick the numer of topics with this plot
# number of topics
K <- 3
# set random number generator seed
set.seed(99)
# compute the LDA model, inference via 1000 iterations of Gibbs sampling
topicModel <- LDA(DTM, K, method="Gibbs", control=list(iter = 500, verbose = 25))
# have a look a some of the results (posterior distributions)
tmResult <- posterior(topicModel)
# format of the resulting object
# attributes(tmResult)
nTerms(DTM) 
beta <- tmResult$terms   # get beta from results
dim(beta) 
rowSums(beta) 
nDocs(DTM) 
# for every document we have a probability distribution of its contained topics
theta <- tmResult$topics 
dim(theta)               # nDocs(DTM) distributions over K topics
rowSums(theta)[1:6]   
terms(topicModel,20)

# top5 keywords
top5termsPerTopic <- terms(topicModel, 20)
topicNames <- apply(top5termsPerTopic, 2, paste, collapse=" ") # first 5 keywords
top5termsPerTopic
topicNames
```

### Conclusion

LDA topic modeling offers valuable insights into the structure of text data, helping uncover themes and patterns within LLM explanations. By carefully preprocessing the texts and selecting the right parameters, we derived meaningful topics that reflect how these models make decisions.

---

### References

- Murzintcev, Nikita. n.d. “Select Number of Topics for LDA Model.” [CRAN](https://cran.r-project.org/web/packages/ldatuning/vignettes/topics.html).
- Cao Juan, Xia Tian, Li Jintao, Zhang Yongdong, and Tang Sheng. 2009. A density-based method for adaptive LDA model selection. *Neurocomputing* 72, 7–9: 1775–1781. [DOI](https://doi.org/10.1016/j.neucom.2008.06.011).
- Romain Deveaud, Éric SanJuan, and Patrice Bellot. 2014. Accurate and effective latent concept modeling for ad hoc information retrieval. *Document numérique* 17, 1: 61–84. [DOI](https://doi.org/10.3166/dn.17.1.61-84).

### Bonus WordCloud Code

```r
# visualize topics as word cloud
topicToViz <- 1 # change for your own topic of interest
# select to 40 most probable terms from the topic by sorting the term-topic-probability vector in decreasing order
top20terms <- sort(tmResult$terms[topicToViz,], decreasing=TRUE)[1:20]
words <- names(top20terms)
# extract the probabilites of each of the 20 terms
probabilities <- sort(tmResult$terms[topicToViz,], decreasing=TRUE)[1:20]
# visualize the terms as wordcloud
mycolors <- brewer.pal(8, "Dark2")


wordcloud(words, probabilities, random.order = FALSE, color = mycolors)
```