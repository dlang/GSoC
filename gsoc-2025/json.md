---
parent: DLang GSoC 2025 Project Ideas
nav_order: 4
---

# Json Library

**Mentor:** [Adam Wilson](gamedevelopmental@gmail.com)

| Spec | Details |
|-|-|
| **Difficulty Level** | medium |
| **Project Duration** | 175 hours |
| **Number of Contributors** | 1 |
| **Prerequisites** | json, parsers, object oriented programming |

## Description

D currently does not have a json parser integrated in the [standard library](https://github.com/dlang/phobos/) and it is the year 2025.
There are 3rd party libraries that implement some pieces to a certain extent, however they are not at industry level requirements.
The purpose of this project is to create a json library that offers all the facilities required for working with json objects.
The goal is to eventually integrate it in the standard library, however, an initial step is to publish as a [dub (D package manager)](https://code.dlang.org/) package.

Although there is no json library in the D ecosystem, there are multiple json parser implementations.
We can start by picking up a notable [json parser](https://github.com/schveiguy/jsoniopipe) as a basis for our implementation.
Next, we can built higher level functionalities on top of the existing parser.

This project is of high priority and impact, as json objects essentially rule the world.

## Project Milestones

1. Initial Package Setup and Porting from jsoniopipe.
1. Object Model Design/Implementation.
1. Object Model Serialization/Deserialization
1. Streaming Serialization/Deserialization
1. Stretch Goal: Object Serialization/Deserialization (Direct serialization/deserialization from a D object instead of using the object model.)

## Resources

- [jsoniopipe](https://github.com/schveiguy/jsoniopipe)
