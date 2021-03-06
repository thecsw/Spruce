# Planned and Existing Features

Spruce currently compiles, but with a reduced feature set. This document
exists to coordinate the work of building new features.

## Primitives

| Type | Status |
|------|--------|
| Bool | :heavy_check_mark: |
| Int | :heavy_check_mark: |
| Float| |
| Char | |
| String | |
| Tuple | |
| Record / Struct | |

In general the Spruce approach to primitives has not received a lot of
thought. My general instinct is to implement as many types as possible in
Spruce's type system, but obviously that doesn't make sense for things like
Int and Float. Also, I don't think String should be implemented as a List of
Char, as is done in Haskell.

## Lists

| Feature | Status |
|---------|--------|
| Lists | :heavy_check_mark: |
| JS-backed Lists | |
| List Indexing (Python-style) | |
| List Comprehension | |
| List Iteration (for loop) | |

Technically, Lists can currently be constructed in Spruce with ADTs as such:

```
type List {
    Cons(Float, List)
    Nil
}
```

This is the list definition one might expect to see in functional languages.
However, for performance reasons it probably makes more sense to back Spruce's
lists with JavaScript lists. Ideally interfaces will make it possible for both
versions of a list to be used in things like for loops. One of the main design
goals of Spruce is to make list processing easy and expressive with a mix of
functional and imperative concepts.

## Functions

| Feature | Status |
|---------|--------|
| Basic Functions | :heavy_check_mark: |
| Anonymous (lambda) functions | |
| Closures | |
| Optional Arguments | |

## Type System

| Feature | Status |
|---------|--------|
| Type Annotations | |
| Type Inference | :heavy_check_mark: |
| Type Aliases | |
| Typeclasses | |

Spruce currently features a type inference algorithm based on hindley-milner,
but adapted for imperative languages. It should be able to deduce any type,
and produce general types for functions! That being said, it's not thoroughly
tested yet, and may break in some edge cases.

## ADTs

| Feature | Status |
|---------|--------|
| ADT | :heavy_check_mark: |
| Type Parameters | :heavy_check_mark: |
| Arbitrary ADT Constructor Types | |

ADTs have been a huge priority in developing Spruce, since once we have good
ADTs we get a bunch of features for free. For instance, Booleans are
implemented in Spruce as adts, and case statements can function as ifs no
problem! That's not to say we won't want if statements eventually, but for now
this is a great stop-gap.

ADTs also let us make pretty much any data structure we want: lists, maps,
trees, etc. as long as we don't care about performance. "Don't care about
performance" _is_ a pretty big caveat, admittedly, so for key data structures
we should probably use the js equivalents under the hood.

## Pattern Matching

| Feature | Status |
|---------|--------|
| ADT matching | :heavy_check_mark: |
| Any (underscore) | |
| Numeric patterns | |
| String patterns | |
| Tuples | |
| Incomplete Pattern Detection | |

Pattern matching currently works to allow destructuring of ADT values, but
cannot do anything useful with numeric types, or strings or tuples when those
are implemented.

## Parser

| Feature | Status |
|---------|--------|
| Basic language parsing | :heavy_check_mark: |
| Multiline Statements | |
| Understanding of Indentation | |

The current parser can take language into an AST, but it lacks any
understanding of indentation, and as such can't currently parse multiline
statements.

## Codegen

| Feature | Status |
|---------|--------|
| Code Generation | :heavy_check_mark: |
| Indentation | :heavy_check_mark: |
| Output Optimization | |

The compiler currently however generates javascript that faithfully executes
the instructions provided by the source Spruce. However, no optimization is
done on this output, which is of course very important if we want anyone to
seriously consider using Spruce. Compier optimization is a massive topic
deserving of much more than one table row, likely its own section once work on
optimization starts.

## Miscellaneous

| Feature | Status |
|---------|--------|
| Assignment From Case | |
| Multiple Assignment| |
