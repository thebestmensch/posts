---
layout: post
title: "Production Apollo GraphQL - Essential Setup and Tooling"
date: 2017-11-13
comments: true
description: ""
keywords: "graphql nodejs node javascript server production apollo"
categories:
- tutorials
tags:
- graphql
- production
- javascript
- node
- nodejs
---

[GraphQL](http://graphql.org/) has revolutionized the way we think about APIs, and [Apollo](https://github.com/apollographql) has provided a suite of frameworks to get up and running quick and easy. We've been using GraphQL and Apollo since inception at the [The Wed Clique](https://www.thewedclique.com/). Since then I've learned the ins and outs of the Apollo GraphQL stack, and I'm here to share some tools I use supplement the relative immaturaty and get the stack to a place that's a reliable production stack.

## Machine readable errors with apollo-errors

The first headache you'll encounter with the Apollo GraphQL stack is that errors returned to the client are in string format. An example:

![apollo-errors example error](https://gist.githubusercontent.com/JMensch/2ea1eec9a3011d7f343f4271eab9e67c/raw/6fe76b3daaadef643eefb6f84189ca4d94bb5624/apollo-error.png)

Pretty tough to do anything with that, right? Luckily [thebigredgeek's](https://github.com/thebigredgeek) [apollo-errors package](https://github.com/thebigredgeek/apollo-errors) is here to save us! All you have to do is plug it into your schema (a 1 line change), and now your errors looks like this:

<script src="https://gist.github.com/JMensch/bd1b88798d6af51f4a452de9330ae93d.js"></script>

Magic!

<br/>

## Performance Insight with Apollo Engine

The beauty of nested GraphQL queries can also be its downfall if your resolvers aren't structured correctly. Luckily we can use [Apollo Engine](https://engine.apollographql.com/) to monitor each resolver for usage and quickly debug those long running queries. Check it out:

![apollo engine metrics](https://gist.githubusercontent.com/JMensch/2ea1eec9a3011d7f343f4271eab9e67c/raw/e96d538db469435b46ffa454969b87b595248c8d/apollo-engine.png)

Apollo Engine can do so much more, including caching and error tracking- all for free. Read this great post by [Rohit Bakhshi](https://dev-blog.apollodata.com/introducing-apollo-engine-insights-error-reporting-and-caching-for-graphql-6a55147f63fc) of the Meteor team to learn more.

<br/>

## Query Context

Query context isn't a tool, but something I rarely see use cases for in the multitude of "Hello World!" GraphQL posts. Context is a great place to inject request specific information that your resolvers can use. One quick use case is passing a current user variable for authorization:

<script src="https://gist.github.com/JMensch/47b5d0116dee685366bf64ec969a46fe.js"></script>

If you're using something like JWT for middleware, you can attach the context to each request like so:

<script src="https://gist.github.com/JMensch/e26a43121180ab91b615364541147227.js"></script>

And thats it!

<br/>

## Fin

Hopefully this has been useful! I'd love to hear what you're using, please reach out!
