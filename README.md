# Will it Sort?

An NLP exploration of the wilds of Reddit. You have been warned.



___
### Goals

Can you take a post from a subreddit and determine which of two different subreddits it came from?

I will examine a post and through logistic regression determine which of two subreddits it came from.

Success will be measured by accuracy of both the train and the test set.



---
### Audience

This is intended for those individuals who are interested in NLP and Logistic Regression, namely, my fellow DSI plebes.



---
## Overview

I collected data from two fairly disparate subreddits, ran them through some basic NLP preprocessing, and then used either Logist Regression or a Naive Bayes classifier. The results were under-whelming.

I then went back to reddit to get several additional subreddits to compare them. Each subreddit was a subset of the subject matter, in this case, football (soccer for you non-metric types). Soccer > MLS > SoundersFC. SoundersFC is a team in the MLS, and the MLS is a league in the greater world of soccer.

This was still pretty overfit and highly accurate on training, so I decided to try a different route.

r/TalesFromRetail and r/TalesFromYourServer are both story based tales of customer interactions, albeit from two different industries.

Results were very similar.

Once more back to Reddit we go. This time, r/bartenders and r/TalesFromYourServer. Both are story based, customer service, and food service based.

This time I got results that were much worse. 

I used this set of data to tune the model on with GridSearch.

Once the best set of hyperparmateres was found, I used those on the original set of data, r/soccer and r/motorcycles.

It did not fit well. 

Running GridSearch resulted in a very different set of hyperparameters.


___

## Take-aways

1. Hyperparameters matter
    - The correct hyperparameters make a significant impact on the ability of the model to properly fit the data. While all the data was text, the sources of that text made a difference as well. 
2. Different matters.
    - When I looked at the top predictors for the bikes vs ball regression, the top terms were very different and very unique to the subject matter, which goes quite a ways to explaining how I got a $R^2$-score of 1.0 on one of my models.
3. Vectorizers didn't matter much
    - I did not see a lot of difference bewteen the various vectorizers. However, I had a pretty small set of data to work with. The reading and investigating I did indicated that at least an order of magnitude greater in the number or words would be useful.
4. NaiveBayesMN was surprisingly robust
    - Naive Bayes produced pretty good results. I didn't tune to see if I could get better results. Time limitations and all that.
5. Multi-class vs. Binary Logistic Regression
    - Didn't seem to make a difference. Again, I didn't tune, as there was that whole time limitations thing.
6. Size matters
    - DATA DATA DATA DATA. I needed more. Looooooots more.

___

### Technical Details


#### Directory Structure

```
project-3
|__ notebooks
|   |__ 01_Data_Collection.ipynb   
|   |__ 02_EDA_and_Modeling.ipynb   
|   |__ 03_Visualizations.ipynb 
|__ datasets
|   |__ bar.csv
|   |__ fb.csv
|   |__ mc.csv
|   |__ mls.csv
|   |__ ssfc.csv
|   |__ tfr.csv
|   |__ tfys.csv
|__ assets
|   |__ football_mask.jpg
|   |__ football_wc.jpg
|   |__ footballmask_wc.jpg
|   |__ motorcycle_mask.jpg
|   |__ motorcycle_wc.jpg
|   |__ motorcyclemask_wc.jpg
|__ project_03_slides.pdf
|__ README.md
```


#### Data Dictionary
| Column | Type   | Description                            |
|--------|--------|----------------------------------------|
| title  | object | The title of the subreddit post        |
| text   | object | The text of the subreddit post         |
| author | object | The reddit user id                     |
| sub    | object | The subreddit the post was pulled from |
