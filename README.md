# Analyzing Reddit's Sentimental Shifts during COVID-19

## Abstract

The COVID-19 pandemic was an emotionally charged event which introduced major changes in people’s lives. In this project, we explore whether the pandemic changed how Reddit users share their thoughts in posts and comments, and which emotions were most dominant in their activities. We want to uncover how the emotions of users during the pandemic might have influenced the sentiments expressed in their activities on the platform.

We aim to compare how people felt through analyzing activities related to COVID on Reddit and how they compare to baseline feelings for activities before the pandemic. We’ll use Distilbert library to give a score per sentiment (anger, sadness, joy, and others) per submission/comment and compare how these scores changed pre-pandemic and during pandemic times.

## Research Questions

1. Primary: What are the dominant emotions expressed by users during the pandemic as compared to before the pandemic? 
2. What are the primary sentiments in comments to COVID-specific posts* and does it differ from the average sentiment score of a pre-pandemic post?

*We find a COVID specific post by filtering all posts that contain words related to COVID. The notebook specifies the details on how this was done.

## Datasets
We will not be using additional datasets, only the Reddit dataset provided to us. 

### Loading and Managing Sizes of Datasets

We are primarily using `text_submissions`, which is a very large file. We store the data for submissions in two data frames, one for pre-covid entries and one for post-covid entries, where the date to split is February 1, 2020. This allows us to deal with smaller dataframes and if we need the full data, we can concatenate them. 

Our DistilBERT model also took a lot of time to assign sentiment scores for each and every submission in the 3 dataframes (pre-covid, post-covid, post-covid covid-related). It was taking way too much time and power from our laptops to do this for the entire post-covid dataframe, so we instead found the sentiments for 175k random submissions, about 37% of the entire dataframe. To avoid having to go through the whole time-consuming process each time, we save these dataframes with processed text_submission information and sentiment scores on our computers as csv files and simply load it up from there.

## Pre-Processing & Cleaning-up Data

We took certain pre-processing steps to clean up, filter, and transform the data and make it more useful for our exploration. Similar to the original paper “Reddit in the Time of COVID”, we removed submissions which can ‘bot’ or ‘mod’ in the author name, case insensitive, to remove bot posts. We also removed submissions whose bodies were [removed] or [deleted] because we cannot analyze those. Similarly, we removed submissions which had NaN or empty titles, self-text, or created_utc because they were not useful to us. Certain columns (['author', 'domain', 'is_self', 'score', 'subreddit']) were also not necessary for our analysis and were dropped. Filtering out these rows and columns also helps us reduce the size of the dataframes. 

## Methods

[DistilBERT](https://huggingface.co/docs/transformers/model_doc/distilbert) is the library that we will be using to give textual data sentiment scores. The model is a smaller, cheaper, and lighter version of BERT and can provide probabilities (between 0-1) or scores indicating the likelihood of certain emotions being present in the analyzed text. The model provides scores for the following emotions based on the text given: sadness, joy, love, anger, fear, surprise.

We will be using this library for exploratory purposes as well as the modeling steps. 
Also, note that when talking about a “post's activity” or “activity” we mean the post's text body.

### Exploratory Analysis and Statistical Summaries

- **Average sentiments of Pre-pandemic Posts:** We thought that it would be interesting to analyze pre-pandemic Reddit activity and treat it as our “baseline” before moving onto analyzing activity during the pandemic. One way of doing this is to get the sentiment score of each pre-pandemic activity for each sentiment and get the average sentiment score across all posts. This can set us the baseline sentiments per activity. We can similarly calculate the average values for activity during the pandemic and compare these averages.
- **Frequency Distribution Analysis:** After getting the average of sentiment scores for pre-pandemic activity, we can count the activities that have higher and lower sentiment scores than the average.
- **Correlations between Sentiments:** Another interesting exploration would be to see how much sentiments correlate to each other. For instance, if plotting sadness and joy we should be able to see a moderate to strong inverse correlation between the two.


### Modeling Approaches

Our goal is to model pre-pandemic submission sentiment scores for each sentiment and see if post-pandemic submission scores follow our models prediction. We wanted to model by simply fitting a best fit polynomial to pre-pandemic data for each sentiment using numpy’s polyfit function. But considering the size of the pre-pandemic sentiment data, and that we had to experiment with multiple polynomial degrees, and do this for each sentiment, this was too expensive for us. But by plotting sentiment scores, we could visually see general trends for pre-pandemic sentiment scores. 

### Visualization techniques

We also created graphs to show how some sentiments correlate with each other. We chose pairs of sentiments that might show an interesting pattern, particularly ones that we thought would have strong correlation, or strong inverse correlation. Plotting the correlations can show patterns or relationships between emotions. It helps in understanding how certain emotions might influence others.

We used pie charts to compare the prominence of certain sentiments before and during the pandemic, as well as specifically Covid-related posts, because sentiments are a categorical nominal data type. We used bar graphs to compare different sentiment averages, such as a stacked bar graph to show the number of submissions which were higher or lower than the average sentiment pre-pandemic and a bar graph that compares average sentiment in an average submission during the pandemic vs an average Covid-related submission.

Finally, for each sentiment we plot the sentiment scores of the `title` of the submissions across pre-pandemic and pandemic periods. This allows us to notice any trends and patterns present in the pre-pandemic sentiment data and compare these trends to those present in pandemic sentiment data. We can do this using the modeling approaches explained previously. Ideally, we wanted to do this for the `selftext` column which contains the body of the submissions as well, but the sentiment model had a limit to the number of characters
it could process and a lot of the submissions had bodies of text that went over this limit. We know there is a solution to this problem, but we were limited in time and didn't process the bodies.

## Organization within the team

We got on a call together at the beginning to brainstorm our ideas and split up tasks. We split up the tasks based on who will be tackling which research question or which of the visualizations that we have discussed, such as Fariha works on the pie charts for primary sentiments while Ava works on modeling sentiments over time. The person who does a specific visualization writes about it in the README or data story while we both answer the other sections.

