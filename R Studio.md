# sentiment-analysis-for-tweets
Project on how the tweets impact the stock market. We have imported tweets from S&P 500 companies and we want to apply sentiment analysis using R Studio.

> # Read file
> fb <- read.csv(file.choose(), header = T)
> str(fb)
'data.frame':	7 obs. of  1 variable:
 $ tweets: Factor w/ 7 levels "i cant sleep",..: 5 4 7 6 2 3 1
> 
> # Build corpus
> library(tm)
> corpus <- iconv(fb$text, to = "utf-8")
> corpus <- Corpus(VectorSource(corpus))
> 
> # Clean text
> corpus <- tm_map(corpus,tolower)
> 
> corpus <- tm_map(corpus, removePunctuation)
> 
> corpus <- tm_map(corpus, removeNumbers)
> 
> cleanset <- tm_map(corpus, removeWords, stopwords('english'))
> 
> removeURL <- function(x) gsub('http[[:alnum:]]*', '', x)
> cleanset <- tm_map(cleanset, content_transformer(removeURL))
> 
> cleanset <- tm_map(cleanset, stripWhitespace)
> 
> # Sentiment analysis
> library(syuzhet)
> library(lubridate)
> library(ggplot2)
> library(scales)
> library(reshape2)
> library(dplyr)
> 
> # Read file
> fb <- read.csv(file.choose(), header = T)
> tweets <- iconv(fb$text, to = "utf-8")
> 
> # Obtain sentiment scores
> s <- get_nrc_sentiment(tweets)
Error in `[.data.frame`(result_df, , my_col_order) : 
  undefined columns selected
> 
> # Bar plot
> barplot(colSums(s),
+         las = 2,
+         col = rainbow(10),
+         ylab = 'Count',
+         main = 'Sentiment Scores for Tweets')
Error in is.data.frame(x) : object 's' not found

