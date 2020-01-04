# NLP Auhorship Detection

**Problem** 

Having texts from two song writers, detect the authorship of a new sample.


**Approach**

1. Preprocess the samples 
* clean the documents from apostrophes which were misleading the tokenizer
* tokenize into words
* lemmatize the words to consider different forms of the same word as one; use pymorphy2 morphological analyser github.com/kmike/pymorphy2/issues/80 that works with Ukrainian language, as our data is all in Ukrainian
2. Extract features 
* build a vocabulary from all the texts we have
* use bag-of-words technique to store the cout of words (present in vocabulary) computed with the Term-Frequency Inverse Document-frequency (TF-I-DF). TF-I-DF helps to avoid over-weighting the topic-specific words or some frequently-used parts of speech by assuming that a less-frequent word is more important to the text than a typical one.

3. Train and evaluate several cassifiers to determint a better model for this task.
4. Writeup on the outcomes :arrow_down:


**Writeup**

Whichever feature extraction technique we are using, the input for NLP model is usually very high dimensional. This causes deteriorated performance in many classifier models which are assuming that features are independent. For NLP tasks, however, the features (e.g. word occurrence) actually may have covariance - due to natural sentence hierachy and some common phrases used in texts. Moreover, such  type of data often suffers from an empty space phenomenon (as more data is needed to 'fill' its space for a decent training - otherwise some sampes could be seen as outliers, and some cases could be underrepresented).

The first model that comes to mind that could deal with the problems above is Support Verctor Machine (SVM). It still works good in high-dimentional space because it doesn't use all the saples (vectors in the space) for the hyperplane - but only the support vectors which help to separate the classes.

And, as you can see with the AUC scores, the sklearn.svm.SVC (SVM model implementation with linear kernel by default) is performing better than other models. 

Another theoretically good algorithm choice could be the Random Forest model, but it didn't quite confirmed with only 0.78 AUC score on average.  

I aslo tried some other models to check if some would surprisingly turn out to work better on our specific dataset, but SVM still kept it's championship :)  
