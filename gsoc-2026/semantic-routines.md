---
parent: DLang GSoC 2026 Project Ideas
nav_order: 2
---

# Separate Semantic Routines From AST Nodes

**Mentor:** [Razvan Nitu](razvan.nitu1305@gmail.com)

| Spec | Details |
|-|-|
| **Difficulty Level** | easy-medium |
| **Project Duration** | 175 hours |
| **Number of Contributors** | 1 |
| **Prerequisites** | Familiarity with compiler organization, visitor pattern, object oriented programming |

## Description

In the DMD compiler codebase, AST nodes are defined as classes within various files.
The ideal structure for these nodes is to have minimal fields and methods focused solely on field queries.
However, the current state of the DMD frontend deviates from this ideal.
AST nodes are laden with numerous methods that either perform or are dependent on semantic analysis.
Furthermore, many AST node files contain free functions related to semantic analysis.
Our objective is to decouple AST nodes from these functions.

## How to start working on this project

1. Clone the compile repository - check [this guideline](https://github.com/dlang/dmd/blob/master/CONTRIBUTING.md).
1. Choose an AST node file: start by selecting a file from [this list](https://github.com/orgs/dlang/projects/41) of AST node definition files.
1. Examine Imports: open your chosen file and scrutinize the top-level imports.
1. Isolate semantic imports: temporarily comment out one of the imports that includes semantic routines, particularly those ending in sem (e.g., dsymbolsem, expressionsem, etc.).
1. Build and identify dependencies: compile DMD and observe any unresolved symbols that emerge.
1. Relocate functions: shift the functions reliant on the unresolved symbols to the semantic file where the import was commented out.
1. Move and test a function: select a function for relocation and ensure it functions correctly in its new location.
1. Submit a Pull Request: Once you're satisfied with the changes, create a PR that follows [the guidelines](https://github.com/dlang/dmd/blob/master/CONTRIBUTING.md).

Check this [PR](https://github.com/dlang/dmd/pull/15755) for an illustration of the above steps.

Sometimes, more intricate solutions are required.
For instance, if an overridden method in an AST node calls a semantic function, it can't be simply relocated.
In these cases, using a visitor to collate all overrides, along with the original method, into the appropriate semantic file is the way forward.
A notable instance of this approach is detailed in [this pull request](https://github.com/dlang/dmd/pull/15782).

Other complex scenarios may arise, especially when dealing with AST nodes that interact with the backend.
Finding solutions to those will be the fun part of the project.

This project helps advance the development of the compiler library by creating a clear separation between compilation phases.

This project is ideal for someone that has no prior experience with real-life compilers but wants to start by doing valuable work.

Recently, progress has been made on this project, so in case the dependency is broken, we can advance by improving the dmd as a library project, which directly depend on the completion of this project.

## Resources

- [Compiler codebase](https://github.com/dlang/dmd/tree/master/compiler/src/dmd)
- [List of files that need to have semantic separated out of them](https://github.com/orgs/dlang/projects/41/views/1)
- [How to start](https://github.com/dlang/dmd/blob/master/CONTRIBUTING.md#refactoring-the-dmd-ast)
- [Building the compiler](https://wiki.dlang.org/Building_under_Posix#Building_DMD)
