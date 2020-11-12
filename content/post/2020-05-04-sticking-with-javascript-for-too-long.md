---
title: Sticking with JavaScript for too long
date: 2020-05-04T18:52:14.509Z
summary: An example of what it costs to stay in one's comfort zone
---
**TL;DR: Don't write your first program in JavaScript, write your first app in JavaScript**

There's a reason why JavaScript is the most popular language in the world. It's easy to pick up and is insanely forgiving. But there is a point in an engineer's career where it becomes too messy to pick up new patterns and become a better programmer.

Here's what I discovered the hard way.

## TypeError

I hated TypeScript from the moment I experienced it to the moment I added Sentry to my app.

At first, I remained shielded behind the fact that it's still JS running. It's just a bloody syntax and a series of tools painful to setup - that last part remains true.

But one day (after users and CEO shouting at me relentlessly) I decided to get real and monitor things, came in Sentry. The number of TypeError was ridiculous.

Plus the smart people at Airbnb admitted to 60% of their JS bugs coming from type errors.

Planning anything longer than 500 lines in JavaScript? Go TypeScript.

## `JSON.parse()`

`JSON.parse()` is a beautiful thing. But as they say, power comes with responsibility.

Even more so when it's hidden. At least the explicit call make you acknowledge that you are abandoning all control over what you're parsing. I think the more dangerous is `app.use(bodyParser())`. Your endpoint can receive all kinds of crap without you even noticing.

## Operations

That's where it gets funny! And all credit goes to Mr. Gary Bernhardt famous [Wat talk](%5B%3Chttps://www.destroyallsoftware.com/talks/wat%3E%5D(%3Chttps://www.destroyallsoftware.com/talks/wat%3E)).

There's almost no harm behind a cute `'item' + 1` but try those out:

* `[] + []`
* `{} + 1`
* `{} + []`
* `[] + {}`

Still have faith?

Today I don't recommend JS to first time programmers. But JS may be the best way to bring makers on board. No language will get you from zero to app as fast as JS. That may be what new comers are after: something as close to no-code as possible.

In the end, we're all in this to build cool things. The more the merrier!