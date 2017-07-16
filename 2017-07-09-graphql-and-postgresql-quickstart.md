---
layout: post
title: "Node.js GraphQL & PostgreSQL Quickstart"
date: 2017-07-09
comments: true
description: ""
keywords: "graphql postgresql javascript node node.js"
categories:
- tutorials
tags:
- graphql
- postgresql
- javascript
- node
- node.js
---

GraphQL is an API query language that aims to replace REST. With GraphQL, you can
combine data from multiple sources into one response and expose it as a single API endpoint. We'll explore one option in this below: querying data from PostgreSQL.

# Prerequisites
From your terminal, install the necessary packages:

```sh
npm i pg-promise graphql graphql-tools cors body-parser express graphql-server-express
```

# PostgreSQL Connection
First, we'll setup a PostgreSQL connection instance:
<script src="https://gist.github.com/JMensch/b8f95d7b979c2485591186c92ecb863d.js"></script>

# Sample GraphQL Resolver
Now, let's create a simple GraphQL resolver to retrieve the data from Postgres:
<script src="https://gist.github.com/JMensch/25c7a3909ed473a9d7c862c04dab14e4.js"></script>

# Sample GraphQL Schema
Next, we'll tell GraphQL which fields we can query and what values to expect in the response:
<script src="https://gist.github.com/JMensch/c1824bb7f248b7166ce41d1ae22db4ec.js"></script>

# Sample GraphQL Server
Last, spin up an express server hosting our new API:
<script src="https://gist.github.com/JMensch/30ea85cf8d35c953cd673a4bf7fefbaa.js"></script>

# Fin
And that's it! You can now point your browser to localhost:3000/graphiql for a GUI representation.
Don't forget to create your users table in Postgres!


