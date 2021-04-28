# Adjunct

Adjunct is a concept that is not found in DDD methodology.

## Properties of adjunct

* An adjunct is an object, which existence is bound to its host entity(s).
* Adjunct host must be object with the type of entity.
* An adjunct can have one or more hosts.
* The type(s) and the the number of the host(s) are static.
* Adjunction is not bound to domains. An adjunct could be created from
  entities from various domains as long as there is no circular dependencies.
* Two types of adjunct: _entity_ and _value object_:
  - An adjunct with a type of value object is always have one-to-one to
    all of its hosts
  - An adjunct with a type of entity could be made to have any kind of
    cardinality to its host(s). The constraints must be defined as AZML.
  
## Types of usage

### Describing a relationship between objects

A membership is an adjunct which describes a relationship between an
organization an a person.

A more obvious example, a marriage is an adjunct formed between two persons.

### Attaching attributes to an entity

A job contract adds "a worker" and "company A employee" attributes to
the person it belongs to.

## More examples

A cart in an online store is an adjunct with type of value-object of a user. A cart's
existence is exclusively bound to its user, and one user has only one cart. A cart
does not to be referenceable so it does not need to be an entity.

A job contract is an adjunct, with type of entity, which hosts are a company and a person.
A job contract needs to be referenceable and between the same hosts, there might be more
than one instance of contract.

## Discussions

### Concept-related discussions

#### Optional hosts

An adjunct must have at least one host, the first one, that is required, but it might
allow the rest to be optional.

There's a case in IAM. A Terminal is an adjunct entity formed between an Application
and a User. The requirement of the User part depends on the the agency type of the
Application. If the Application is a user-agent, User must be provided; if the
Application has a type of service (non-user-representing application), User must
not be provided.

#### Ownership as a special adjunct

### Syntax-related discussions

#### Inline adjunct definition in its first host

This could work if the adjunct and its first host are in the same module.
An adjunct of a host defined in another module is always non-inline;
it's not possible as this will be a form of cyclic dependency, and we
will never have any support for cyclic dependency in AZML.

#### Describing arity (and exclusivity or uniqueness)

Session is an adjunct entity of Terminal, but the number of Session at
a given time is limited to at most one.
