---
layout: post
title: Why I don't use Docker Compose
permalink: /why-i-dont-use-docker-compose
---
**I don't use Docker Compose. I prefer to use `docker run` commands. Here are
my reasons why.**

Using a `docker run` command with parameters is more explicit. Configuration in
a "Compose file" is further away from the user.

When a `docker run` command is in a README file, configuration is right there
with the documentation for the service you're bringing up. With Docker Compose,
the configuration is in a file somewhere, often combining multiple
repositories, further away.

> Keep data close to where it's used.

Also, the configuration for dev and prod are right there beside each other, in
subsequent commands in the documentation. Not in separate files.

When an engineer is bringing up the containers for the first time, he can work
through the issues for each container one at a time, following a set of
instructions. He can see the `docker run` commands he's executing right there,
with the parameters, and make any adjustments to them.

At a higher level, I just don’t want to compose services together. Why take
down Postgres with my app? It's just a service. Once it's up, leave it up.
