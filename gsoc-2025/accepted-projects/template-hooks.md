---
parent: Accepted Projects
nav_order: 1
---

# Translate DRuntime Hooks to Templates

<img width="100px" src="https://summerofcode.withgoogle.com/assets/media/gsoc-generic-badge.svg" align="right" />

Contributor: [Albert Guiman](https://github.com/albert24gg)

Mentor: [Teo Dutu](https://github.com/teodutu)

## Project Overview

**D** is a systems programming language that features some built-in high-level constructs and operations such as casting, array creation, array append, associative arrays, and more. Unlike other languages, these are part of the language syntax and not part of the standard library, so they do not require the programmer to explicitly call any function. This is made possible by runtime hooks, which are functions that replace these high-level constructs. The process is called "lowering" and is done by the compiler during the semantic analysis phase.

Initially, these hooks were implemented as normal functions that have a `TypeInfo` parameter, which is a type descriptor that contains information about the type of the value being operated on. This approach is inefficient, as it relies on type information being queried at runtime, introducing some overhead that is, in most cases, unnecessary, because the compiler already has this information at compile time and can inject it directly into the hook. Since D features a powerful template system, there has been a push to replace these runtime hooks with template-based implementations, but not all hooks had been translated yet.

The goal of this project was to translate the remaining DRuntime hooks to templates, which will allow for potentially better optimization opportunities, on top of improving the maintainability of the codebase and ease of integration by other compilers, such as LDC and GDC.

## Contributions

My contributions are split into multiple smaller PRs, each focusing on a specific hook, or addressing related issues. The following is a list of the PRs I worked on during the GSoC period:

- **Templated Hooks**:
  - **Array Hooks**: [\_d_arraysetcapacity](https://github.com/dlang/dmd/pull/21143), [\_d_arrayappendcTX](https://github.com/dlang/dmd/pull/21205), [\_d_arrayshrinkfit](https://github.com/dlang/dmd/pull/21373), [\_adEq2](https://github.com/dlang/dmd/pull/21513), [\_d_arrayliteralTX](https://github.com/dlang/dmd/pull/21567)
  - **Casting Hooks**: [\_d_dynamic_cast](https://github.com/dlang/dmd/pull/21402), [\_d_paint_cast](https://github.com/dlang/dmd/pull/21427), [\_d_class_cast](https://github.com/dlang/dmd/pull/21440), [\_d_interface_cast](https://github.com/dlang/dmd/pull/21473)
- **Misc**:
  - **Refactoring**: [Refactor `_d_arrayliteralTX`](https://github.com/dlang/dmd/pull/21573), [Cleanup unused symbols](https://github.com/dlang/dmd/pull/21629), [Move lowering of `ConstructExp` to a dedicated field](https://github.com/dlang/dmd/pull/21706), [Refactor `_d_cast`](https://github.com/dlang/dmd/pull/21727)
  - **Bug Fixes**: [Add missing exception handling in `_d_arrayappendT`](https://github.com/dlang/dmd/pull/21699), [Account for lowering during post-order visit on `CatExp`](https://github.com/dlang/dmd/pull/21701)
  - **Performance**: [Improve performance of `_d_arrayctor`](https://github.com/dlang/dmd/pull/21675)

For some of these hooks, the lowering was already implemented in the compiler and my only concern was the templatization of the hook itself, but for most of them I needed to modify the frontend, usually `expressionsem.d` and `e2ir.d`, to introduce the lowering logic. This was often not a trivial task, as I had to ensure the behavior matched the previous implementation and new issues/bugs were discovered in the process. That's why a fairly large part of my time was spent on debugging and testing.

In addition to my work on the DMD compiler, I have also contributed to the repository dedicated to [hook benchmarks](https://github.com/teodutu/druntime-hooks-benchmarks), which was started by my mentor, Teo Dutu. This was a great way to test any performance improvements or regressions introduced by the new template-based implementations, allowing me to apply fixes as needed. All the PRs I made to this repo can be found in the [Pull Requests section](https://github.com/teodutu/druntime-hooks-benchmarks/pulls?q=is%3Apr+is%3Aclosed+author%3AAlbert24GG).

During this period, I also documented my progress through weekly forum posts on the [D Programming Language forum](https://forum.dlang.org/group/general):

- [Week 1](https://forum.dlang.org/thread/mytrsiwjqqkyakiizvuq@forum.dlang.org)
- [Week 2](https://forum.dlang.org/thread/wpvfdabhpkscxggeoaho@forum.dlang.org)
- [Week 3](https://forum.dlang.org/thread/adhvwscqzxlhebbwgvnt@forum.dlang.org)
- [Week 4](https://forum.dlang.org/thread/hormnqkocgrvobdylfih@forum.dlang.org)
- [Week 5](https://forum.dlang.org/thread/ctrtjtmclyqmitkskvnv@forum.dlang.org)
- [Week 6](https://forum.dlang.org/thread/yaiggslkvaentnsbbziy@forum.dlang.org)
- [Week 7](https://forum.dlang.org/thread/jeclwhptacrrnezfkqtg@forum.dlang.org)
- [Week 8](https://forum.dlang.org/thread/timgzbqiszicuiwghuio@forum.dlang.org)
- [Week 9](https://forum.dlang.org/thread/nevwccmnxstnijjkysnw@forum.dlang.org)
- [Week 10](https://forum.dlang.org/thread/ejpqoyhtmtmghtzsqcaa@forum.dlang.org)
- [Week 11](https://forum.dlang.org/thread/nzdbyjldbpdkvmckcsna@forum.dlang.org)
- [Week 12](https://forum.dlang.org/post/cshtuveaypwlmuqgxbwy@forum.dlang.org)

## Current Status

As of the end of GSoC, I have successfully translated all the hooks that were planned for this project. Using the aforementioned benchmark repository in conjunction with the DMD compiler, I have verified that the performance of the new template-based implementations is comparable to the old ones, and in some cases, even better. The results can be found in the [benchmark repository](https://github.com/teodutu/druntime-hooks-benchmarks/tree/master/performance), under each hook's folder.

DMD serves as the reference compiler for the D language, providing the shared frontend used by all major D compilers, while its backend is distinct from those of LDC (LLVM-based) and GDC (GCC-based). Although DMD is performance-oriented in terms of compilation speed, past benchmarks [\[1\]](https://programming-language-benchmarks.vercel.app/d) [\[2\]](https://github.com/kostya/benchmarks?tab=readme-ov-file#test-cases) have shown that the code generated by its backend is generally not as fast as that produced by LDC or GDC. Changes to the DMD compiler take some time to be integrated into these third-party compilers, so I was unable to truly benchmark the performance of the new hooks. However, I have tested the hooks that have been translated into templates a while ago and are already available in LDC and GDC, which should provide a reasonable indication of the improvements to expect.

Below are two tables summarizing the performance gains running the benchmarks (excluding tests having _1Elems_ in their name), as well as the size increase of the `libdruntime` and `libphobos` (D's standard library) libraries, when utilizing LDC and GDC, respectively. The machine used was an Intel i5-12400 with 8GB of RAM, running Debian 12. As mentioned earlier, the full results can be found in the [benchmark repository](https://github.com/teodutu/druntime-hooks-benchmarks/tree/master/performance).

| Hook                  | Performance Gain | libdruntime/libphobos size increase | libphobos compilation time increase |
| --------------------- | :--------------: | :---------------------------------: | :---------------------------------: |
| `_d_arrayctor`        |     30 - 99%     |         ~ 3.5% / -2.4 - -2%         |                ~ -2%                |
| `_d_arrayappendT`     |     1 - 83%      |         ~ 2.2% / 2.2 - 2.7%         |               ~ 0.4%                |
| `_d_arraycatnTX`      |     3 - 88%      |           ~ 2% / -3 - -8%           |              ~ -10.7%               |
| `_d_arrayassign`      |     61 - 99%     |       ~ -0.5% / -4.1 - -3.9%        |               ~ -2.6%               |
| `_d_newarraymTX_2D`   |     18 - 46%     |         ~ 1% / -3.3 - -8.3%         |               ~ -10%                |
| `_d_newarraymTX_3D`   |     21 - 32%     |         ~ 1% / -3.3 - -8.3%         |               ~ -10%                |
| `_d_arraysetcapacity` |     13 - 24%     |         ~ -0.8% / 1 - 1.3%          |               ~ 0.5%                |

| Hook                | Performance Gain | libdruntime/libphobos size increase | libphobos compilation time increase |
| ------------------- | :--------------: | :---------------------------------: | :---------------------------------: |
| `_d_arrayappendT`   |    -38 - 38%     |          ~ 3% / 3.3 - 4.7%          |                ~ 1%                 |
| `_d_arrayassign`    |     -8 - 82%     |             ~ 0% / 0.1%             |               ~ 1.4%                |
| `_d_newarrayT`      |     5 - 13%      |         ~ 3.6% / 0 - 15.6%          |                ~ 3%                 |
| `_d_newarrayiT`     |     11 - 16%     |         ~ 3.6% / 0 - 15.6%          |                ~ 3%                 |
| `_d_newarraymTX_2D` |     3 - 17%      |         ~ 2.4% / -1.9 - 14%         |               ~ 0.1%                |
| `_d_newarraymTX_3D` |     -9 - 28%     |         ~ 2.4% / -1.9 - 14%         |               ~ 0.1%                |

{: .note }

> - The workloads tested consisted of simple array operations that trigger the respective hooks.
> - Each benchmark is made up of multiple tests, each with different parameters, such as the number of elements and the size of each element.
> - Each test's run time is measured over 1 million iterations, the results being averaged over multiple runs, usually 20.
> - The commits tested for the templated/non-templated hooks are usually adjacent, so that the differences are minimized, but in some cases there might be gaps of a few commits. That happened, for example, when the templated hook made use of different GC features which made it slower, but a later commit improved the performance by either optimizing the hook itself or the GC feature used.

As you can see, GDC exhibits some inconsistent results for some of the hooks, with both performance gains and losses depending on the test parameters. This is unlike what we have seen with LDC, which indicates that GDC doesn't optimize the code as well as LDC on our testing system.

With some help from [Iain](https://github.com/ibuclaw), the maintainer of GDC, we discovered that the performance regression was due to a lack of inlining for the templates. By default, D templates are emitted as weak symbols, which means that a function's body could be overwritten at link time, so due to the One Definition Rule, the compiler cannot inline them. GDC is apparently the only D compiler that adheres to this rule. To instead emit the templates to COMDAT sections, which allows inlining, the `-fno-weak-templates` flag needs to be passed to GDC. After doing so, the performance improved significantly, as shown in the table below:

| Hook                | Performance Gain |
| ------------------- | :--------------: |
| `_d_arrayappendT`   |    -17 - 55%     |
| `_d_arrayassign`    |     27 - 99%     |
| `_d_newarrayT`      |     5 - 13%      |
| `_d_newarrayiT`     |     20 - 41%     |
| `_d_newarraymTX_2D` |     19 - 41%     |
| `_d_newarraymTX_3D` |     27 - 33%     |

## Future Work

Based on the benchmark results above, the only noticeable performance issue seems to be with some tests of the `_d_arrayappendT` hook when using GDC. Further investigation would be required to determine the cause and implement a fix.

Given that real performance changes will be seen with LDC and GDC, the next step is to perform benchmarks on the hooks as soon as they are integrated into these compilers. This will allow us to observe any performance regressions, find the root cause of the issue and fix it. On top of that, some of the hooks directly call other hooks that may not have been integrated when I performed the benchmarks presented above. Therefore, it would be ideal to rerun all benchmarks once all the templated hooks are integrated into the compilers, so that any performance dependencies are accounted for.

Another beneficial addition could be refactoring the hooks where needed, including some cleanup and simplification of the code. As time goes on, some bugs or unhandled edge cases might be discovered, so they will need to be addressed as well, potentially adding new tests to the test suite.
