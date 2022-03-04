---
layout: post
title: Why I don't use Docker Compose
permalink: /why-i-dont-use-docker-compose
---
**I don't use Docker Compose. I prefer to use `docker run` commands. Here are
my reasons why.**

Docker Compose is another layer on top of Docker, that can break or change its
interface. Using Docker directly removes the need for it. 

Using a `docker run` command with parameters is more explicit. The parameters
are right there in front of you. Configuration in a "Compose file" is further
away from the user.

By putting a `docker run` command in a README file, configuration is right
there with the documentation for that service. With Docker Compose, the
configuration is in a file somewhere, often combining multiple repositories,
further away.

> Keep data close to where it's used.

Also, the configuration for dev and prod are together, beside each other in
subsequent commands in the documentation. Not in separate files.

When an engineer is bringing up the containers for the first time, he can work
through the issues for each container one at a time. He follows a set of
instructions, pasting `docker run` commands from a README. Once a service is
up, great, move onto the next one.

At a higher level, I just don’t want to compose services together. Why take
down Postgres with my app? It's just a service. Once it's up, leave it up.
