# Adjunct

Adjunct is a concept that is not found in DDD methodology.

## Properties of adjunct

* An adjunct is an object, which existence is bound to its host entity(s).
  Adjuncts cannot outlive their respective hosts.
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
  
## Usages

### Describing a relationship between objects

A membership is an adjunct which describes a relationship between an
organization an a person.

A more obvious example, a marriage is an adjunct formed between two persons.

### Attaching attributes or objects to an entity

![simple dot](https://user-images.githubusercontent.com/77626/118584955-2ce9f280-b7c2-11eb-8aff-0ee6f14089e5.png)

A job contract adds "a worker" and "company A employee" attributes to
the person it belongs to.

## More examples

A cart in an online store is an adjunct with type of value-object of a user. A cart's
existence is exclusively bound to its user, and one user has only one cart. A cart
does not to be referenceable so it does not need to be an entity.

![two-entities dot](https://user-images.githubusercontent.com/77626/118584866-01ff9e80-b7c2-11eb-9d5e-1e11e6beb5df.png)

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

#### Two hosts of the same kind

A user-to-user chat is an adjunct of two instances of User. Identifier for this
chat must be consistent. As the identifier is constructed from each user's
identifier, the ordering must be determined.

We must should also provide a way to prevent an adjunct which hosts are the
same instance. By default we'll allow any adjunct to have hosts that are the
same instance (in messenger example, this is a self-chat).

#### Ownership as a special adjunct

### Syntax-related discussions

#### Inline adjunct definition in its first host

This could work if the adjunct and its first host are in the same module.
An adjunct of a host defined in another module is always non-inline;
it's not possible as this will be a form of circular dependency, and we
will never have any support for circular dependency in AZML.

#### Describing cardinality (and exclusivity or uniqueness)

Session is an adjunct entity of Terminal, but the number of Session at
a given time is limited to at most one.

What we want is a syntax to express the following examples:

- "the cardinality of Manager to Shop is 1..3" -- one Shop may have one
  to three Managers.
- "the cardinality of Session to Terminal is 0..1" -- one Terminal may
  have one Session at most.

A more complex case (fictious): one Shop may have one to three Managers,
and one User can be a Manager of two Shops at most.
