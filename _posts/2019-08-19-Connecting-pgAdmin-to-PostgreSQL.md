---
layout: post
title: Connect pgAdmin to PostgreSQL
date: '2019-08-19 07:44:54 +0700'
categories: jekyll update
---

Today I tried to connect pgAdmin to PostgreSQL but failed.
I got `fe_sendauth: no password supplied` error.

After googling, I found this:

> Basically, it is important to understand that for most Unix distributions, **the default Postgres user neither requires nor uses a password for authentication**. Instead, depending on how Postgres was originally installed and what version you are using, the default authentication method will either be ident or peer.

More: [https://chartio.com/resources/tutorials/how-to-set-the-default-user-password-in-postgresql](https://chartio.com/resources/tutorials/how-to-set-the-default-user-password-in-postgresql)

So in the default setup, the default user for Postgres is postgres and requires no password. The solution to allow pgAdmin to connect to Postgres is to change the authentication in Postgres from md5 to trust.

First, open `pg_hba.conf` by running:
```bash
sudo nano /etc/postgresql/10/main/pg_hba.conf
```

And change the line:
```
# IPv4 local connections:
host    all             all             127.0.0.1/32            md5
```

to:

```
# IPv4 local connections:
host    all             all             127.0.0.1/32            trust
```

After that, don't forget to restart the PostgreSQL server.
