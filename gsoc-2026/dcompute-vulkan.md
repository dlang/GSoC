---
parent: DLang GSoC 2026 Project Ideas
nav_order: 1
---

# Dcompute Vulkan Backend

**Mentor:** [Nicholas Wilson](iamthewilsonator@hotmail.com)

| Spec | Details |
|-|-|
| **Difficulty Level** | hard |
| **Project Duration** | 350 hours |
| **Number of Contributors** | 1 |
| **Prerequisites** | Compilers (prefereably LLVM and/or DMD), C++ or D, Graphics or Compute APIs (Prefereably vulkan) |

## Description

Dcompute is a compiler extension and runtime library that currently interfaces to OpenCL and CUDA by the SPIRV and PTX backends of LLVM to generate programs that can run D code natively on GPUs.

LLVM's SPIRV backend has recently been enhanced to be able to produce compute shaders for use with the Vulkan API for graphics and compute.

The goal of this project is to extend the LLVM D compiler (LDC) to utilise the new capabilities of the SPIRV backend to produce and run Vulkan compute shaders.

## Project Milestones

- Build LDC + LLVM with the vulkan backend enabled, become familiar with the IR accpted by the SPIRV Vulkan backend
- Add Vulkan as a backend for Dcompute to LDC (see [this PR](https://github.com/ldc-developers/ldc/pull/4958
)
    - add command line switches
    - generate IR in the format accepted by the SRPIV Vulkan backend.
    - Design a consistent ABI for the compiler and Dcompute runtime to interface to each other to launch compute shaders
- Write a dcompute runtime backend to interface to Vulkan
- Test and validate generated shaders using Vulkan

## First Step

Clone and build LDC and LLVM

## Resources

- [LDC](https://github.com/ldc-developers/ldc/)
- [LLVM](https://github.com/llvm/llvm-project/)
- [Dcompute](https://github.com/libmir/dcompute/)
- [This PR](https://github.com/ldc-developers/ldc/pull/4958)
