# Sentiments on Reddit Posts and Comments in the Time of Covid

**Abstract**: 

**Research Questions**:

**Datasets**:
We will not be using additional datasets, only the Reddit dataset provided to us. 

We are primarily using text_comments and text_submissions, which are very large files. text_comments.csv is especially large and in order to load it, we first load it in chunks and process the data before putting it in data frames. Then, we try to make each chunk smaller by dropping unneeded columns, like score, and some of our data cleaning techniques, such as our removal of bot or deleted comments, reduce the size as well. We also store the data for comments and submissions in two data frames each, one for pre-covid entries and one for post-covid entries, where the date is February 1, 2020. This allows us to deal with smaller dataframes and if we need the full data, we can concatenate them. Additionally, to avoid having to go through the whole time-consuming process each time, we save the data frames on our computers as csv files and simply load it up from there because they are much smaller in size than the original csv files.

**Methods**:

**Organization within the team**:
We get on a call together at the beginning to brainstorm our ideas and split up tasks. We try to split up the work so that it’s not completely dependent on one person to finish their task for the other person to progress but if this happens, the person who can’t proceed works on the writing portion, such as the README.
