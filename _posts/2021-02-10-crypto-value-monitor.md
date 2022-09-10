---
layout: post
title: "New Project: Crypto Value Monitor"
date: 2021-02-10 00:00:00 -0500
author: Jason Lutterloh
excerpt_separator: <!--more-->
excerpt: "If you have been looking for a simple way to monitor the value of all of your crypto holdings in one place, this project might interest you."
image: /assets/posts/post_crypto.png
canonical: https://lutterloh.dev/posts/2021-02-10-crypto-value-monitor/
---

If you have been looking for a simple way to monitor the value of all of your crypto holdings in one place, this project might interest you.

![Crypto Holdings Value Monitor](/assets/posts/post_crypto.png)

My original problem was that I didn't like having to login to 4 or 5 different apps/sites to check on the value of the different cryptocurrency holdings I had spread among the variety of wallets/services. I wanted one screen with all my holdings and how much it was worth. I tried a few apps that are supposed to do this but they all felt clunky, tried to do too much, made me worried about security/privacy, used API keys I didn't want to mess with, etc. So, this project was born...

The app is fairly simple and probably only useful if you are hodling across a few different wallets and services and want one place to monitor the value of your holdings. Essentially, you get a UI, a JSON file to detail what crypto you own and how much, and code for one API call to get current prices. The idea at this point is that the app runs locally (since that's as far as my use case warranted) but you're more than welcome to deploy it out with your data wherever you want.

I'm not sure anyone beyond myself will really have a use case for this, but thought I'd publish it anyways. If you end using it and enjoying it, let me know!

[Crypto Value Monitor on GitHub](https://github.com/jasonlutterloh/cryptovaluemonitor)
