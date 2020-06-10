# Sentiment Analysis of Covid-19 Related Tweets based on Geographic Location and State Policies

#### Authors: Steve Diamond [(GitHub)](ttps://github.com/ssdiam2000), Markell Jones-Francis [(GitHub)](https://git.generalassemb.ly/markelljones-francis), and Julia Kelman [(GitHub)](https://git.generalassemb.ly/julia-kelman/)

## Problem Statement

The COVID-19 response has been largely regional and state-based in nature. Some states have enacted strictly enforced stay-at-home policies, while others have provided guidelines. Now, some states are rapidly moving to reopen while others are following scientific guidelines and moving towards reopening very deliberately. While data concerning the number of Covid-19 cases and deaths has been reported for each state and analyzed based on the states' policies on social distancing, little information is known about the relationship between those features and individuals' sentiments about the pandemic. To get a full picture of the U.S.'s response to the coronavirus,  there is a need to look at the sentiment analysis of social media posts across geographic regions and compare them to both the local policies on social distancing and the occurrences of the pandemic in those areas.   

In order to gain a deeper understanding of the relationship between sentiment and location, we will compare the sentiment of residents in New York and Texas, two large states on opposite ends of the political spectrum whose state governments have acted very differently in terms of the crises. More specifically, we will map the sentiment score based on Covid-19 related posts on Twitter between April 28th and May 6th, 2020 across New York and Texas counties. In addition, we will build two different models using Covid-19 occurences, population, and state policy information in an effort to identify features which drive sentiment:
- A regression model predicting the sentiment score of New York and Texas residents with the highest R-squared score and interpretability possible. 
- A classification model predicting whether a post on Twitter has a positive, neutral, or negative sentiment with the highest accuracy and interpretability possible.  
 
## Executive Summary
COVID-19 is hitting the United States to varying degrees in different parts of the country and state/local governments have not been very consistent in their reactions to the pandemic. Our team of data scientists was tasked with using social media posts to understand the relationships between citizen sentiment and the COVID-19 case loads, deaths and public policy in their local areas.
To accomplish this problem, we did the following:
1. Data Gathering
    - A list of approximately 13,400 U.S. Twitter posts dated between April 28th and March 6th in 2020. These tweets, which contained terms related to Covid-19, were compiled by Rabindra Lamsal, a data scientist at Jawaharlal Nehru University in New Delhi
        * The data was run through TextBlob, a Python library for processing textual data and a sentiment score was appended to each record.
        * The Twitter data was removed, leaving the sentiment score and a tweet ID number.
    - COVID-19 case & death by state/county data from The New York Times.
    - Population from 2019 Census
    - Population density data from simplemaps.com.
    - Mobility trends data from Apple Maps.
1. Data Processing
    - Tweet IDs were used to retrieve the tweet information using webscraping
    - Our team identified New York and Texas representative large states with somewhat differential public policy and COVID case data. We then narrowed our data down to 1,727 posts from these two states TX.
    - COVID-19 data regarding infection rates, deaths and testing were combined with the Twitter data, along with several pieces of data engineered to represent the differences that we found between the states (and, where applicable, between counties).
    - We also incorporated data for popluation, population density and data from Apple Maps concerning the driving mobility of New Yorkers and Texans during this time.
1. Exploratory Data Analysis & Data Mapping
    - We used a variety of methods to discover broad trends in our data, inlcuding examinations of:
        * User engagement with the tweets.
        * Tweet content analysis.
        * Plotting maps which looked at a combination of tweet locations and COVID data.
1. Modeling and Evaluation
    - We used regression modeling, attempting to predict sentiment score, using R-Squared as our metric.
    - We also used classification modeling, attempting to predict if a tweet would have a positive, neutral or negative sentiment score, using accuracy as our metric.
    - 
