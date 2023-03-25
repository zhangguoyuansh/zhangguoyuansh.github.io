---
title: 'Ingenious application of session analysis'
date: 2022-01-01
permalink: /posts/2012/08/blog-post-4/
tags:
  - cool posts
  - category1
  - category2
---

Session Analysis: Definition, Meaning, and Indicators
Session is a mechanism we often use to record browser status. Many business colleagues are often very interested in session analysis in user behavior analysis, but there are many misunderstandings about the definition and application scenario of this analysis method. Therefore, the author intends to write a special explanation for session analysis, hoping to bring some thinking and harvest to young partners.

Definition
Session is a sequence of browsing, clicking, sliding and other behaviors aggregated by users on platforms such as app / Applet / official website (taking app as an example below, all scenarios can be applied to applets and web pages).
Similar to the scenario of shopping on the e-commerce platform, when we click and open the customer service chat box, we enter a "conversation" with the customer service. We will ask the customer service about the product or complain. The customer service will send a "satisfaction invitation" only when we actively end our communication with the customer service or we do not continue to send messages to the customer service for a period of time, This "session" is over.
A series of operations and interactions on the app after the user starts the app can also be regarded as a "session" between the user and the app. Even if the user puts down the phone for a short time to do other things, as long as the app is reopened later for operation, the "session" will not end. Unless the user's departure time exceeds the threshold, the "session" will end automatically.

Meaning of Session Existence
Someone may ask, since you want to analyze the user's behavior sequence, why not directly analyze the whole behavior chain and events in the chain from opening to exiting the app, but create the concept of session? An example is given below.

Example of behavior chain

In the figure above, the user opened the app on his way to work, played for a while and then quit the app. After returning home from work, I opened the app, played for a while, put down the mobile phone, poured a glass of water in a minute, then came back and opened the app to continue browsing until I finally quit the app.
If the user simply uses "open exit app" as the cutting standard of behavior sequence, the depth of using app on the way to work is higher than that after going home (the number of "circles" in the figure from opening app to exiting app can be calculated to calculate the depth of interaction between user and app from opening to exiting).
But this is not the case. After exiting the app for the first time, the user just got up and poured a glass of water, and did not end the interaction with the app. If it is easy to draw the wrong conclusion that "the depth of use during working hours is higher than that after going home", it will mislead business colleagues, and in serious cases, it may lead them to make wrong decisions. On the contrary, session can merge the two seemingly "fragmented" behavior sequences after going home, so as to reveal the user's behavior and motivation over a period of time.

"Slicing" Principle of Session
Back to the example just now, since "open - exit app" is not roughly used as the cutting standard of user behavior sequence, what standard should be used to cut the user's behavior chain on the app?
This requires the introduction of a concept of "Slicing time". In the first part, the author mentioned that "unless the time the user leaves the app exceeds the threshold, the session will end automatically". This "threshold" is the "Slicing time".
For another simple example,