# Language Extension

This exemplar demonstrates how to extend a language without changes to the language that is being extended.

## Use cases

 - A language with an open-source frontend (e.g. syntax and static semantics) but a proprietary backend (e.g. code generation). In such a case, the code generation could be implementated as an extension to the frontend.

## Description

The `base` project being extended is defined in the `/base` directory.
It is a simple language with syntax for addition expressions.
The `extension` project is defined in `/extension`.
It extends the base language with an editor action that swaps the terms in additions.

The extension project configuration file `/extension/.metaborg.yaml` contains the following lines:

```yaml
contributions:
- name: base
  id: org.metaborg:exemplars.extension.base:0.1.0-SNAPSHOT
dependencies:
  source:
  - org.metaborg:exemplars.extension.base:0.1.0-SNAPSHOT
```

First, this indicates that the project contributes to the base language.
The `name` and `id` values correspond to those in `/base/.metaborg.yaml`.
Second, this defines a source dependency on the base project, such that the extension project has access to e.g. the addition expression constructor for defining the swap transformation.
The Maven configuration in `/extensions/pom.xml` also contains this dependency.

The base project exports its source with the following lines in `/base/.metaborg.yaml`:

```yaml
exports:
- language: Stratego-Sugar
  directory: trans
  includes:
  - "**/*.str"
- language: Stratego-Sugar
  directory: src-gen
  includes:
  - "signatures/base/*.str"
```

The extension project has its context set to none in `/extensions/editor/main.esv`:

```
language
  context: none
```

## References

 - http://www.metaborg.org/en/latest/source/langdev/manual/language-extension.html
