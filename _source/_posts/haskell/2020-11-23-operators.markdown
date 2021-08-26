---
layout: post
category: haskell
title: Haskell operators
permalink: /haskell/operators
---
Compose
```haskell
(.)   :: (b -> c)   -> (a -> b)   -> (a -> c)
(>=>) :: (a -> m b) -> (b -> m c) -> (a -> m c)
```

Map, apply, bind
```haskell
fmap :: (a -> b)   -> f a        -> f b
ap   :: f (a -> b) -> f a        -> f b
bind :: m a        -> (a -> m b) -> m b
```
