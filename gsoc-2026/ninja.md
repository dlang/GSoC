---
parent: DLang GSoC 2026 Project Ideas
nav_order: 4
---

# Adding a Ninja backend to Dub

**Mentor:** [Atila Neves](atila.neves@gmail.com)

| Spec | Details |
|-|-|
| **Difficulty Level** | medium |
| **Project Duration** | 175 hours |
| **Number of Contributors** | 1 |
| **Prerequisites** | D, dub internals, build systems (Ninja), cross-platform tooling/testing |

## Description

dub can build projects directly, and it can also generate build descriptions for other tools.
There is existing Ninja generation functionality via a reggae Ninja backend, but it is tied to reggae which means users must opt-in to using a different tool instead of the D standard which is dub.

This project adds a native Ninja backend to dub that provides equivalent functionality to the reggae Ninja backend, i.e. generating correct build.ninja files for dub packages (including dependencies) across supported platforms and compilers. The backend should cover the same set of dub features currently supported by the reggae Ninja backend.

## Project milestones:

1. D source compilation and linking for executables/libraries.

1. Re-running dub to regenerate build.ninja/rules.ninja files when dependencies have changed (dub recipe file, dub.selections.json, added/removed source files).

1. Building D projects all at once, per package, or per module, with "per package" being the default.

1. Configuration/variant support (debug/release, build types, platforms/architectures where applicable).

1. Propagation of relevant dub.json / dub.sdl settings (import paths, versions, debug flags, string imports, linker flags, etc.).

1. Relevant tests for all functionality, with a preference for unittest blocks.

## Resources

- [Dub](https://github.com/dlang/dub)
- [Ninja](https://ninja-build.org/)
- [reggae](https://github.com/atilaneves/reggae)
