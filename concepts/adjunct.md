# Adjunct

> A contract is an adjunct which hosts are the parties which bound by the said contract.

## Properties of adjunct

- two types of adjunct: entity and value object
- an adjunct with a type of value object is always have one-to-one to all of its hosts
- an adjunct with a type of entity could be made to have any kind of cardinality to its host(s).
  The constraints must be defined as AZML.

## Discussions

### Syntax-related discussions

#### Inline adjunct definition in its first host

This could work if the adjunct and its first host are in the same module.
An adjunct of a host defined in another module is always non-inline;
it's not possible as this will be a form of cyclic dependency, and we
will never have any support for cyclic dependency in AZML.
