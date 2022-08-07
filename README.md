# Project: Wrangle and Analyze Data
We Rate Dogs Data Analysis Using Python
# Introduction
WeRateDogs is a popular tweet handle with over a 9.2million followers(at the time of writing this article) that post and rate pictures of amazing dogs. They are a source for professional dog ratings and are nonprofit. This data set contains information about 864 tweet ids gathered, assessed, and cleaned from WerateDogs using Twitter Api referencing an enhanced Twitter archive file provided by udacity, It contains 864 rows and 22 columns. This information includes ratings, favorite counts, dog stage, source of the tweets, etc.
## Gathering
 Data was gathered from:
1. The enhanced tweet archive of Twitter user @dog_rates, also known as WeRateDogs. This dataset was downloaded as a csv file manually from the udacity workspace and read as a data frame using the pandas read_csv function.
2. The image prediction file, a CSV file downloaded programmatically using the Requests library. This tsv file was read as a data frame.
3. The JSON data(retweet count and favorite count) of all tweet IDs in the enhanced tweet archive file downloaded from Twitter API using the tweepy library. Then JSON file was collected as text was read and passed into a data frame.
## Assessing
After gathering these data, it was assessed visually and programmatically and the issues observed are as follows;

Quality issues according to the gathered datasets.
> ***Twitter Archive***
1. There are tweet ids that are of retweets
2. These Columns: in_reply_to_status_id, in_reply_to_user_id, retweeted_status_id, retweeted_status_user_id, retweeted_status_timestamp are not required for our analysis so we drop them.
3. Expanded_urls has 59 null values (completeness issues)
4. Some entries in the Expanded_urls column have more than one URL in them. (consistency issue)
5. a and None is used for dog name instead of NaN ( these are not valid names).
6. The timestamp has an object as its data type as against DateTime that it should be.
> ***Image Prediction***
1. image num column should be dropped as they are of no use in this analysis
2. Dog predictions that are False in p1_dog, p2_dog, and p3_dog are not dog-related and should be dropped.

Tidiness issues on all the 3 data sets
1. In twitter archive data the dog stages doggo, pupper, puppo, and floofer should be in one column
2. All the data sets should be merged into one.
3. All duplicates and null values are to be dropped.

## Cleaning
The cleaning done to the issues addressed in the assessed stage are as follows;
> ***Quality***
1. Drop rows that do not have null value in retweeted_status_id, retweeted_status_user_id, retweeted_status_timestamp, we do not need them for the analysis.
2. Drop the columns we do not need for the analysis in the archived tweets using the drop function
3. Drop Null values in the expanded_urls column
4. The expanded_urls column was transformed each list-like to a separate row using explode(). This will replicate the index values from the original row and then assign them to the Twitter archive.
5. Replace invalid names with Nan
6. Convert TimeStamp column Datatype to DateTime
7. Drop the img_num column in the Image Prediction data frame
8. Drop dog predictions that are False in p1_dog, p2_dog, and p3_dog as they are not dog-related.
> ***Tidiness***
1. Make the dog stages doggo, pupper, puppo, and floofer into one column using the melt function.
2. Merge all DataFrame into one tidy data
3. Drop Duplicates and Null data.

The merged data was stored as 'twitter_archive_master.csv'
## Questions
1. What name is the top 5 most Common?
2. What are the details of the dog with the least rating numerator?
3. Is there a correlation between the Rating numerator and the likes(favourite) count?
4. What is the least common Dog stage in the data set?
5. What is the frequency of Dog Ratings?
## Insights 
Answers were generated to these questions and it can be said that;
1. According to this data set with unique dog names of six hundred and twenty-seven (627), Cooper, Oliver, Charlie, Sadie, Koda are the 5 most common dog names.
2. The dog is named Crystal, the dog had 2281 retweets and 5006 likes.It is the only dog with that rating numerator of 2.
3. There is a weak positive correlation between the rating numerator and the likes count.
4. Floofer is the least common dog stage in the distribution
5. The ratings twelve (12) happen to be the most common ratings given to dogs
