---
layout: post
title: Big Ball of Mud
permalink: /big-ball-of-mud
---
A big ball of mud is a software system that lacks any perceivable architecture.

> Although undesirable from a software engineering point of view, such systems
> are common in practice due to business pressures, developer turnover and code
> entropy. They are a type of design anti-pattern.
> 
> <cite>[Wikipedia](https://en.wikipedia.org/wiki/Big_ball_of_mud)</cite>

The original term comes from a 1997 conference:

> A Big Ball of Mud is a haphazardly structured, sprawling, sloppy,
> duct-tape-and-baling-wire, spaghetti-code jungle. These systems show
> unmistakable signs of unregulated growth, and repeated, expedient repair.
> Information is shared promiscuously among distant elements of the system,
> often to the point where nearly all the important information becomes global
> or duplicated.
>
> The overall structure of the system may never have been well defined. If it
> was, it may have eroded beyond recognition.
>
> Programmers with a shred of architectural sensibility shun these quagmires.
> Only those who are unconcerned about architecture, and, perhaps, are
> comfortable with the inertia of the day-to-day chore of patching the holes in
> these failing dikes, are content to work on such systems.
>
> <cite>Brian Foote and Joseph Yoder, Big Ball of Mud. Fourth Conference on
> Patterns Languages of Programs (PLoP '97/EuroPLoP '97) Monticello, Illinois,
> September 1997</cite>

What to do if you have a BBOM:

- Any new work coming in goes into a new application (or _applications_).
- Start peeling off pieces of code into the new application(s), starting with
  the least entangled parts.
- Emit events from the old system to a message queue which can be consumed by
  the new system.

If management aren’t interested in these things and just want to keep adding
features to the trash pile, leave and go help someone else.
