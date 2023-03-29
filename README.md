![image](https://github.com/jswec/Phase4/blob/main/data/appletwitter.jpeg)

# Sentiment Analysis for Apple Inc.

---

## Background

The dataset was provided by [CrowdFlower](https://data.world/crowdflower/brands-and-product-emotions) on August 30, 2013. Contributors evaluated tweets about Apple, Google, and unknown brands/products and if these tweets expressed positive, negative, or no emotions.

---

## Business Problem

---

## Data Review

9,093 rows

---

## Data Cleaning

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
- Lemmatizes the words

We then feature engineered additional columns that identified if the tweets pertained to Google or Apple and approximated these two companies as well based on text from the tweet.

Finally we passed the text through a VADER Sentiment Analyzer which predicted sentiment values ('pos', 'neg', 'neu') from the text and created emphasis columns that scored the number of exclamation points, question marks, and capital letters that are also in the text.

---

## Modeling

---

### First Simple Model

### Second Model

### Third Model
