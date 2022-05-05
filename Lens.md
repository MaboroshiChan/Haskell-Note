# **What is Lens**

Costate Comonad Coalgebra is equivalent of Java's member variable update technology for Haskell

```Haskell
data Lens a b = Lens {
  view :: a -> b,
  set :: a -> b -> a
}

view :: Lens a b -> a -> b
set :: Lens a b -> a -> b -> a
```

Laws:

1.) set l (view l s) s = s
2.) view (set l s t) = t
3.) set (set l s t) s u = set l s u

```Haskell
newtype Lens s a = Lens (a -> Store s a)
data Store s a = Store (s -> a) s
instance Category Lens where
  id = Lens (Store id)
  Lens g . Lens f = Lens (\x -> Store (f x . g (view f x)) x)
```