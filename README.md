tweet-stream-globe
==========

A real-time 3D visualization of Tweets from around the world.

This web app attaches to the Twitter standard realtime filter API, and runs rudimentary sentiment analysis on Tweets that have associated geo data. Tweets are then published through PubNub WebSockets, and plotted onto a 3D globe in the browser.

Inspired by the [Web GL Globe Chrome Experiment](http://www.chromeexperiments.com/globe) and the [PubNub Real-Time WebGL Visualization](http://www.pubnub.com/blog/creating-real-time-webgl-visualizations/).

[Screenshot](screenshot.png "Screenshot")
[Video Capture](https://vimeo.com/104759844)

Installing and Running
----

Clone the GitHub repo:

```
https://github.com/twitterdev/twitter-stream-globe.git
```

Create a Twitter app and PubNub account:

- Create a [Twitter application](https://developer.twitter.com/apps) (requires a free, but approved, developer account)
- Create a [PubNub account](https://admin.pubnub.com/#signup) (this is free)

Create a `config.json` file using `config.sample.json` as a template. Fill in your Twitter API and PubNub keys.

Install node module dependencies:

```
npm install
```

Run application:

```
npm start
```

Go to [http://localhost:3000](http://localhost:3000) in your browser.


Remix this!
----

<a href="https://glitch.com/edit/#!/import/github/twitterdev/twitter-stream-globe?TWITTER_CONSUMER_KEY=&TWITTER_CONSUMER_SECRET=&TWITTER_ACCESS_TOKEN=&TWITTER_TOKEN_SECRET=&PUBNUB_PUBLISH_KEY=&PUBNUB_SUBSCRIBE_KEY="><img src="https://cdn.glitch.com/2703baf2-b643-4da7-ab91-7ee2a2d00b5b%2Fremix-button.svg" alt="Remix on Glitch" /></a>
You will need to populate the environment variables in the `.env` file for this to work


Deploying to other cloud services
----
This application should be ready to run on free Cloud Foundry, OpenShift or Heroku accounts.

**Heroku**

You can deploy to Heroku via [Git](https://devcenter.heroku.com/articles/git) with the [Heroku toolbelt](https://toolbelt.heroku.com/).

Before deploying to Heroku, set your environment [config vars](https://devcenter.heroku.com/articles/config-vars) to mirror `config.json`, and set `NODE_ENV` to "production."

[![image](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy?template=https://github.com/twitterdev/twitter-stream-globe/tree/master)

Tip: Managing the Twitter stream is more appropriately accomplished with a worker or background job. See this [gist](https://gist.github.com/stephenlb/36aef15a165d5bad0d82) for setting up a Twitter / PubNub [worker on Heroku](https://devcenter.heroku.com/articles/background-jobs-queueing). 

**OpenShift**

You can deploy to OpenShift with [`rhc`](https://github.com/openshift/rhc), by adding your own keys to the following command:

```
rhc app create twglobe nodejs-0.10 \
  --from-code=http://github.com/twitterdev/twitter-stream-globe.git \
  NODE_ENV=production \
  TWITTER_CONSUMER_KEY=YOUR_TWITTER_CONSUMER_KEY \
  TWITTER_CONSUMER_SECRET=YOUR_TWITTER_CONSUMER_SECRET \
  TWITTER_ACCESS_TOKEN=YOUR_TWITTER_ACCESS_TOKEN \
  TWITTER_TOKEN_SECRET=YOUR_TWITTER_TOKEN_SECRET \
  PUBNUB_PUBLISH_KEY=YOUR_PUBNUB_PUBLISH_KEY \
  PUBNUB_SUBSCRIBE_KEY=YOUR_PUBNUB_SUBSCRIBE_KEY
```

**Cloud Foundry**

You can deploy to a Cloud Foundry instance with the [`cf`](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html) command line tool.

Copy `manifest.sample.yml` to `manifest.yml`, edit the application name, and then insert your Twitter and PubNub API keys.

Run `cf push` to deploy and start the app on Cloud Foundry.

Resources
----
- [Twitter API statuses/filter stream](https://developer.twitter.com/en/docs/tweets/filter-realtime/api-reference/post-statuses-filter.html)
- [Twitter REST API Rate Limiting](https://developer.twitter.com/en/docs/basics/rate-limiting.html)
- [AngularJS](https://angularjs.org/)
- [PubNub AngularJS SDK](https://github.com/pubnub/pubnub-angular)
- [Three.js](https://threejs.org/)
