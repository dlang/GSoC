---
parent: DLang GSoC 2026 Project Ideas
nav_order: 1
---
# Ship a Protental Phobos Datastructure

**Mentor:**???

| Spec | Details |
|-|-|
| **Difficulty Level** | techically trivail, politically hard |
| **Project Duration** | 100 hours |
| **Number of Contributors** | 1 |
| **Prerequisites** | Some templates, taste in api |

## Description 

As the old saying goes, `datastructures + algorithms = programs` phoboes has 80% of the algorithms I use and is defensable as a canon. Its data structure options, is not.

Linked lists and trees do not address the concerns of large segments of the user base, for me personally I often have these requirements: stable indexes, stable pointers on resizing, O(1) random access delete of continous data; etc. 
There are well know data structures with several of these features, grab one from a c++ stl propasal, or game dev scene.

If its a choose 3 from 4, so be it, if I need 1 of these unaddressed requirements, one data structure may cover 75% of my use cases that slices do not.

## Project Milestones

- Gathered gists from the community, make contract with phobes leadership.
- Pick a front running data structure.
- Working unit tests with map, filter, reduce while following the offical style guide.
- Finalize the api.
- Unit test with rarer range functions.
- Try to PR.

## First Step

Ask the community for data stucture gists and ask the infitely wise leaders for thier requirements. 

## Resources

//TODO: should I link to my gists? c++ talks?
