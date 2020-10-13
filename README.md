# PUBSUB
This project contains two sub-projects - **publisher** and **subscriber**. They simulate a simple publish/subscribe mechanism using HTTP. Under the hood, both projects run express server, and do HTTP requests using node-fetch.

### Publisher
Publisher containts three endpoints:
```
1. /subscribe - accepts channel (string) and clientUrl (string), and saves this data to redis set
2. /unsubscribe - same as above, but removes data from redis set
3. /publish - accepts channel (string) and message (any), then fetches all client urls for specified channel from redis, and uses HTTP POST to send a request body to all client urls
```

Additionally, publisher will fetch RSS Meteo feed for Europe every 60 seconds, and publish data of each city.

### Subscriber

Subscriber starts express server, which is ready to accept messages from publisher. When message is received, it logs it to console. 

Subscriber is started with ```npm start channelName```. Parameter ```channelName``` can of course have any value, as it's the name of a channel we're subscribing to. When started, subscriber will use HTTP POST to subscribe to a provided channel.


### Example

Starting publisher with ```npm start``` and starting subscriber with ```npm start tirana```, will result in subscriber receiving weather description for Tirana, every 60 seconds.