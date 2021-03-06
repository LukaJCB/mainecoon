---
layout: page
title:  Type classes
section: typeclasses
position: 4
---


## Type classes

Currently there are three type classes defined in mainecoon: [FunctorK](#functorK), [InvariantK](#invariantK), and [CartesianK](#cartesianK). They can be deemed as somewhat higher kinded versions of the corresponding type classes in cats.


### <a id="functorK" href="#functorK"></a>`FunctorK` 
```tut:silent
  def mapK[F[_], G[_]](af: A[F])(fk: F ~> G): A[G]
```

For tagless final algebras whose effect `F` appears only in the covariant position, instance of `FunctorK` can be auto generated through the `autoFunctorK` annotation.

### <a id="invariantK" href="#invariantK"></a>`InvariantK` 
```tut:silent
  def imapK[F[_], G[_]](af: A[F])(fk: F ~> G)(gK: G ~> F): A[G]
```

For tagless final algebras whose effect `F` appears in both the covariant positions and contravariant positions, instance of `InvariantK` can be auto generated through the `autoInvariantK` annotation.

### <a id="cartesianK" href="#cartesianK"></a>`CartesianK` 
```
 def productK[F[_], G[_]](af: A[F], ag: A[G]): A[Tuple2K[F, G, ?]]
```

For tagless final algebras that
1. has no extra type parameters or abstract type members, and
2. whose effect `F` appears only in the covariant position for **all members**,

instance of `CartesianK` can be auto generated through `autoCartesianK` annotation.


Their laws are defined in `mainecoon.laws`. To test your instance (if you decide to roll your own) against these laws please follow the examples in `mainecoon.tests`, especially the ones that test against `SafeAlg`.


