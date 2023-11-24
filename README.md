# Analyzing Reddit's Sentimental Shifts during COVID-19

**Abstract**: 

The COVID-19 pandemic was an emotionally charged event which introduced major changes in people’s lives. In this project, we explore whether the pandemic changed how Reddit users share their thoughts in posts and comments, and which emotions were most dominant in their activities. We want to uncover how the emotions of users during the pandemic might have influenced the sentiments expressed in their activities on the platform.

We aim to compare how people felt through analyzing activities related to COVID on Reddit and how they compare to baseline feelings for activities before the pandemic. We’ll use Distilbert library to give a score per sentiment (anger, sadness, joy, and others) per submission/comment and compare how these scores changed pre-pandemic and during pandemic times.

**Research Questions**:

1. Primary: What are the dominant emotions expressed by users during the pandemic as compared to before the pandemic? 
2. Did some subreddits show more shifts in sentiments compared to others during the pandemic?
. What are the primary sentiments in comments to COVID-specific posts (*) and does it differ from the average sentiment score of a pre-pandemic post?
(*) We find a COVID specific post by filtering all posts that contain words related to COVID. The notebook specifies the details on how this was done.

**Datasets**:
We will not be using additional datasets, only the Reddit dataset provided to us. 

*Loading and Managing Sizes of Datasets*

We are primarily using text_comments and text_submissions, which are very large files. text_comments.csv is especially large and in order to load it, we first load it in chunks and process the data before putting it in data frames. Then, we try to make each chunk smaller by dropping unneeded columns, like score, and some of our data cleaning techniques, such as our removal of bot or deleted comments, reduce the size as well. We also store the data for comments and submissions in two data frames each, one for pre-covid entries and one for post-covid entries, where the date is February 1, 2020. This allows us to deal with smaller dataframes and if we need the full data, we can concatenate them. Additionally, to avoid having to go through the whole time-consuming process each time, we save the data frames on our computers as csv files and simply load it up from there because they are much smaller in size than the original csv files.

*Pre-Processing Tasks*

We took certain pre-processing steps to clean up, filter, and transform the data and make it more useful for our exploration. Similar to the original paper, we removed comments which can ‘bot’ or ‘mod’ in the author name, case insensitive, to remove bot comments. We also removed comments whose bodies were [removed] or [deleted] because we cannot analyze those. Similarly, we removed submissions which had nan titles or self-text because they were not useful to us. Filtering out these rows also helps us reduce the size of the dataframes. 

**Methods**:

**Organization within the team**:
We got on a call together at the beginning to brainstorm our ideas and split up tasks. We try to split up the work so that it’s not completely dependent on one person to finish their task for the other person to progress but if this happens, the person who can’t proceed works on the writing portion, such as the README.

