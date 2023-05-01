# Marketplace

```
domain marketplace

entity Store {
  id {
    prefix MSh
  }
  
  lifecycle {
    creation {
      # TODO:
      # A creation must respect ownership
      # and constraints defined in the
      # attributes.
      # With a user who owns two stores,
      # any attempt to create another store
      # will be rejected.
      # With a user who manages three strores,
      # any attempt to create a store
      # will be rejected.
    }
  }

  ownership {
    # A store ownership could be transferred
    transfer enabled {
    }

    # A store has at least one owner but no more than two owners
    owner_cardinality 1..2
  }
  
  attributes {
    DisplayName: {
      name-is-prepared false
      access {
        read: allow all
        update: allow if $user is in $realm.Administrators
      }
    } thing.Name {
      # can be used to provide parameters to the type
      symbols disallow
      length-min 5
    }

    Categories: set {
      cardinality 0..4
      access {
        read: allow all
        add: allow if $user is owner or in Managers
      }
    } of Category {}

    # Attribute managers is a set of Manager.
    Managers: set {
      # How many managers can a store have.
      # TODO: a way to make this settable from a dashboard. If it can be set dynamically, there should be a rule for the existing data (e.g., update or keep or other strategy like notify the owners for a period of time).
      cardinality {
        configurable env
        on-config-change keep-data
        default 1..3
      }
    } of value Manager {
      # A manager of a store
      # does not need to be addressable.
      # We can use `value` instead `entity`.

      rels {
        # As the primary key in the table,
        # we are compounding
        # the entity Store with entity iam.User.
        # the entity Store is implicit.
        iam.User {
          # One user can be a manager of up to 3 stores.
          cardinality to Store 0..3
        }
      }

      # TODO: the creator will automatically become a manager
    } {
      # This section can
      # be used to provide parameters
      # for the type
    }

    Showcases: ordered set {
      cardinality 0..20
      default-ordering $creation.timestamp desc
    } of entity Showcase {
      id {
        prefix SC
        uniqueness-scope host
      }

      attributes {
        Articles: ordered set {

        } of Article {

        }
      }
    }
    
    # ...
  }

  # An article needs to be addressable
  adjunct entity Article {
    id {
      prefix A

      # A parameter that defines whether the IDs are scoped within the host or
      # unique across host.
      # Here, we define that the IDs are unique across host, i.e.,
      # we can address an instance 4567 as `/articles/4567` instead of, e.g,
      # `/stores/837/articles/4567`.
      # This is useful if we don't want the users to identify the store of an
      # article from its identifier / URL. 
      uniqueness-scope type

      ordering orderable
    }

    attributes {
      DisplayName: thing.Name
      Images: ordered set {
          cardinality 1..16
        } of media.Image {
        }

      # ...
    }

    # ...
  }

  # A store could have zero to unlimited (?) number of showcases.
  # Showcases are referenceable, e.g., it can be represented by an URL
  #
  # - Showcase or section?
  adjunct entity Showcase {
    id {
      prefix SC
      uniqueness-scope host
    }
  }
  
  # ...
}

# Here we create adjuncts for an entity defined in another module,
# in this case, it's entity User from the iam module.
with iam.User {

  attributes {
    # A cart has one-to-one relationship with a user, and
    # it does not need to be referenceable.
    Chart: value Cart {
      attributes {
        Items: ordered set {

        } of Article
      }
    }

    Lists: ordered set {

    } of entity List {
      attributes {
        Label: thing.Name
        CoverImage: media.Image
      }
    }
  }

}

entity Category {
  id {
    # Slug?
  }
  lifecycle {
    creation {
      #TODO: only admins
      allow if $user in $realm.administrators
    }
    deletion {
      #TODO: only admins
    }
  }

  attributes {
    DisplayText: thing.Name {
      localization enabled
      access {
        read {
          allow all
        }
        deletion {
          allow if $user in $realm.administrators
          event {
          }
        }
      }
    }
    Slug: xxx {
      source DisplayText
    }
    BannerImage: media.Image {
      aspect-ratio 4:1
      oversize crop
    }
    IconImage: media.Image {
      aspect-ratio 1:1
      oversize crop
    }

  }
}

# ...

```

TODO:

- [ ] Store approval
- [ ] Store tier (paying stores get more features)
- [ ] Store id
- [ ] Store lifecycle
- [ ] Store ownership (transfer, transfer rules etc.)
- [ ] Store name constraints (length, how can it be changed)
- [ ] Store icon and banner
- [ ] Article images constraints
- [ ] Article id (not SKU; SKU is an adjunct)
- [ ] Article variations: sizes, colors, optional parts. Also the related images for each variation.
- [ ] Article bundles (an article comprised of other items, e.g., a bike and its wheels)
- [ ] Cart articles
- [ ] Showcase articles
- [ ] Showcase id
- [ ] Order
- [ ] Receipt
- [ ] Review
- [ ] Payment
