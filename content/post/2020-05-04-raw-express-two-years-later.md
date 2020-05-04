---
title: Raw Express, two years later
date: 2020-05-04T18:30:54.140Z
description: Things can grow out of hands quicker than you think
summary: Things can grow out of hands faster than you plan
---
```javascript
// https://expressjs.com/en/starter/hello-world.html
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => res.send('Hello World!'))

app.listen(port, () => console.log(`Example app listening on port ${port}!`))
```

Express is one of my favorite lib. Once comfortable with it powerful things can be built in a matter of minutes.

While it can basically do anything, the main drawback is the freedom it gives you (much like JS itself).

Like many we built our app with express using our version of a smart architecture. After two years in production, managing chaos takes up to a third of my time.

## The application

For the sake of this article let's say it's just your average SaaS application. We have a bunch of fancy things running but that happens outside of Express (Bull can be a cool topic for another article).

The application is mature enough reflect on it. A good indicator of maturity I thing (and maintenance chaos) is that it's been a while since we added an endpoint.

The server has 110 routes. Most of them to interact with a MySQL database. Some create background jobs that in turn trigger websocket events. It also serves static files.

Plain express with vanilla nodejs 10.16.3.

## Problems

Two years down the line, our main issues are:

* no sessions
* no caching
* manual HTTP input validation
* overhead code with internal APIs

## My sauce

We starter this project when the microservice craze was as its peak. So, like I assume many others, our design decisions were influenced into massive premature optimization. The idea was to build a monolith that could be decoupled with ease. The answer was **internal APIs**. 

Not all influence is bad. A paper from a Twitter engineer (find ref) presented the controller model future concept. So each pseudo service is actually nicely coupled with single controller and model files.

What we ended up with is a server that hits itself. Kinda bad I know. Plus two years down the line the decoupling is absolutely not where it was planned for.

The decoupling solution was a job queue and workers. This is actually nice. Bull helps a lot with this, even if it has its downsides. "Job stalled more than the allowable limit". 

## Building your own auth

## The ORM pitfall

So after decoupling we ended up with three sevices hitting the same database tables. And here comes deadlock land. Hands down, I don't have enough experience managing relational databases to solve deadlocks. Patterns are hard to identify. Asking for help resulted in everyone telling me to use Postgres as it "handles deadlocks way better". So on we went.

"I use knex and all my database queries are in a single file so I can support any database", yeah right.

The real value of a library like Knex lies in the sanitization of queries, not database engine compatibility. Plus, I completely agree that planning to support several DBMSs is a red flag for bad system design.

Refactoring queries to switch to Postgres took two months.

## Actions

### Use firebase hosting

### Move to pusher

As a fresh developer I often got the urge to build everything myself. Looking back it was mostly for learning purposes.