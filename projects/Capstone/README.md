# General Assembly DSI Capstone: Music Rating Predictor

This project is based on a Kaggle competition sponsored by EMI back in 2012, which seeks to estimate how much a listener will like a new song (on a scale from 0-100) based on their demographic information, music habits, and how their ratings for other artists.

Through undertaking this analysis, I realized just how many ways there are to handle the high number of missing values in the dataset. A portion of the dataset, words.csv, features 82 words that interviewees use to describe artists that they have just heard. These include words like edgy, fun, exciting, boring, talented, etc. However, not all of these words were used in each interview given. As a result, many null values exist for each listener listed in the dataset. Null values can complicate the data analysis process, and how I handle them can impact my findings.

Therefore, this analysis is broken out into three sets of notebooks, each outlining an alternative approach to handling the missing data in words.csv and the other EMI data:

        1) Categorizing the 82 words in words.csv into 11 categories, then dropping any rows in the larger dataset with null values. In each category, if a user marks a 1 for any word in the category (marking "yes, the artist sounds like this word"), then the overall category is marked with a 1. If no words are marked with a 1, the category receives a 0. This approach is meant to not overweight any categories with words that have more words (and therefore more potential 1's) than other categories.
        2) Same approach as above, but using the _fraction_ of words marked with 1 over total words in the category. This approach is meant to give more weight to categories that have more words with 1's than others. In addition, I then impute any remaining null values with the mean value of their respective column.
        3) I do not categorize any words but drop any columns that have less than less than 100,000 non-null values (~47% missing data). This drops 39 features of more than 100. I then impute any remaining null values with the mean value of their respective column.

Since the Kaggle competition was judged based on root mean squared error, I am judging my three approaches using the same metric:
- Approach 1: 15.19
- Approach 2: 14.86
- Approach 3: 14.81

In all three approaches, the words listeners used to describe (or in the case of Approach 1 and 2, the categories they selected) tended to have the largest impact on the outcome of the rating. This seems intuitive, given that a word used to describe an artist will likely indicate how I feel about it. If I think something is "bad," I'm probably going to give it a low rating.

Moving forward, there are a slew of directions to take this. First and foremost, these are not the only ways to handle null values. In addition, the model should be improved so that is trained on only the listener ID, artist ID, track ID, track rating, and time the survey was given. Doing so will likely involve some hybrid of a recommendation system and regression. Additionally, the current model's predictions do not capture the "peakiness" of ratings of songs, which peak at ratings of 10, 30, 50, 70, and 90 (what apparently happens when people are given such a wide range to rate on), underestimating ratings at peaks and overestimating in the valleys between. A multimodel approach could address this problem.

So that's about it! Feel free to contact me to discuss my process, findings, problems, etc.

John
