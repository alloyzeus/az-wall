# Concepts

* Entity -- An object that is defined by a thread of continuity and
  its identity.
* Adjunct -- An object which existence is bound to its host(s). Used
  to define the relationships and/or to provide attributes for its host(s).
* Abstract -- A set of traits which could be implemented by entities.

## Objects

|               | has identity   | have no identity |
|---------------|----------------|------------------|
| _independent_ | (root) entity  | value object     |
| _dependent_   | adjunct entity | adjunct (v.o.)   |

So, where's **aggregate**?

An aggregate is a representation of an entity. An aggregate is
constructed from adjuncts of that entity. The entity could be
root entity or adjunct entity.

A real-world example. A résumé is an aggregate with a person as the
entity. A detail like where that person is currently working is coming
from an adjunct in form of job contract.
