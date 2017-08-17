---
layout: post
title: "Database source control, versioning, and environment management with Sqitch"
date: 2017-08-15
comments: true
description: ""
keywords: "database postgresql sqitch docker"
categories:
- tutorials
tags:
- database
- postgresql
- sqitch
---

View the source code [here](https://github.com/JMensch/database-source-control-demo)

We've been using source control for application code for years. Even infrastructure can be coded and versioned controlled. But some engineers are still oblivious to the need for version control around databases that house crucial data their applications rely on. Crazy, right? I use [Sqitch](http://sqitch.org/), which touts itself as "sane database change management" (and I agree) as a lightweight database version control tool for all of my production databases. In this tutorial I'll walk through how to get setup with Sqitch and manage a log of changes for a sample table.

# Setup
First, install Sqitch and the necessary database adapter (we'll be using PostgreSQL)

OSX:
```bash
brew tap theory/sqitch && brew install sqitch_pg
```

Debian:
```bash
apt-get install sqitch && apt-get install libdbd-pg-perl postgresql-client
```

# Database Schema

First, we have to initialize sqitch. In your terminal, run:

```bash
mkdir schema && cd schema
sqitch init myproject --uri https://myproject --engine pg
```
We use the `uri` argument as a unique identifier for our project, and `pg` to let Sqitch know we're using the PostgreSQL engine.

Next, let's add a basic user table using sqitch. In your terminal, run:

```bash
sqitch add users -n 'add table definition'
```

You'll see Sqitch generated a `users.sql` file in the `deploy`, `revert`, and `verify` folders, representing a deployment, revertion, and verification script for the users table.

Let's add appropriate code to the generated files:

<script src="https://gist.github.com/JMensch/5991f17e0ae1b2a19ded949778cdea83.js"></script>

# Database Changes

Let's add a sample change to our database. In /myproject/schema, run:

```bash
sqitch add users-email-col -n 'add users.email'
```

Same as before, we have 3 `users-email-col.sql` files generated. Lets add the code:

<script src="https://gist.github.com/JMensch/69883250eac63d93ac958c78b274effc.js"></script>

Sqitch runs changesets sequentually, so first the users table will be created (`users.sql`), then the email column will be added (`users-email-col.sql`).

# Managing Environments in Sqitch
Sqitch manages changes via a hash table in the target database, which means we need to point Sqitch to the correct database for dev, staging, and production environments so it can manage changes appropriately. We can do this with the `sqitch.config` file and the `target` property. Edit your config file to look like so:

<script src="https://gist.github.com/JMensch/52355b52aa94a794d57bf3a9d5429231.js"></script>

Now, you can deploy to the appropriate environments by specifying your target. For example:

```bash
sqitch deploy -t dev
```

# Fin
And that's it! Now you're managing every change to your database, and can deploy changes to multiple environments at different target locations.