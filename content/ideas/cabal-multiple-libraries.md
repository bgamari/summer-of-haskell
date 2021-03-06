---
title: Proof of Concept Support for Multiple Public Libraries in a .cabal package
---

A common pattern with large scale Haskell projects is to have a large number of
tightly-coupled packages that are released in lockstep.
One notable example is amazonka; as pointed out in
[amazonka#4155](https://github.com/haskell/cabal/issues/4155#issuecomment-270126748)
every release involves the lockstep release of 89 packages. Here, the tension
between the two uses of packages is clearly on display:

1. A package is a unit of code, that can be built independently. amazonka is
split into lots of small packages instead of one monolithic package so that
end-users can pick and choose what code they actually depend on, rather than
bringing one gigantic, mega-library as a dependency of the library.

2. A package is the mechanism for distribution, something that is ascribed a
version, author, etc. amazonka is a tightly coupled series of libraries with a
common author, and so it makes sense that they want to be distributed together.

The concerns of (1) have overridden the concerns of (2): amazonka is split into
small packages which is nice for end-users, but means that the package
maintainer needs to upload 89 packages whenever they need to do a new version.

The way to solve this problem is to split apart (1) and (2) into different units.
The package should remain the mechanism for distribution, but a package itself
should contain multiple libraries, which are independent units of code that can
be built separately.

The goal of this project is to complete a proof-of-concept implementation of
multiple public libraries in Cabal and cabal-install.
The completion of this feature requires additional work outside the scope of
this project, including patching hackage-server and Haddock.

For additional information and discussion, see
[cabal#4206](https://github.com/haskell/cabal/issues/4206)

**Mentor**: Edward Z. Yang

**Difficulty**: Advanced
