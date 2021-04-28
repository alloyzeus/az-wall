# AlloyZeus Wall
A wall (of ideas) for AlloyZeus

## What is AlloyZeus?

**NOTE**: AlloyZeus is a codename. We might or might not retain it as the
name of the product.

AlloyZeus is an attempt to build a methodology, modelling language (AZML), a
set of tools, a standard library (stdlib) for AZML, and support libraries
(packages) for supported target languages which allow software developers,
especially software architects, to model a service-oriented system, and then
be able to generate the source code of that system, end-to-end.

## What problem it attempts to solve?

Bridging the gap between system modelling and working systems.

TODO: elaborate

## AZML - AlloyZeus Modelling Language

A quick and dirty peek into the language:

```

entity User {
    implements system.User

    id {
        prefix KUs0

        num {
            space 64
            identifier_space 48
            embedded_fields {
                field 1 1 {
                    # Bot account is ....

                    identifier Bot
                }
            }

            generator LocalRandom {

            }
        }
    }

    lifecycle {
        creation {
            # We don't expose the creation of a instance of User through
            # cross_process_api (cross_process_api is disabled by default).
            # An instance of User will be created
            # as the result of internal process.
        }

        # The directives for the deletion of instances of the entity.
        # Could an instance be deleted? Who can delete an instance? From where it can be deleted?
        #
        # By default, instances of an entity can not be deleted. We must explicitly declare that a type
        # of entity is deletable.
        deletion enabled {
        
            notes enabled optional

            # A user must be able to delete themselves.
            # Options:
            # - public: cross-process (intraprocess is implied). the generator might generate a REST endpoint, a gRPC call handler and/or others based on the configured protocols,
            # - intraprocess: cross-module (exported; intramodule is implied) within a process,
            # - intramodule (default): available within the same module (unexported)
            operation public {
                access {
                    token Bearer
                    
                    # Here we define the authorization as a Polar policy https://docs.osohq.com/python/getting-started/policies.html
                    check language="polar" {
                        allow(context: CallContext, _method, target: User) if
                            context.Application.IsFirstParty = true and
                            context.Application.IsUserAgentAuthorizationPublic = true and
                            context.User = target;
                    }
                }
            }

            # The directives for the events.
            # Are events generated? Who can listen to the events? Which event dispatch strategy to use?
            #
            # Options:
            # - public: cross-process
            # - intraprocess: cross-module within a process
            # - none (default): not generating events
            event public {
                access {}
            }
        }
    }

    attributes {
        DisplayName: thing.Name {

        }
    }
}

```

## Related works, concepts and references

- UML
- Domain-driven design
- ThingML
