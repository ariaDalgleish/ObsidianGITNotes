
A datatype is a custom category of data you invent, made up of a fixed set of variants like the bintree.



## Why EOPL datatypes?

Racket's `struct` can build new data types, but for language interpreters we often want more structure than `struct` gives on its own — specifically, **variants** (like a tagged union) with automatic type-checking. EOPL (from Friedman & Wand's _Essentials of Programming Languages_) provides `define-datatype` for exactly this. You need `#lang eopl` to use it.

## `define-datatype` syntax

```racket
(define-datatype type-name type-predicate-name
  {(variant-name {(field-name predicate)}*)}+)
```

- **type-name** — the name of the datatype as a whole (e.g. `bintree`)
- **type-predicate-name** — a predicate auto-generated to test "is this any variant of this type?" (e.g. `bintree?`)
- **variant-name** — one of possibly several constructors/shapes the type can take
- **field-name / predicate** — each field in a variant has a name and a predicate that validates the value stored there

### Worked example: binary tree

```racket
(define-datatype bintree bintree?
  (null-node)
  (leaf-node (datum number?))
  (interior-node (key symbol?)
                 (left bintree?)
                 (right bintree?)))
```

Three variants:

- `null-node` — empty tree, no fields
- `leaf-node` — holds one number
- `interior-node` — holds a symbol key plus a left and right subtree (recursive — fields are validated with `bintree?`)

**Usage:**

```racket
(define T1 (leaf-node 23))
(define T2 (leaf-node 11))
(define T3 (interior-node 'key1 T1 T2))
(define T4 (interior-node 'key2 T3 (null-node)))
```

This builds a tree: `key2` at the root, with `key1` (holding leaves 23 and 11) as its left child and an empty node as its right child.

## `cases` — pattern matching on the datatype

Like `cond`, but specialized to pull apart a datatype's variants and bind their fields.

**Syntax:**

```racket
(cases type-name expression
  {(variant-name ({field-name}*) consequent)}*
  (else default))
```

**Example — summing all leaves:**

```racket
(define (leaf-sum tree)
  (cases bintree tree
    (null-node () 0)
    (leaf-node (v) v)
    (interior-node (k l r)
      (+ (leaf-sum l) (leaf-sum r)))))
```

- `null-node` → base case, contributes 0
- `leaf-node` → binds the datum to `v`, returns it
- `interior-node` → binds key/left/right, recurses on both children (ignores `k` here since we only need the sum)

## Predicates for individual variants

The blanket predicate `bintree?` is generated automatically, but predicates for a _specific_ variant (e.g. "is this a leaf-node?") are **not** auto-generated — you write them yourself using `cases`:

```racket
(define (leaf-node? x)
  (if (not (bintree? x))
      #f
      (cases bintree x
        (null-node () #f)
        (leaf-node (v) #t)
        (interior-node (k l r) #f))))
```

Check membership in the type first, then use `cases` to test which variant it actually is.

## Key conceptual point

You can only construct **variant** instances — `null-node`, `leaf-node`, `interior-node` — never the abstract type `bintree` itself. Each variant _is a_ `bintree`, but there's no way to build a "generic" bintree directly; the type only exists as the union of its variants.

---

Given this looks like it's feeding into the same programming-languages/Racket coursework you've been working on, want me to also sketch how `define-datatype` + `cases` would apply to something like the event-stream processor from your functional programming assignment?