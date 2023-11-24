# Analyzing Reddit's Sentimental Shifts during COVID-19

## Abstract

The COVID-19 pandemic was an emotionally charged event which introduced major changes in people’s lives. In this project, we explore whether the pandemic changed how Reddit users share their thoughts in posts and comments, and which emotions were most dominant in their activities. We want to uncover how the emotions of users during the pandemic might have influenced the sentiments expressed in their activities on the platform.

We aim to compare how people felt through analyzing activities related to COVID on Reddit and how they compare to baseline feelings for activities before the pandemic. We’ll use Distilbert library to give a score per sentiment (anger, sadness, joy, and others) per submission/comment and compare how these scores changed pre-pandemic and during pandemic times.

## Research Questions

1. Primary: What are the dominant emotions expressed by users during the pandemic as compared to before the pandemic? 
2. Did some subreddits show more shifts in sentiments compared to others during the pandemic?
3. What are the primary sentiments in comments to COVID-specific posts* and does it differ from the average sentiment score of a pre-pandemic post?

*We find a COVID specific post by filtering all posts that contain words related to COVID. The notebook specifies the details on how this was done.

## Datasets
We will not be using additional datasets, only the Reddit dataset provided to us. 

### Loading and Managing Sizes of Datasets

We are primarily using text_comments and text_submissions, which are very large files. text_comments.csv is especially large and in order to load it, we first load it in chunks and process the data before putting it in data frames. Then, we try to make each chunk smaller by dropping unneeded columns, like score, and some of our data cleaning techniques, such as our removal of bot or deleted comments, reduce the size as well. We also store the data for comments and submissions in two data frames each, one for pre-covid entries and one for post-covid entries, where the date is February 1, 2020. This allows us to deal with smaller dataframes and if we need the full data, we can concatenate them. Additionally, to avoid having to go through the whole time-consuming process each time, we save the data frames on our computers as csv files and simply load it up from there because they are much smaller in size than the original csv files.

## Pre-Processing & Cleaning-up Data

We took certain pre-processing steps to clean up, filter, and transform the data and make it more useful for our exploration. Similar to the original paper “Reddit in the Time of COVID”, we removed comments which can ‘bot’ or ‘mod’ in the author name, case insensitive, to remove bot comments. We also removed comments whose bodies were [removed] or [deleted] because we cannot analyze those. Similarly, we removed submissions which had nan titles or self-text because they were not useful to us. Filtering out these rows also helps us reduce the size of the dataframes. 

## Methods

[DistilBERT](https://huggingface.co/docs/transformers/model_doc/distilbert) is the library that we will be using to give textual data sentiment scores. The model is a smaller, cheaper, and lighter version of BERT and can provide probabilities (between 0-1) or scores indicating the likelihood of certain emotions being present in the analyzed text. The model provides scores for the following emotions based on the text given: sadness, joy, love, anger, fear, surprise.

We will be using this library for exploratory purposes as well as the modeling steps. 
Also, note that when talking about a “post's activity” or “activity” we mean the post's text body and its comments.

### Exploratory Analysis and Statistical Summaries

- **Average sentiments of Pre-pandemic Posts:** We thought that it would be interesting to analyze pre-pandemic Reddit activity and treat it as our “baseline” before moving onto analyzing activity during the pandemic. One way of doing this is to get the sentiment score of each pre-pandemic activity for each sentiment and get the average sentiment score across all posts. This can set us the baseline sentiments per activity. We can similarly calculate the average values for activity during the pandemic and compare these averages.
- **Frequency Distribution Analysis:** After getting the average of sentiment scores for pre-pandemic activity, we can count the activities that have higher and lower sentiment scores than the average. This can, for instance, roughly show us if there is a huge increase in posts with a higher than average sadness score or with a lower than average joy score. If these changes are significant enough, we may reason that they might be due to COVID as an emotionally charged event. 
- **Correlations between Sentiments:** Another interesting exploration would be to see how much sentiments correlate to each other. For instance, if plotting sadness and joy we should be able to see a moderate to strong inverse correlation between the two.

### Modeling Approaches

In the paper “Reddit in the Time of COVID”, they trained using the model Prophet on the data pre-covid and predicted the activity from Feb 1 2020 (the assumed start time of COVID) onwards. In our case, we will also use Prophet to train the data based on each sentiment, such as joy and sadness, in order to see the trends of pre-Covid comments and posts on a monthly basis. Then, we will use the model to predict the trajectory of each sentiment and compare it with the real sentiments from the data Feb 1, 2020 onwards.

### Visualization techniques

We will use line graphs to track the trajectory of different sentiments across the months, as well as the pandemic predictions from Prophet. We can use bar graphs (including stacked), area charts, or pie charts to compare the prominence of certain sentiments before or during the pandemic because sentiments are a categorical nominal data type. We used scatter plots to display the correlation between different sentiments for a segment of pre-pandemic post titles, we can also implement this idea for post-pandemic Reddit posts and comments. 

## Organization within the team

We got on a call together at the beginning to brainstorm our ideas and split up tasks. We try to split up the work so that it’s not completely dependent on one person to finish their task for the other person to progress but if this happens, the person who can’t proceed works on the writing portion, such as the README.

