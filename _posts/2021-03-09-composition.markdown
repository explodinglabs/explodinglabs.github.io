---
layout: post
title: Composition is the essence of programming
permalink: /composition
---
*This post is a work in progress.*

Engineers achieve big things by solving little problems. If we can solve all
the little problems, we can combine the solutions to solve bigger problems.

Why do we break down problems? This is due to the limitations of the human mind
- our brains can only deal with a small number of concepts at a time. So we
break down problems, and break them down again until we can mentally digest
them.

In programming we solve small problems by writing functions. Here we zoom in to
focus on a single task.

> The psychological profiling (of a programmer) is mostly the ability to shift
> levels of abstraction, from low level to high level. To see something in the
> small and to see something in the large.
> — An interview with Donald Knuth. Dr. Dobb’s Journal, pages 16–22 (April
> 1996)

In Haskell, the body of a function is always an expression; there are no
statements in functions. In a way this guides you to making sure functions are
small.

Finally, we combine the solutions.

Programming is about composition. Decomposing problems and composing the
solutions.

“Being able to decompose bigger problems into smaller problems, and then
combine the solutions, that’s essentially the description of... well, I don’t
know it depends on who you are, you will say that’s the description of what I’m
doing as a programmer, and a mathematician will say that’s the description of
what I’m doing as a mathematician, and a physicist will say that’s what I’m
doing as a physicist. It’s like, everybody’s doing this, this is the essence of
all human activity.”

In most languages there’s no built-in way of composing two functions. Something
as fundamental as combining functions is not built into the language.

Haskell is built around composition. In Haskell, as in math, composition is
represented as a dot.

"Once you realise how simple things are in Haskell, the inability to express
straightforward concepts in other languages is a little embarrassing."

A brief mention of category theory?  
Compare with Unix's simplicity?  
