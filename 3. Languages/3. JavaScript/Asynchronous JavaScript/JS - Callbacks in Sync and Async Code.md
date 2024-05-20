### What is a callback function
* A function that is passed through another function, from which it's called later
* Can be anonymous or passed by name

# Examples: Synchronous Callbacks
* Synchronous Callback
```js
const tweets = [
  "some weird thread",
  "a reply to Marissa Mayer's tweet",
  "reaction to breaking news"
];

// anoynmouys function calls
tweets.forEach((tweet) => {
    console.log(tweet);
}); 
```

```js
const tweets = [
  "some weird thread",
  "a reply to Marissa Mayer's tweet",
  "reaction to breaking news"
];

function consoleTweet(tweet) {
    console.log(tweet);
}

// named function call
tweets.forEach(consoleTweet); 
```

* Working with multiple callbacks
```js
// this function will be passed as a callback and executed if the tweetContainer isn't found to create a new container and add the tweet
function createTweet(tweet) {
	const newTweetContainer = document.createElement("div");
	newTweetContainer.textContent = tweet;
	document.body.append(newTweetContainer);
}

// add a third parameter, which is a callback
function insertTweet(tweet, containerSelector, callbackFn) {
	// Select the cotiner
    const tweetContainer = document.querySelector(containerSelector);
    // If the right container isn't found, execute the callbackFn
    if (!tweetContainer) {
        callbackFn(tweet);
        return;
    }
    // if the container is found, add the tweet to it
    tweetContainer.textContent = tweet;
}

// the call will look like this:
insertTweet("a reply to Marissa Mayer's tweet", ".tweets", createTweet); 
```

# Examples: Asynchronous Callbacks