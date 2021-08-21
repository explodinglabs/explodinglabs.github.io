---
layout: post
title: Composition
permalink: /composition
---
Engineers achieve big things by solving little problems. If we can solve all
the little problems, we can combine the solutions to solve bigger problems.

Why do we break down problems? This is due to the limitations of the human mind
-- we can only deal with a small number of concepts at a time. So we break down
problems, and break them down again until we can mentally digest them.

In programming we solve small problems by writing functions. Here we zoom in to
focus on a single task, ignoring everything else.

In Haskell, the body of a function is always an expression; there are no
statements in functions. In a way this guides you into making sure functions
are small. A function does no more than give you a value based on an argument.

Finally, we combine the solutions.

So programming is about composition -- decomposing problems and composing the
solutions.

> Being able to decompose bigger problems into smaller problems, and then
> combine the solutions, that’s essentially the description of... well, I don’t
> know it depends on who you are, you will say that’s the description of what
> I’m doing as a programmer, and a mathematician will say that’s the
> description of what I’m doing as a mathematician, and a physicist will say
> that’s what I’m doing as a physicist. It’s like, everybody’s doing this. This
> is the essence of all human activity.
>
> <cite>Bartosz Milewski</cite>

> The psychological profiling (of a programmer) is mostly the ability to shift
> levels of abstraction, from low level to high level. To see something in the
> small and to see something in the large.
>
> <cite>An interview with Donald Knuth. Dr. Dobb’s Journal, pages 16–22 (April
> 1996)</cite>
