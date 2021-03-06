## Module Data.FingerTree

This module defines a general-purpose data structure, known as a "finger
tree", which is intended to be used as a building block for implementing
other data structures. See, for example, `Seq` from `Data.Sequence`.

#### `Node`

``` purescript
data Node v a
  = Node2 v a a
  | Node3 v a a a
```

##### Instances
``` purescript
instance showNode :: (Show a, Show v) => Show (Node v a)
instance functorNode :: Functor (Node v)
instance foldableNode :: Foldable (Node v)
instance traversableNode :: Traversable (Node v)
instance measuredNode :: Measured (Node v a) v
```

#### `node2`

``` purescript
node2 :: forall a v. (Monoid v, Measured a v) => a -> a -> Node v a
```

#### `node3`

``` purescript
node3 :: forall a v. (Monoid v, Measured a v) => a -> a -> a -> Node v a
```

#### `nodeToDigit`

``` purescript
nodeToDigit :: forall a v. Node v a -> Digit a
```

#### `FingerTree`

``` purescript
data FingerTree v a
  = Empty
  | Single a
  | Deep (Lazy v) (Digit a) (Lazy (FingerTree v (Node v a))) (Digit a)
```

##### Instances
``` purescript
instance showFingerTree :: (Show v, Show a) => Show (FingerTree v a)
instance semigroupFingerTree :: (Monoid v, Measured a v) => Semigroup (FingerTree v a)
instance functorFingerTree :: Functor (FingerTree v)
instance foldableFingerTree :: Foldable (FingerTree v)
instance traversableFingerTree :: Traversable (FingerTree v)
instance measuredFingerTree :: (Monoid v, Measured a v) => Measured (FingerTree v a) v
```

#### `lazyEmpty`

``` purescript
lazyEmpty :: forall v a. Lazy (FingerTree v a)
```

#### `deep`

``` purescript
deep :: forall a v. (Monoid v, Measured a v) => Digit a -> Lazy (FingerTree v (Node v a)) -> Digit a -> FingerTree v a
```

#### `Digit`

``` purescript
type Digit a = Array a
```

#### `eqFingerTree`

``` purescript
eqFingerTree :: forall a v. (Monoid v, Measured a v, Eq a) => FingerTree v a -> FingerTree v a -> Boolean
```

#### `compareFingerTree`

``` purescript
compareFingerTree :: forall a v. (Monoid v, Measured a v, Ord a) => FingerTree v a -> FingerTree v a -> Ordering
```

#### `cons`

``` purescript
cons :: forall a v. (Monoid v, Measured a v) => a -> FingerTree v a -> FingerTree v a
```

#### `snoc`

``` purescript
snoc :: forall a v. (Monoid v, Measured a v) => FingerTree v a -> a -> FingerTree v a
```

#### `consAll`

``` purescript
consAll :: forall f a v. (Monoid v, Measured a v, Foldable f) => f a -> FingerTree v a -> FingerTree v a
```

#### `snocAll`

``` purescript
snocAll :: forall f a v. (Monoid v, Measured a v, Foldable f) => FingerTree v a -> f a -> FingerTree v a
```

#### `toFingerTree`

``` purescript
toFingerTree :: forall f a v. (Monoid v, Measured a v, Foldable f) => f a -> FingerTree v a
```

#### `ViewL`

``` purescript
data ViewL s a
  = NilL
  | ConsL a (Lazy (s a))
```

##### Instances
``` purescript
instance functorViewL :: (Functor s) => Functor (ViewL s)
```

#### `headDigit`

``` purescript
headDigit :: forall a. Digit a -> a
```

#### `tailDigit`

``` purescript
tailDigit :: forall a. Digit a -> Digit a
```

#### `viewL`

``` purescript
viewL :: forall a v. (Monoid v, Measured a v) => FingerTree v a -> ViewL (FingerTree v) a
```

#### `deepL`

``` purescript
deepL :: forall a v. (Monoid v, Measured a v) => Digit a -> Lazy (FingerTree v (Node v a)) -> Array a -> FingerTree v a
```

#### `isEmpty`

``` purescript
isEmpty :: forall a v. (Monoid v, Measured a v) => FingerTree v a -> Boolean
```

#### `head`

``` purescript
head :: forall a v. (Monoid v, Measured a v) => FingerTree v a -> Maybe a
```

#### `tail`

``` purescript
tail :: forall a v. (Monoid v, Measured a v) => FingerTree v a -> Maybe (FingerTree v a)
```

#### `lastDigit`

``` purescript
lastDigit :: forall a. Digit a -> a
```

#### `initDigit`

``` purescript
initDigit :: forall a. Digit a -> Digit a
```

#### `ViewR`

``` purescript
data ViewR s a
  = NilR
  | SnocR (Lazy (s a)) a
```

#### `viewR`

``` purescript
viewR :: forall a v. (Monoid v, Measured a v) => FingerTree v a -> ViewR (FingerTree v) a
```

#### `deepR`

``` purescript
deepR :: forall a v. (Monoid v, Measured a v) => Array a -> Lazy (FingerTree v (Node v a)) -> Array a -> FingerTree v a
```

#### `last`

``` purescript
last :: forall a v. (Monoid v, Measured a v) => FingerTree v a -> Maybe a
```

#### `init`

``` purescript
init :: forall a v. (Monoid v, Measured a v) => FingerTree v a -> Maybe (FingerTree v a)
```

#### `app3`

``` purescript
app3 :: forall a v. (Monoid v, Measured a v) => FingerTree v a -> Array a -> FingerTree v a -> FingerTree v a
```

#### `nodes`

``` purescript
nodes :: forall a v. (Monoid v, Measured a v) => Array a -> Array (Node v a)
```

#### `append`

``` purescript
append :: forall a v. (Monoid v, Measured a v) => FingerTree v a -> FingerTree v a -> FingerTree v a
```

#### `Split`

``` purescript
data Split f a
  = Split (f a) a (f a)
```

#### `LazySplit`

``` purescript
data LazySplit f a
  = LazySplit (Lazy (f a)) a (Lazy (f a))
```

#### `unsafeSplitDigit`

``` purescript
unsafeSplitDigit :: forall a v. (Monoid v, Measured a v) => (v -> Boolean) -> v -> Digit a -> Split Array a
```

#### `unsafeSplitTree`

``` purescript
unsafeSplitTree :: forall a v. (Monoid v, Measured a v) => (v -> Boolean) -> v -> FingerTree v a -> LazySplit (FingerTree v) a
```

#### `split`

``` purescript
split :: forall a v. (Monoid v, Measured a v) => (v -> Boolean) -> FingerTree v a -> Tuple (Lazy (FingerTree v a)) (Lazy (FingerTree v a))
```

#### `filter`

``` purescript
filter :: forall a v. (Monoid v, Measured a v) => (a -> Boolean) -> FingerTree v a -> FingerTree v a
```

#### `unfoldLeft`

``` purescript
unfoldLeft :: forall f a v. (Unfoldable f, Monoid v, Measured a v) => FingerTree v a -> f a
```

#### `unfoldRight`

``` purescript
unfoldRight :: forall f a v. (Unfoldable f, Monoid v, Measured a v) => FingerTree v a -> f a
```

#### `fullyForce`

``` purescript
fullyForce :: forall a v. FingerTree v a -> FingerTree v a
```


