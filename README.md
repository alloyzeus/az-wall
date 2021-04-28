# AlloyZeus Wall
A wall (of ideas) for AlloyZeus

## What is AlloyZeus?

**NOTE**: AlloyZeus is a codename for the project. It might or might not be
retained as the name of the product.

AlloyZeus is an attempt to build a methodology, modelling language (AZML), a
set of tools, a standard library (stdlib) for AZML, and foundation libraries
(packages) for supported target languages, that allows software developers,
especially software architects, to model a service-oriented system, and then
be able to generate the source code of that system, reactive and end-to-end.

## What problem it attempts to solve?

Bridging the gap between system modelling and actual working systems.

TODO: elaborate

## AZML - AlloyZeus Modelling Language

A quick and dirty peek into the language:

```
domain iam

entity User {
    implements system.User

    # Entity primary identifier definition.
    id {
        # The prefix of the textual representation of the ID.
        prefix KUs0

        # The definition of the numeric representation of the ID.
        num {
            # Here we define that the ID will use 64bit integer
            space 64
            
            # We reserve 48bit for the instance identifiers.
            identifier 48
            
            # We embed some fields, which are part of the identity of the
            # entity. These fields will occupy the remaining bits.
            fields {
                # Fields start at index 1 as index 0 is reserved for
                # the carry bit and for consistency between signed and
                # unsigned integer representations.
                field 1 1 {
                    # A User with the type of Bot was designed to perform
                    # tasks automatically based on triggers.

                    identifier Bot
                }
            }

            # The id-num generator. Root entities (entities which are
            # not adjunct of others) are required to use random number
            # generator.
            generator LocalRandom
        }
    }

    lifecycle {
        creation {
            # We don't expose the creation of a instance of User through
            # cross-process API (cross-process API is disabled by default).
            # An instance of User will be created as the result of
            # an internal process.
            #
            # Operation API visibility options:
            # - public: cross-process (intraprocess is implied). the
            #   generator might generate a REST endpoint, a gRPC call
            #   handler and/or others based on the configured protocols,
            # - intraprocess: cross-module (exported; intramodule
            #   is implied) within a process,
            # - private (default): available within the same
            #   module (unexported).
            operation private
        }

        # The directives for the deletion of instances of the entity.
        # Could an instance be deleted? Who can delete an instance? From
        # where it can be deleted?
        #
        # By default, instances of an entity can not be deleted. We must
        # explicitly declare that a type of entity is deletable.
        deletion enabled {
        
            notes enabled optional

            # A user must be able to delete themselves.
            operation public {
                access {
                    token Bearer
                    
                    # Here we define the authorization as a Polar
                    # policy https://docs.osohq.com/python/getting-started/policies.html
                    check language="polar" {
                        allow(context: CallContext, _method, target: User) if
                            context.application.is_first_party = true and
                            context.application.is_user_agent_authorization_confidential = true and
                            context.user = target;
                    }
                }
            }

            # The directives for the events.
            # Are events generated? Who can listen to the events?
            # Which event dispatch strategy to use?
            #
            # Event API visibility options:
            # - public: cross-process
            # - intraprocess: cross-module within a process
            # - private (default): events are not observable
            #   from the outside of the module
            event public {
                access {}
            }
        }
    }

    attributes {
        DisplayName: thing.Name
    }
}

```

## Related works, concepts and references

- UML
- Domain-driven design
- ThingML
