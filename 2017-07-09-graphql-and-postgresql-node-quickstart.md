---
layout: post
title: "Node.js GraphQL & PostgreSQL Quickstart"
date: 2017-07-09
comments: true
description: "GraphQL and Node.js server quickstart."
keywords: "graphql postgresql javascript node nodejs"
categories:
- tutorials
tags:
- graphql
- postgresql
- javascript
- node
- nodejs
---

View the source code [here](https://github.com/JMensch/graphql-postgres-quickstart-demo)

GraphQL is an API query language that aims to replace REST. With GraphQL, you can
combine data from multiple sources into one response and expose it as a single API endpoint. We'll explore one option in this below: querying data from PostgreSQL.

## Prerequisites
From your terminal, install the necessary packages:

```bash
npm i pg-promise graphql graphql-tools cors body-parser express graphql-server-express
```


## PostgreSQL Connection
First, we'll setup a PostgreSQL connection instance:
<script src="https://gist.github.com/JMensch/b8f95d7b979c2485591186c92ecb863d.js"></script>

## Sample GraphQL Resolver
Now, let's create a simple GraphQL resolver to retrieve the data from Postgres:
<script src="https://gist.github.com/JMensch/25c7a3909ed473a9d7c862c04dab14e4.js"></script>

## Sample GraphQL Schema
Next, we'll tell GraphQL which fields we can query and what values to expect in the response:
<script src="https://gist.github.com/JMensch/c1824bb7f248b7166ce41d1ae22db4ec.js"></script>

## Sample GraphQL Server
Last, spin up an express server hosting our new API:
<script src="https://gist.github.com/JMensch/30ea85cf8d35c953cd673a4bf7fefbaa.js"></script>

## Conclusion

And that's it! You can now point your browser to localhost:3000/graphiql for a GUI representation.
Don't forget to create your users table in Postgres!

<br/>

---

<br/>

*If you enjoyed this article, please help out with a like, a share, or a comment. It fuels my focus to write more of it, thanks!*

<br/>

James Mensch is the Tech / Product Lead at <a href='https://www.thewedclique.com'>The Wed Clique</a> and the CEO at <a href='http://magnifai.io'>Magnifai</a>. I believe in building intelligent products, using data to drive decisions, and engineering for social impact. I <a href='https://medium.com/@james_mensch'>write</a> about some of the cool stuff I do with tech, productivity and motivation psychology, and my social innovation projects. Connect with me on <a href='https://www.linkedin.com/in/james-mensch/'>LinkedIn</a> or say hi on <a href='https://twitter.com/thebestmensch'>Twitter</a>.

