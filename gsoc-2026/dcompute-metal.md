---
parent: DLang GSoC 2026 Project Ideas
nav_order: 5
---

# Dcompute Metal Backend

**Mentor:** [Nicholas Wilson](iamthewilsonator@hotmail.com)

| Spec | Details |
|-|-|
| **Difficulty Level** | hard |
| **Project Duration** | 350 hours |
| **Number of Contributors** | 1 |
| **Prerequisites** | Compilers (prefereably LLVM and/or DMD), Language (C++, Objective-C or D), access to Metal capable hardware, Ideally Graphics or Compute APIs (Prefereably Metal) |

## Description

Dcompute is a compiler extension and runtime library that currently interfaces to OpenCL and CUDA by the SPIRV and PTX backends of LLVM to generate programs that can run D code natively on GPUs.

Apple's Metal also uses LLVM, and now that LDC has full `extern(Objectice-C)` support for Apple's Metal API is important to extend the platform support for dcompute.

The goal of this project is to extend the LLVM D compiler (LDC) to be able to produce Metal shaders from D code and then build a runtime the wraps the Metal Objective-C API to launch, test and validate the shaders.

## Project Milestones

- Build LDC, become familiar with the IR accpted by the `metal`/`metal-ar` compiler tools
- Add Metal as a backend for Dcompute to LDC (see e.g. [this PR](https://github.com/ldc-developers/ldc/pull/4958) for Vulkan)
    - add command line switches
    - generate IR in the format accepted by the `metal``.
    - Design a consistent ABI for the compiler and Dcompute runtime to interface to each other to launch compute shaders
- Write a dcompute runtime backend to interface to Metal
- Test and validate generated shaders using Metal

## First Step

Clone and build LDC and LLVM

## Resources

- [LDC](https://github.com/ldc-developers/ldc/)
- [LLVM](https://github.com/llvm/llvm-project/)
- [Dcompute](https://github.com/libmir/dcompute/)
- [This PR](https://github.com/ldc-developers/ldc/pull/4958)
- [D Metal bindings](https://code.dlang.org/packages/metal-d)
