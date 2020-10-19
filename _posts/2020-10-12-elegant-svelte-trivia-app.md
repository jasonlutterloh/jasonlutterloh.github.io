---
layout: post
title:  "An Elegant Svelte Trivia Quiz Application"
date:   2020-10-12 00:00:00 -0500
categories: svelte css magnum-pi trivia
---

# An Elegant Svelte Trivia Quiz Application

I was looking for a way to publish some trivia about one of my favorite shows (the original Magnum, P.I. TV series from the 1980s) and decided to build it using Svelte (my favorite JavaScript framework as of late). I wanted something that was simple, elegant, and could be easily used by any other developer to create their own trivia quiz. So, I built this and just published the source on GitHub.

The app relies on one JSON file to house the questions and answers (and even followup information). Past that, the app keeps score in state and relies on Svelte's built-in transitions for seamless transitions.

Oh, and you may be asking, "Why did you just use one of the 100 million quiz generator sites to hold your trivia?" My answer is two-fold...

1. This seemed like a quick and fun project to build.
2. I've been on a privacy/anti-advertisement kick lately so I wanted to make sure what I build would have no tracking, social features, or privacy implications. This app is nothing but a simple trivia app for fun. Nothing more. Of course, a developer could add that functionality, but I didn't want it.

I have a few other enhancements and feature ideas that I may get to one day but for now, this is going to do the trick.

 [Demo - Magnum, P.I. Trivia](https://trivia.lutterloh.dev/)

 [GitHub Repository](https://github.com/jasonlutterloh/trivia-app)
