# Adjunct

Analogous to 'relationship' in ERD.

An adjunct is an object that purpose is to associate an object to one or a set of entity.  
  
The lifecycle of an adjunct is strictly depended on its host entity(s). An adjunct can't outlive any of its hosts.  
  
An adjunct is used to associate a value to an Entity, especially if said entity is declared in another domain. In this case, an adjunct could be considered as an external attribute for the said entity.  
  
Other uses is to describe relationships between two or more instances of entity (a relationship is an object).  
  
TODO: constraint based on a globally ever-increasing value?  
TODO: an adjunct is entity because it can only be attached to entities

Only entities could be host of an adjunct. An adjunct could have one or more hosts depending on the type.
  
One-host example: Messages are adjunct of a Chat. Each message is hosted by one specific Chat.

Multi-host example: "Following" in social media is an adjunct which hosts are "followed user" and "follower user".
  
Multi-host example: A Contract is an adjunct which hosts are Company and Person.


## Types by associated object

In general, adjunct-value is for associating a single instance (one*-to-one)   
and the instance has no self identity, adjunct-entity is for associating  
 multiple instance (one*-to-many) with each having their self identity.

### Adjunct-entities

An adjunct-entity is an entity which the only reason of existence is to provide attribute(s) to, i.e., to describe, its host entity(s). lifecycle is strictly depended on the host entity(s).  
  
Putting it in a different way, an adjunct-entity is an adjunct that each instance has self identity.   
  
Identifier for an adjunct-identity is constructed from its hosts' identifiers and it's own. Example: message 45678 of chat 123 may have an identifier of chat/123/message/45678  
  
Example: Messages in a Chat. Each message in a Chat can be addressed individually.  
  
Example 2: A Contract between Company and Person. An instance of Contract is individually identifiable. Between the same Company and Person, there could be more than one instance of contracts.  
  
TODO: promote the ID of a kind of adjunct-entity to the root-level. for example, in marketplace, we will have something like /product/id . although the product will still be under a shop, it can be addressed globally so that people won't be able to determine the shop based on the product identifier alone. this case might be preferred from the business stand point.

#### ID

ID is the arbitrary identifier for the adjunct-entity.

Adjunct-entity has two parts of identifier: host-derived and own (scoped/local) identifier.  
  
The own-identifier is used to differentiate between instances of the same kind under the same set of hosts. Two instances of the same kind might have the same own-identifier if they are under different hosts.  
  
Unlike root entities, adjunct-entities can have non-random IDs based on their natural ordering.  
  
Using this scheme, we can make some optimizations, e.g., data sharding based on the hosts.  
  
Example: messages in a chat will have IDs which can be ordered chronologically.  
  
A body weight tracker of a person will assign an ID derived (or constructed) from the date-time for an entry.

##### Parts

###### Host-derived parts

Example: a job contract is an adjunct-entity between a company and a person, the host-derived part might look like: /company:75/person:7492/

###### Scoped ID part

### Adjunct-values


## Built-in operation ports

When an adjunct is defined for a host, the host service will provide operations related to the adjunct.

CRUD. Easily translatable to HTTP methods: POST, PUT, DELETE.

### Mutations

#### Add

Related HTTP method: POST.

Requires the appropriate constraint.

E.g., `POST /users/12345/bookmarks` means that we are adding a bookmark (adjunct-value, which value is contained in the HTTP request) to user with ID 12345 (the entity).

TODO: the value object is an identifier.

E.g, `POST /users/12345/email_addresses` means that we are associating an email address (adjunct-entity?) to user with ID 12345 (entity).

#### Set

Related HTTP method: PUT.

E.g, `PUT /users/12345/display_name` means that we are setting the display name (adjunct-value) of user with ID 12345 (entity).

#### Unset

Related HTTP method: DELETE.

## Association constraints

Constraints are defined per adjunct type.

### Cardinality

Defines the limit of adjuncts can be created for the same set of host entities.  
  
Example: the number of Products in a Shop is limited to 1000 at maximum (0..1000).  
  
TODO: there will two types of cardinality: host set and host-specific. In the first case, we'll limit the number of instances for every host combination. In the latter case, we will limit the number of adjunct instances based on the lowest limit among hosts and the global limit.


## Metadata

### Creation

Information about the creation of an adjunction.

#### Creation timestamp

When was the adjunction was created.

#### Creation actor

Who created the adjunction.


### Deletion
