---
layout: post
title: Why I don't use Docker Compose
permalink: /why-i-dont-use-docker-compose
---
**I don't use Docker Compose. I prefer to use `docker run` commands. Here are
my reasons why.**

Docker Compose is another layer on top of Docker, which can break or change its
interface. Using `docker` directly removes the need for it.

Parameters to a `docker run` command are right there in front of you. Configuration in a "Compose file" is further away
from the user.

By putting a `docker run` command in a README, parameters are right there with
the documentation for that service. With Docker Compose, the configuration is
in a file somewhere, often combining multiple repositories, further away.

> Keep data close to where it's used.

Also, the parameters for dev and prod are together, beside each other in
subsequent commands in the documentation. Not in separate files.

When an engineer is bringing up the containers for the first time, he can work
through the issues for each container one at a time. He follows a set of
instructions, pasting `docker run` commands from a README. Once a service is
up, great. Move onto the next one.

Having dev and prod differ by only parameters in the command is the ultimate in
[Dev/Prod Parity](https://12factor.net/dev-prod-parity).

At a higher level, I just don’t want to compose services together. Why should
Postgres come down with my app? It's just a service. Leave it up.
