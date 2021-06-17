# Concepts

* Entity -- An object that is defined by a thread of continuity and
  its identity.
* Adjunct -- An object which existence is bound to its host(s). Used
  to define the relationships and/or to provide attributes to its host(s).
* Abstract -- A set of traits which could be implemented by entities.

## Objects

|               | has identity   | no identity      |
|---------------|----------------|------------------|
| _independent_ | (root) entity  | value object     |
| _dependent_   | adjunct entity | adjunct (v.o)*   |

Note: even though does not have its own identity, an adjunct could still
be addressed/referenced through the combination of its hosts' identifiers.

So, where's **aggregate**?

An aggregate is a representation of an entity. An aggregate is
constructed from the adjuncts of that entity. The entity could be a
root entity or an adjunct entity.

A real-world example. A résumé is an aggregate with a person as the
entity. A detail like where that person is currently working for is
coming from an adjunct in form of a job contract.
