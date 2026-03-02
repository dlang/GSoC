---
parent: DLang GSoC 2026 Project Ideas
nav_order: 1
---

# Make an Offical Hotloading Solution

**Mentor:** Serg Gini

| Spec | Details |
|-|-|
| **Difficulty Level** | medium |
| **Project Duration** | 150 hours |
| **Number of Contributors** | 1 |
| **Prerequisites** | Ancient C api's, understanding of the full lifecycle the compiler, good taste of template api's |

## Description

While C hotloading libs are often 10,000 lines of pure hell. D has `.mangleof` drasticly simplfying such code.  My gist is 40 lines, tho it needs some clean up to call it production ready. We could totally try to ship it.

Hot reloading is often useful for video games or plug ins. Its often a nightmere and could be a competitive edge; not only does D compilers often run 1000x faster then c++, you can make your dev cycle even tighter with a few extra steps.

## Project Milestones

- Understand the code, document the old gist
- Fix the known flaws, find any new ones
- Identify any things to upstream or needing major rewrites
- ???
- Ship it

## First Step

Download gist, make a test for it.

## Resources

- [Gist](https://gist.github.com/crazymonkyyy/e6edc498376da0501c851c8c339eba4b)
