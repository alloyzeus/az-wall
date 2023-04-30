# Entity


## Identity

"No entity without identity."

An entity might be indentifiable with one or more
identifiers.

### ID

A representation of an identity.  
  
Always random for root entities, optionally order-able for adjunct-entities.  
  
For adjuncts, ID is constructed from its hosts and own ID-num if the instance is an adjunct-entity.

## Lifecycle

### Creation

### Deletion

Deletion is not enabled by default.

#### Triggers

##### Actor action

##### Expiration

Expiration is one of the trigger for deletion
of an entity.

Expiration is not enabled by default.  
  
Automatic deletion based on an ever-increasing global value.  
  
Examples of source value: date-time, block ID (in blockchain).

#### Deletion types

##### Vanish

References won't be preserved. It's as if the object never existed.

##### Ghost

All references are preserved but some attributes might be made inaccessible. There will be traces of existence.

Not to be confused with "soft-deletion."

## Ownership

Ownership is a special kind of adjunct. It's an adjunct, generally between two instances of entity, that describes which owns which.

TODO: make a distinction between ownership and adjunction.

### Constraints

Define the rules of operations related to change in ownership.

What are the rules to transfer-in, what are the rules to transfer-out (disassociate).

#### Transferability

Whether an ownable entity can be transferred.

#### Owner cardinality

Constraint the number of owner for an entity.  
  
Example case: an online shop might be owned by more than one user.  
  
TODO: align with cardinality constraint found in adjunct.

#### Time constraint

TODO: other type of ever-increasing value, e.g., block ID. Generalized as trigger.

This also one of the policies.

## Abstraction

Alternative term: trait.

## Service

In contrast to DDD, service in AlloyZeus is a concept under entity instead of under domain. Service is built around entities; for a kind of entity, there will be a service for it.  
  
Services could be build into a single application (services communicates through intra-process ports) or some combination of separate applications for the services, i.e, micro-services (services communicates through network/IP ports).  
  
TODO: service aggregate for a domain.

## Metadata

Metadata are attributes, usually derived from contexts.

TODO: some metadata require declaration
TODO: describe `InstanceInfo`

### Built-in metadata

Metadata usually contains information about the operation related to the entity.

#### Creation

Governed by lifecycle.

##### Creation timestamp

When the entity instance was created. Answers the "when."

##### Creation actor

Which actor created the instance. Answers the "who."

###### Creation terminal

Which terminal was used to initiate the creation.

###### Creation user

Which user initiated the creation.

##### Creation operation ID

The ID of the operation which resulted in the creation of the instance.

#### Deletion

Governed by lifecycle.

##### Deletion timestamp

##### Deletion actor

###### Deletion terminal

###### Deletion user

##### Deletion operation ID

#### Revision ID

Some types of entity will record the revision identifier for any updates to an instance.

For every change to any of the attributes, a new revision identifier will be generated.

## Implementations

### Root entities

## Special entities (abstracts)

These entities are the fundamental entities in an AlloyZeus system.

### Application

An application defines a class of application.

An authenticated service application or authorization user-agent application is called Terminal in AlloyZeus.

#### Agency types

##### User-agent applications

##### Service applications

### User

User is something that have an agency, i.e., the only object that can do operations.

### Terminal

A Terminal is an authorized instance of application. A Terminal is associated to a user if the application is a user agent. If the application is service application, there will be no User reference.  
  
A Terminal is an adjunct of Application and User with User requirement depends on the Application's agency type.

### Session
