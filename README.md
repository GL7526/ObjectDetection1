# ObjectDetection
# ** readme to be edited **

<!--
# Finding Toilet Paper
At the time of the project, I've been wanting to find a way to get more familiar with convolutional neural networks. At the same time, a new strain of coronavirus had reached pandemic levels of prevalency. This has caused people to panic buy face masks, hand sanitizer, and toilet paper. As a result, I decided to focus on creating a model that would be able to detect a roll of toilet paper in an image.



<br>

- [Project Goal](#ProjGoal)
- [Cleaning Data](#Preprocessing)
- [EDA](#EDA)
- [The Model](#Model)
- [Potential Improvements](#Improvements)

<br>

## Project Goal <a name = 'ProjGoal'></a>
The goal of this project is to predict the rating of a drug review based on the text.
<br>
<br>
## Preprocessing/Data Cleaning <a name = 'Preprocessing'></a>
Cleaning text data is slightly different from cleaning typical numerical data. The inputs are strings that we want to extract information from. For this set of data, I used nltk's TweetTokenizer to tokenize the data. The benefit of using TweetTokenizer as opposed to nltk's word_tokenize is that the former doesn't split words by apostrophes so a word like "didn't" stays as "didn't" instead of becoming two words "did" and "n't". Now that the data is tokenized, the stop words and punctuation can then be removed. The words were then lemmatized according to their parts of speech to reduce dimensionality and also because I saw no loss of meaning from considering words like "jump" and "jumping" the same, at least here. Finally, I used keras' Tokenizer to transform the data into a matrix of tf-idf values of each word, but keeping only the 5000 most common words to avoid crashing the kernel from using too much memory.
<br>
<br>
## Exploratory Data Analysis <a name = 'EDA'></a>
It's important to look at the data to get a good understanding of it for any dataset, and this is no different. One piece of information that might be interesting is what are the conditions whose drugs have the best and worst rating? To find this out, I calculated the average of the ratings for each condition that occurred at least 500 times, so that the drugs can be fairly represented and so that drugs with only one 1/10 review don't skew the numbers improperly by dropping that drug to the bottom. By doing this, I created the following charts:
<br> <br>
<p align = "center">
<img src = "images/Cond_Best_Rate.png" width = 500></img>
</p>

##
<br>
<p align = "center">
<img src = "images/Cond_Worst_Rate.png" width = 500></img>
</p>
<br>
From this, we can see that drugs for conditions related to the urinary tract are generally bad.
<br>
<br>
One other very important piece of information is the distribution of the classes that are going to be predicted. From the chart below, we can see that most of the ratings are concentrated at the far ends of being 1/10 or 10/10. This may tell us that looking at the extremes is a good representation of the overall data:
<br>

<p align = "center"><img src = "images/Distr_Ratings.png" width = 500></img></p>

##

By looking at the words used in a 1/10 review: 
<br>
<p align = "center">
<img src = "images/wordcloud1.jpg" width = 350></img>
</p>
<br>
and the words in a 10/10 review: 
<br>
<p align = "center">
<img src = "images/wordcloud10.jpg" width = 350></img>
</p>
<br>
We can see that the words, when taken individually, are almost the same. Even the proportions among the sizes of the words, which describe their frequency, is about the same. This tells us that there is barely any difference in the words used throughout the reviews.


## The Model <a name = 'Model'></a>
The model is a neural network that accepts an input vector of length 5000, corresponding to a string after undergoing the same preprocessing as the training data. The output is a vector that whose values are the probability of being each class, which are the ratings 1-10.
<br>
<br>
## Potential Improvements <a name = "Improvements"></a>
Although this project focused on using NLP techniques, we can always incorporate the rest of the information provided in the dataset to improve the model, such as creating dummy variables for each condition. We can also use Word2Vec, which uses continuous bag of words or skip-grams, which better maintains the context of the words.
