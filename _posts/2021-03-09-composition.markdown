---
layout: post
title: Composition is the essence of programming
permalink: /composition
---
Engineers can achieve big things by solving little problems. If we can solve
all the little problems, we can combine the solutions to solve bigger problems.

Why do we break down problems? This is due to the limitations of the human
mind. Our brains can only deal with a small number of concepts at a time. So we
break down problems, and break them down again until we can mentally digest
them.

In programming we write small solutions as functions. Here we zoom in. In
Haskell the body of a function is always an expression; there are no statements
in functions. In a way this guides you to making sure functions are small.

Finally we combine the solutions.

Programming is about composition. Decomposing problems and composing the
solutions. Even the small solutions are compositions of other small solutions.

“Being able to decompose bigger problems into smaller problems, and then
combine the solutions, that’s essentially the description of... well, I don’t
know it depends on who you are, you will say that’s the description of what I’m
doing as a programmer, and a mathematician will say that’s the description of
what I’m doing as a mathematician, and a physicist will say that’s what I’m
doing as a physicist. It’s like, everybody’s doing this, this is the essence of
all human activity.”

In c or Python there’s no built-in way of composing two functions. Something as
fundamental as combining functions is not built into the language.

Haskell is built around composition. In Haskell, as in math, composition is
represented as a dot.

“Once you realise how simple things are in Haskell, the inability to express
straightforward concepts in other languages is a little embarrassing.“

Compare with Unix.
