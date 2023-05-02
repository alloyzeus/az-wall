# AlloyZeus Methodology

## Objects

### Core object types

#### [Entities](entity.md)

#### Value objects

### Supporting object types

#### Adjuncts

An entity on its own does not have any attributes. To associate an value or object to an entity, a new type of object is required.

An adjunct can be used to associate a value object to an entity. It can also be used to associate an entity with another entity, i.e., define the relationships between entities.

Adjunct is a concept of associating object(s) with other object(s).

If the one that being associated is an entity, it is analogous to 'relationship' in ERD.

An adjunct is an object that purpose is to associate an object to one or a set of entity.  
  
The lifecycle of an adjunct is strictly depended on its host entity(s). An adjunct can't outlive any of its hosts.  
  
An adjunct is used to associate a value to an Entity, especially if said entity is declared in another domain. In this case, an adjunct could be considered as an external attribute for the said entity.  
  
Other uses is to describe relationships between two or more instances of entity (a relationship is an object).

TODO: constraint based on a globally ever-increasing value?  
TODO: an adjunct is entity because it can only be attached to entities

#### Aggregates

Similar concepts: View in SQL, a model in GraphQL.

An aggregate is an object representing an entity.

Aggregate requires adjuncts to work.
  
An aggregate describes an instance of Entity by collecting adjuncts which any of hosts is said entity.
  
An aggregate doesn't have its own attributes. Every value accessible through an aggregate is is either sourced directly from an entity or its adjunct, or derived from them (e.g., BMI is calculated from adjuncts body height and body weight of a person entity). An aggregate is a rule on how to represent and entity.
  
Example: A CV describes a Person. It lists his work history (each work is an adjunct).

Aggregates has only read port.


### Attributes


## Ports

### Types

### Access control

Every port could be guarded by access control policies. Information required by authorization checks are generally obtained from the contexts.

#### Policies

##### Expression language

### Visibility

Visibility is not access control. A port might be public but it might be possible that nobody could actually perform an operation through that port.

#### Public

API is accessible from other processes.

#### Intra-process

Across module, within an application process.

#### Private

Within the module/package.
