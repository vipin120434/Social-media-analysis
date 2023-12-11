import tweepy
from textblob import TextBlob

# Twitter API credentials
consumer_key = 'your_consumer_key'
consumer_secret = 'your_consumer_secret'
access_token = 'your_access_token'
access_token_secret = 'your_access_token_secret'

# Set up Tweepy API authentication
auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)
api = tweepy.API(auth)

# Function to perform sentiment analysis using TextBlob
def analyze_sentiment(tweet):
    analysis = TextBlob(tweet)
    # Classify the polarity of the tweet
    return 'Positive' if analysis.sentiment.polarity > 0 else 'Negative' if analysis.sentiment.polarity < 0 else 'Neutral'

# Function to fetch and analyze tweets
def fetch_and_analyze_tweets(query, count=10):
    tweets = tweepy.Cursor(api.search, q=query, lang='en', tweet_mode='extended').items(count)

    for tweet in tweets:
        print(f'Tweet: {tweet.full_text}')
        print(f'Sentiment: {analyze_sentiment(tweet.full_text)}')
        print('-' * 30)

# Example usage
if __name__ == "__main__":
    search_query = 'Python programming'  # Change this to your desired search query
    fetch_and_analyze_tweets(search_query, count=5)
