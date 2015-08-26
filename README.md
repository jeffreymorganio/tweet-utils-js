# tweet-utils-js

**tweet-utils-js** is a JavaScript library of functions for working with tweets in JSON format return by the [Twitter API](https://dev.twitter.com/rest/public).

## Installation

```
npm install tweet-utils-js
```

## Use

```
var TweetUtils = require('tweet-utils-js');

var aTweet = ...; // A JSON-format object retrieved from the Twitter API

// Geocoding
var geoCoding = TweetUtils.extractGeocoding(aTweet);

// User Mentions
var userMentions = TweetUtils.extractUserMentions(aTweet);

// Hashtags
var hashtags = TweetUtils.extractHashtags(aTweet);

// Retweets
if (TweetUtils.isRetweet(aTweet)) {
  // do something with the retweet
}
```

## API

**extractGeocoding**([*tweet*])

Returns the geocoded location in a tweet as an object with `latitude` and `longitude` keys, or `null` if the tweet is `null` or does not contain a geocoded location. This function returns an object with keys that explicitly label the latitude and longitude values to avoid the confusing and error-prone use of two-element arrays. Example output:

```
{
  longitude: 51.500152,
  latitude: -0.126236
}
```

**extractUserMentions**([*tweet*])

Returns an array of the Twitter-user screen names mentioned in a tweet (without the @ prefix). The array will be empty if the tweet is `null` or does not mention any Twitter users. For example, the output for the tweet:

> @BBCNews and @CNN are reporting the story live.

would be:

```
['BBCNews', 'CNN']
```

**extractHashtags**([*tweet*])

Returns an array of the hashtags used in the text of a tweet (without the # prefix). The array will be empty if the tweet is null or does not contain any hashtags. For example, the output for the tweet:

> It's great to #opensource your #nodejs code!

would be:

```
['opensource', 'nodejs']
```

**isRetweet**([*tweet*])

Returns `true` if the tweet is a retweet. A tweet is retweeted when users press the retweet button of a Twitter user interface or when they prefix the tweet text with "RT" or "RT:". For example, the output for the following tweets would be `true`:

> RT @BBCNews and @CNN are reporting the story live.

> RT: @BBCNews and @CNN are reporting the story live.

In constrast, the output for the following tweet would be `false`:

> @BBCNews and @CNN are reporting the story live.
