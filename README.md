# AlloyZeus Wall
A wall (of ideas) for AlloyZeus

## What is AlloyZeus?

**NOTE**: AlloyZeus is a codename for the project. It might or might not be
retained as the name of the product.

AlloyZeus is an attempt to build a methodology, a modelling language (AZML),
a set of tools, a standard library (stdlib) for AZML, and foundation
libraries (packages) for supported target languages, that allows software
developers, especially software architects, to model a service-oriented
system, and then be able to generate the source code of that system,
reactive and end-to-end.

Mind map: https://www.mindmeister.com/1593890042/alloyzeus-components

## What problem it attempts to solve?

Bridging the gap between system modelling and actual working systems.

TODO: elaborate

## Goals

- Faster iteration.
- Automate All The Things! Including the coding. Reduce the area with
  error potential by removing manual code writing.
- Single source of truth for the whole system. The documentations
  (including charts and visualizations), server applications,
  APIs/protocols, data schema migrations, configuration schema, client
  applications/SDKs, and even deployment and publishing directives, are
  all generated from a single source. No more lying documentations, no
  more duplicated efforts to update an endpoint.
- Transparent and open by generating codebase rather than as a fully
  black-box systems like other no-code / low-code solutions. System
  owners could inspect the codebase of their systems and they have the
  options to continue the development of those systems manually.

## Working strategy

- Use existing methodologies, concepts, technologies and their
  implementations as the starting point. Try to avoid
  developing/introducing new things. Find existing works that have matured.
  They are usually battle-proven and a number people are already
  familiar with them.
- Sometimes, it's better to start of with a completely new concept and
  then merge it with other concepts later on than bending existing
  concepts. When it's required to introduce a new concept, use the most
  relevant real-world concept as the base.
- Observe the pain points from real-world practice and think the solution
  for those pains. Don't address them individually but attempt to
  correlate with others. Some individual pains could be addressed with
  a single solution.
- Reality-check by reproducing existing, in-production systems.
- Break down everything, decompose everything. Construct new concepts
  from those parts.

## The Methodology

Mind map: https://www.mindmeister.com/1898713101/alloyzeus-methodology

## AZML - AlloyZeus Modelling Language

While in general purpose languages we are talking about classes or structs,
in AZML we talk about entities, adjuncts, value objects, and services.

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
            # Procedure API visibility options:
            # - public: cross-process (intraprocess is implied). the
            #   generator might generate a REST endpoint, a gRPC call
            #   handler and/or others based on the configured protocols,
            # - intraprocess: cross-module (exported; intramodule
            #   is implied) within a process,
            # - private (default): available within the same
            #   module (unexported).
            procedure private
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
            procedure public {
                access {
                    token Bearer
                    
                    # Here we define the authorization as a Polar policy
                    # https://docs.osohq.com/python/getting-started/policies.html
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

We have not implemented a parser for such language. Meanwhile, we start
from the parsed structures:
[iam.yaml](https://github.com/alloyzeus/az-wall/blob/master/case-studies/iam.yaml).
For the untouched generated Go code from the YAML file:
[user__azgen.go](https://github.com/kadisoka/kadisoka-framework/blob/562fadec0bc1a7f694959fcfea82043427881796/iam/pkg/iam/user__azgen.go)) 

## Related works, concepts and references

- UML
- Domain-driven design
- [Modelica](https://modelica.org/documents/MLS.pdf)
- ThingML
