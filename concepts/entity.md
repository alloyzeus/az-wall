# Entity

The concept of entity in AlloyZeus is roughly similar to that of found in Domain-Driven
Design methodology.

## Properties of entity

### An entity distinguished by its identity

Not by its attributes. An attribute, or combination of them, might be used
to identify an entity, but attributes are not part of identity.

### An entity has an identity, always

Identity is the essence of existence of an entity.

### Identity makes entities referenceable

Any object which requires to be referenceable, needs to be an entity.

### Identity is not the same as identifier

A name assigned to a person is an identifier, not their identity. If the person
decided to change their name, their identifier changes but their identity does not.

### Identity of an entity is non-reassignable, non-replaceable, non-nullable

### Identities are non-recycleable

An identity is not reassignable even though the entity it was assigned to has been
disposed of.

### Entity may have attributes

## Two forms of entity

There are two forms of entity based on whether it's standing on its own
which we use the term root entity, or as adjunct.

## Entity persistency

## Service

Each entity has its own service. Every service is built around entity(s).

## Discussions

### Explain the relationship between identity and ID

### Service API visibility, access control

For an interface in API, it should be determined whether it will be
used vertically or horizontally.

APIs which were designed to be used horizontally, they will be accessed
by the same service in different instances. This is for horizontal
scaling purposes. An example of horizontal API is an interface to determine
whether another user is online by checking if that user is connected to any
node.
