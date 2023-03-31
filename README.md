![image](https://github.com/jswec/Phase4/blob/main/plots_and_images/appletwitter.jpeg)

# Sentiment Analysis for Apple Inc.

---

Authors: [Ryan Moore](github.com/mooreaz92), [Diego Fernandez](github.com/dmf1998), [Albert Chen](github.com/albertcchen), [Jake Swecker](github.com/jswec)

---

## Background

The dataset was provided by [CrowdFlower](https://data.world/crowdflower/brands-and-product-emotions) on August 30, 2013. Contributors evaluated tweets about Apple, Google, and unknown brands/products and if these tweets expressed positive, negative, or no emotions.

---

## Business Problem

There is an analytical inefficiency of social media sentiment analysis if this process is manual. According to recent findings, there are approximately 500 million tweets shared daily. Going through all of these tweets manually would be time consuming and ultimately costly for a company. Therefore we plan to train and determine what model plus which features we can use to automatically predict sentiment from the tweets.

---

## Data Review

Our initial dataset consisted of 9,093 rows of tweet data, what product the emotion in the tweet is directed at, and what the emotion is for the brand or product. Emotions were manually tagged by CrowdFlower and used as our target mainly ranging from negative, neutral, and positive emotion. The tweets appear to contain data on mainly Apple or Google products/applications and seem to have been collected during the 2010 South by Southwest (SXSW) conference in Austin, TX.

---

## Data Cleaning & Feature Engineering

We started by adding columns that would count the amount of mentions and links contained in each tweet row. Next we dropped non-significant values where the emotion was categorized as "I can't tell". Text data was then cleaned by creating a function (clean_text) that was composed of:
- Converting text to lower case
- Removing the uses of via
- Removing html syntax from tweet
- Removing urls or instances of links
- Removing words that contained the symbol @ and the RT(retweet)
- Removing the #SXSW hashtag
- Removing punctuation by ignores contraction apostraphes
- Removing stopwords
- Removing non-ASCII chracters
- Lemmatizing the words

We then feature engineered additional columns that identified if the tweets pertained to Google or Apple and approximated these two companies as well based on text from the tweet.

Finally we passed the text through a VADER Sentiment Analyzer which predicted sentiment values ('pos', 'neg', 'neu') from the text and created emphasis columns that scored the number of exclamation points, question marks, and capital letters that are also in the text.

---

## Exploratory Data Analysis

After cleaning our data, we begin exploring the data by comparing the sentiments between Apple versus Google.

![image](https://github.com/jswec/Phase4/blob/main/plots_and_images/emotion_distribution_by_device.png)

Since punctuation as well as capitalization can be used to express emotion, we also wanted to determine if our feature engineered counts of punctuation emphasis and capitalization ultimately contributed to either a negative or positive sentiment rating for the tweet.

![image](https://github.com/jswec/Phase4/blob/main/plots_and_images/emotion_distribution_caps_and_punctuation.png)

We wanted to visualize the top 10 most common words from our cleaned up tweets and see what was most popular from this dataset.

![image](https://github.com/jswec/Phase4/blob/main/plots_and_images/top_10_most_common_words.png)

---

## Modeling

---

### First Simple Model

Our first simple model utilized a Count Vectorizer and a Decision Tree that used only the tokenized tweets without any other features. This was to establish our baseline model.

### Second Model

The second model also used a Count Vectorizer but used Naive Bayes to evaluate our data. For this model we also included sentiment, emphasis scores, and number of links and mentions included in each tweet.

### Third Model

Finally our third model used a TDIF Vectorizer with a Random Forest, including the same features as our second model above.

### Grid Search for Model Tuning

After initially running our three models, we ran them through a grid search to tune the hyperparameters. Once we obtained our results, we evaluated the parameters on our test data.

---

## Analysis and Results

From our analysis, the final model that we went with was the tuned Naive Bayes model that used a Count Vectorizer. The metrics that we used to evaluate these models were F1 scores and accuracy. The Naive Bayes model resulted in the highest F1 and accuracy scores when compared to our other tuned models.

![image](https://github.com/jswec/Phase4/blob/main/plots_and_images/f1_and_accuracy_scores.png)

This model was then deployed and produced word clouds for negative, neutral, and positive sentiments for Apple tweets:

![image](https://github.com/jswec/Phase4/blob/main/plots_and_images/word_clouds.png)

## Recommendations

With our model, we have three proposed recommendations:

**1.** Leak Monitoring - Use this model to gauge public sentiment after an Apple leak. This would allow an opportunity to test the waters for coming features.

**2.** Increased Marketing Productivity - Easy-to-use, user-friendly model that can see widespread adoption

**3.** Competitive Edge - Currently trained on Google products, but we could also apply this modelling to understand overall sentiment on competitor products to see what works well for them and what is not.

## Addition Information

Full review of our notebook can be found [here](https://github.com/jswec/Phase4/blob/main/phase_4_final.ipynb), and our presentation deck can be found [here](https://github.com/jswec/Phase4/blob/main/ADRJ%20-%20Phase%204%20-%20NLP%20Presentation.pdf).

