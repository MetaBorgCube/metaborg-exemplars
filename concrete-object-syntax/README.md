# Concrete Object Syntax

This exemplar demonstrates how to setup concrete object syntax for using concrete syntax (defined in SDF) in transformation rewrite rules (defined in Stratego).

## Use cases

 - Define transformations in Stratego with rewrite rules expressed using _concrete_ rather than _abstract_ syntax.

## Description

Concrete object syntax currently only works with SDF2, hence the configuration in `metaborg.yaml`:

```yaml
language:
  sdf:
    version: sdf2
```

The language name is `concrete-object-syntax`.
The main syntax file is `/syntax/concrete-object-syntax.sdf`, containing definitions for statements with addition expressions.

The Strageo file `/trans/swap.str` defines three variants of a transformation to swap the terms of additions.
The rules `swap-exp-concrete-syntax` and `swap-exp-concrete-syntax-simple` use concrete syntax to define the swap.

To be able to use the language's concrete syntax in Stratego, its syntax must be embedded in Stratego's syntax.
`/syntax/Stratego-concrete-object-syntax.sdf` instantiates the embedding by importing the parameterized modules `StrategoMix` (the Stratego syntax) and `concrete-object-syntax-embedded` (which defines the embedding of Stratego within the language).
The module in `/syntax/concrete-object-syntax-embedded.sdf` defines how statements and expressions of the language can be used in Stratego rules.

When building the project, a parse table is generated for the embedded syntax: `/trans/Stratego-concrete-object-syntax.tbl`.
`/trans/swap.meta` indicates that the Stratego parse table with the language embedding should be used for `/trans/swap.str`, making it possible to use concrete syntax in transformation rules.

## References

 - [Eelco Visser. Meta-programming with Concrete Object Syntax. 2002.](https://doi.org/10.1007/3-540-45821-2_19)
 - http://www.metaborg.org/en/latest/source/langdev/meta/lang/stratego/strategoxt/11-concrete-object-syntax.html
