---
layout: post
title: Why I don't use Docker Compose
permalink: /why-i-dont-use-docker-compose
---
**I don't use Docker Compose. I prefer to use `docker` commands.**

Docker Compose is another layer on top of Docker, which can break or change its
interface. Using `docker` directly removes the need for it.

Parameters to a `docker run` command are right there in front of you. Configuration in a "Compose file" is further away
from the user.

By putting `docker run` commands in a README, parameters are right there with
the documentation for that service. With Docker Compose, the configuration is
in a file somewhere, often combining multiple repositories, further away.

> Keep data close to where it's used.

Also, the parameters for different environments are together, beside each other in
subsequent commands in the documentation. Not in separate files.

## Most Importantly

Having dev and prod differ by no more than the commands executed is the ultimate in
[Dev/Prod parity](https://12factor.net/dev-prod-parity).

At a higher level, I just don’t want to compose services together. Why should
Postgres come down with my app? It's just a service. Leave it up.
