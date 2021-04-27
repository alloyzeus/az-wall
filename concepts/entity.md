# Entity

The concept of entity in AZML is roughly similar to that of found in Domain-Driven
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

### Identities are forever

Once assigned, an identity is reserved to particular entity, even though the entity
has been disposed of.

### Entity may have attributes