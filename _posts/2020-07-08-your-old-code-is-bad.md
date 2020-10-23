---
layout: post
title:  "Your Old Code is Bad... and That's Okay"
date:   2020-07-08 00:00:00 -0500
author: Jason Lutterloh
---

# Your Old Code is Bad... and That's Okay

Every once in awhile, I get the chance to look at some code I wrote in the past. Last week afforded me this chance as a coworker sent me a message and said, “Look whose name is on this changelog!”. Sure enough, it was some front end code I had written my first year on the job. It was appalling! I had used `<br />` tags in my HTML for styling purposes. The horror! 

The crazy thing is, I remember obsessing about that code when I originally wrote it. I wanted it to be perfect in every way, down to the tab spacing before each line. When I checked in that code, I truly believed it was perfect. Thankfully, years later, I recognize it wasn’t. 

One of my first mentors told me, “if you don’t look back on your old code after six months and see opportunity, you’re not growing and becoming a better developer”. I took that to heart but as I was reflecting on seeing my old code, I had two realizations.

The first is that a developer must be graceful with himself or herself. Good developers spend immense amounts of energy crafting their code. Beyond being functional, “good code” must be easily readable, maintainable, performant, testable, extensible, secure, follow best practices, peer-reviewed, etc. This process takes time and effort (and courage in the case of the peer review) and yet when you come back to look at that code after not looking at it for six months, you’re going to find things you dislike. 

How do you live with yourself? (Okay, maybe that’s a bit dramatic, but...)

It can be demoralizing knowing that no matter how much effort you put into your current code, it will never live up to your future standards. However, I implore you to show yourself a little grace and see chances to review your old code as opportunities to reflect and see how far you’ve come. Take these opportunities to be thankful that you’ve grown as a developer and then share what you’ve learned so that others can grow too. Noticing things that you’d do differently now means you’ve learned and gained experience. It means you’re a better developer than you ever have been. Not to mention, not everything you notice in that old code is going to be an oversight or a mistake you made. Most of what you’ll notice will likely be style or preference changes and not true defects (hopefully) and that brings me to my next realization…

The bulk of your time and energy is best spent on hardening your code’s functionality and resiliency. If it’s a foregone conclusion that in the future you’re going to dislike things about your code that you’re writing in the present then it doesn’t make sense to try and be absolutely perfect. I’m not saying to write nasty code or not to care. As I mentioned earlier, good developers naturally craft their code to be easily readable, maintainable, testable, etc and that’s still important. However, what matters at the end of the day is that your application works and is bug-free. Spend the bulk of your energy trying to break your application and make sure it can handle all scenarios thrown at it by your end-user (like handling the inevitable double-click on a “Submit” button).

The code I mentioned at the beginning of this article has been in production for seven years! It’s seen countless changes around it but it’s still there faithfully serving whoever loads that page. While there may be a break tag doing some styling, the code is doing what it was intended to do and the user doesn’t know the difference… even if that code is ugly.

When I initially looked at that old code, I felt some level of shame and asked my friend if they would remove my name from it. I’d be lying if I said I didn’t worry about what other developers would think of me for writing that but then I realized something. Every other good developer has found themselves in that same vulnerable position before. That was a comforting thought to accompany my dose of humility.

Your code will never be perfect so spend your time and energy making sure your code works for the end-user. That doesn’t mean you shouldn’t make your code readable, extensible, etc. but don't do this at the expense of the other. Do it knowing that in six months, you’re probably not going to like something about it. When you do have that realization, be thankful for how far you’ve come and share what you’ve learned so others can grow too.
