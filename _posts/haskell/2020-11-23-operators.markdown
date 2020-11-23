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

Apply
```haskell
fmap :: (a -> b)   -> f a        -> f b
ap   :: f (a -> b) -> f a        -> f b
bind :: m a        -> (a -> m b) -> m b
```
