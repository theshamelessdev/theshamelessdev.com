---
title: Sticking with JavaScript for too long
date: 2020-05-04T18:52:14.509Z
summary: An example of what it costs to stay in the comfort zone
---
There's a reason why JavaScript is the most popular language in the world.

But there is a point in an engineer's carreer where it becomes too forgiving to go further.

Here's what I discovered the hard way, and too late.

## TypeError

I hated TypeScript from the moment I experienced it to the moment I accounted for TypeErrors. Plus the smart people at Airbnb admitted to 60% of their JS bugs coming from type errors.

Since it's still JS running I remained conviced for a while.

At the time of this writing we havn't started the TS move but the plan is to add a build phase with `tsc` and rewrite file incrementally.

## struct

`JSON.parse()` is powerful but as they say, it comes with responsibility.

Even more so when it's hidden. The explicit use make you decide to give away control. I think the more dangerous is `app.use(bodyParser())`. Your endpoint can receive all kinds of crap.

So I got started with golang following \[learn Go with tests], brave new world.