## Data Sources:
[Tweet dataset from IEEE](https://ieee-dataport.org/open-access/corona-virus-covid-19-geolocation-enabled-tweets-dataset)  
[New York Times Information on COVID-19 Cases](https://www.nytimes.com/interactive/2020/us/coronavirus-us-cases.html)  
[Mobility Data from Apple](https://www.apple.com/covid19/mobility)  
[Information on US Cities](https://simplemaps.com/data/us-citiesResources)  
[2019 Census Population](https://www2.census.gov/programs-surveys/popest/datasets/2010-2019/counties/totals/)  

### Data Dictionary 
|**Feature Name**|**Description**|
|:---|:---|
|all_gatherings_prohibited|Indicator variable - 1 if all gatherings prohibited in county|
|businesses_reopening|Indicator variable - 1 if state has reopened businesses|
|city|Twtter user's city name|
|state|Twitter user's state name|
|county|Twtter user county name|
|county_cases|Cumulative number of Covid 19 cases in user's county on the date of the tweet|
|county_deaths|Cumulative number of Covid 19 deaths in user's county on the date of the tweet|
|county_fips|Standard ID number for user county location|
|county_population|Population of user's county|
|date|Date of tweet|
|density|Population density of city|
|hashtags|List of hashtags in tweet (later eliminated)|
|likes|Number of likes for tweet|
|percent_average_mobility_decrease|Mobility decrease vs. 1/13/2020 per Apple Maps|
|replies|Number of replies for tweet|
|retweets|Number of retweets for tweet|
|screen_name|Twitter user screen name|
|sentiment_score|Sentiment score from TextBlob|
|shelter_in_place|Indicator variable - 1 if shelter_in_place order in effect for county|
|state_cases|Cumulative number of Covid 19 cases in user's state on the date of the tweet|
|state_deaths|Cumulative number of Covid 19 deaths in user's state on the date of the tweet|
|state_fips|Standard ID number for user state location|
|state_name|Replaced by is_nys feature|
|state_population|Population of user's state|
|state_stay_at_home|Indicator variable - 1 if statewide stay-at-home order in place|
|temporary_hospitals|Indicator variable - 1 if state has created temporary hospitals|
|tests_per_thousand|Number of tests per thousand in state conducted by 4/28|
|test_positives_rate|Percent of the tests in state conducted by 4/28 that were positive|
|text|Text of tweet (which includes hashtags)|
|timestamp|Timestamp of tweet, including date and time|
|traveler_quarantines|Indicator variable - 1 if state has had traveler quarantines|
|tweet_id|Tweet ID number - used to identify and hydrate tweets|
|username|Twitter user username|

## Conclusion
Contrary to our initial assumptions, New York and Texas were highly similar in the overall sentiments of their Twitter posts regarding the Covid-19 pandemic. In fact, a majority of the most common words were used in tweets from both states. While there was a greater distinction in the most commonly used words between positive and negative tweets, there was still a high degree of overlap as tweets with positive and negative sentiment shared 19 of the 30 most common words.

Much of the similarity between tweets from the two states can be attributed to the sampling of the tweets and the skewness of the active Twitter userbase. For example, most of the tweets collected for our analysis were concentrated in and around major metropolitan hubs. This, combined with the younger, more politically left-leaning composition of Twitter’s userbase, more than likely narrowed the spectrum of opinions available in our dataset. These limitations led to a very small amount of variance across our target variable – sentiment score – and resulted in a model with features that accounted for less than 2% of the variance in our target and was unable to detect variance when predicting using our test data.

Furthermore, it is our conclusion that the tweet information, location, and corresponding Covid-19 data are far too limited to accurately predict the sentiment score of a tweet because of the multitude of outside factors that may influence a given Twitter user’s opinion of the pandemic and their response to it on a public forum.    

Moving forward, to expand upon our analysis and build a better predictive model, we would need to expand the variance of our dataset by including a greater number of posts from users in more states, and across various social media platforms. If possible, we could improve analysis and predictive capability with the addition of personal information – including political leanings – from the user of a given post. 

## References

[Twitter Users Political Affiliation](https://www.pewresearch.org/internet/2019/04/24/sizing-up-twitter-users/pdl_04-24-19_twitter_users-00-03/)    
[Twitter Users Age, Education, Wealth](https://www.pewresearch.org/internet/2019/04/24/sizing-up-twitter-users/pdl_04-24-19_twitter_users-00-04/)    
[May 6th NYS Deaths](https://www.nbcnewyork.com/news/coronavirus/subway-shutdown-begins-infection-rates-spike-outside-new-york-amid-devastating-toll-at-home/2404295/)  
[Stay at Home Order Information](https://abcnews.go.com/US/list-states-stay-home-order-lifts/story?id=70317035)  
[Twitterscraper library used to retrieve tweets](https://github.com/taspinar/twitterscraper)  
