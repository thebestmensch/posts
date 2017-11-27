---
layout: post
title: "Production Apollo GraphQL - Authentication & Authorization"
date: 2017-11-26
comments: true
description: "Production Apollo GraphQL Series part 2: How to authenticate and authorize users"
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

<i>NOTE: This example will be using Apollo-Client 1.x and Apollo-Server-Express 1.2.0.</i>

<i>
This is part two of my Production GraphQL series. Check out part 1, "Essential Setup and Tooling",</i> <a href='https://blog.cloudboost.io/production-apollo-graphql-essential-setup-and-tooling-4447ac01f94e'>here</a>.


<br/>

Each field provided by a GraphQL Schema corresponds to a resolver that produces the correct field. This gives us unparalleled control over our API by allowing us to govern access by _field_ rather than HTTP endpoint. Let's dive into how we do that below.

<br/>

## Authentication
I prefer using JSON Web Tokens for authenticating users. It's reusable across all platforms and doubles as an information exchange. Read more about it <a href='https://jwt.io/introduction/'>here</a>.

To use JWT, you need to send it in the Authorization header in each HTTP request, and decrypt it with a secret on the server. Check out this basic example:

<script src="https://gist.github.com/JMensch/c102e651f39f3c4a673322371d2aa4c1.js"></script>

That's it! When a user with a bad JWT sends a request, your server will return a `401 Unauthorized` error.

<br/>
## Authorization
GraphQL allows us to define each object's resolvers, which means we can define who has access to certain objects and object fields. First, let's update our server to pass the user context to each resolver. Update our previous code to look like this:

<script src="https://gist.github.com/JMensch/e26a43121180ab91b615364541147227.js"></script>

Now the decoded JWT object will be passed to each object and field resolver and mutator:

<script src="https://gist.github.com/JMensch/47b5d0116dee685366bf64ec969a46fe.js"></script>

Now you can perform authorization at the object level, or govern access to individual fields.

<br/>

---

<br/>

<i>If you enjoyed this article, please help out with a like, a share, or a comment. It fuels my focus to write more of it, thanks!</i>

<br/>

James Mensch is the Tech / Product Lead at <a href='https://www.thewedclique.com'>The Wed Clique</a> and the CEO at <a href='http://magnifai.io'>Magnifai</a>. I believe in building intelligent products, using data to drive decisions, and engineering for social impact. I <a href='https://medium.com/@james_mensch'>write</a> about some of the cool stuff I do with tech, productivity and motivation psychology, and my social innovation projects. Connect with me on <a href='https://www.linkedin.com/in/james-mensch/'>LinkedIn</a> or say hi on <a href='https://twitter.com/thebestmensch'>Twitter</a>.

