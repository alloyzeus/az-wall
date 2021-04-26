# azml-wall
A wall (of ideas) for AZML

## What is AZML?

AZML stands for AlloyZeus (that's a codename) Modelling Language.

AZML is an attempt to build a modelling language and tool set (compiler and stuff) which allow
software developers, especially software architects, to model the system and then generate
the source code of the modelled system.

```

entity User {
    implements system.User

    id {
        prefix KUs0
        id_num {
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

        deletion enabled {

            # A user must be able to delete themselves.
            # Options:
            # - public: cross-process (intraprocess is implied). the generator might generate a REST endpoint, a gRPC call handler and/or others based on the configured protocols,
            # - intraprocess: cross-module (exported; intramodule is implied) within a process,
            # - intramodule (default): available within the same module (unexported)
            api public {
                access {
                    token Bearer {
                        user allow
                        service disallow
                    }
                    
                    check ($subject == $target)
                    # As an alternative, declare in Polar of OSO https://docs.osohq.com/python/getting-started/policies.html
                    check language="polar" {
                        allow(callContext: CallContext, _method, target: User) if
                            callContext.Actor.User = target
                    }
                }
            }

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
