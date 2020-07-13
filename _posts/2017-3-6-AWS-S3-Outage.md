---
layout: post
title: AWS S3 Worldwide Outage!
---

About a couple weeks ago we decided to use AWS S3 for storage of a mobile application which needed about 3gb of data dynamically.

We've created an AWS account and uploaded all files in a new S3 bucket.
Everything was good, until...

AWS outage happened. The service was down but fortunately the app was not released at that time.

Our CTO said: Ok, this can happen. What have we thought to prevent this?

We did't! We have not even thought about S3 getting unavailable for a second.

These things can happen. **And whatever can happen will happen (Morphies law)**

We are responsible for outages. 
Not Amazon. 
We could prevent this easily with having another backup bucket on a different platform or even on a cheap VPS just to prevent a complete outage.

It does not require any API gateways and in fact, It's free of charge and works better if implemented correctly.
