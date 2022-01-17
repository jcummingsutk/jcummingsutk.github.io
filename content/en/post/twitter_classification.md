---
#date: 2021-04-09T10:58:08-04:00
#description: ""
featured_image: "/images/twitter.jpg"
#tags: ["scene"]
title: "Analyzing Twitter Data (Currently in Progress)"
---
This is a project that I am currently working on. Here is an image of a wordcloud of the positive tweets from me protoyping the model where, using [tweepy](https://www.tweepy.org/), I query twitter on the topic of "Atlanta". It happened to be MLK day the day that I tested it.

![Positive Tweets](/images/twitter_atl_positive.png)

**Goal**: Using a recurrent neural network (RNN) developed with tensorflow, develop an application that can identify a sentiment of a tweet and make this available as a flask application on Amazon's web service elastic beanstalk.

Useful links:
[GitHub Page](https://github.com/jcummingsutk/ung_twitter_sentiment)

[Jupyter Notebook](https://github.com/jcummingsutk/ung_twitter_sentiment/blob/master/notebook.ipynb)

[Twitter Sentiment Data](https://www.kaggle.com/kazanova/sentiment140)

**Results**: Currently the RNN has been built and using tweepy tweets can be collected on a particular topic. The model has been saved and is ready to be implemented on a flask application on Amazon's elastic beanstalk.
