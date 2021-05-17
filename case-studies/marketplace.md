# Marketplace

```
domain marketplace

entity Shop {
  id {
    prefix MSh
  }
  
  lifecycle {
    creation {
    }
  }

  # - A shop ownership could be transferred
  # - A shop has at least one owner but no more than two owners
  ownership {
    transfer enabled {
    }

    owner_cardinality 1..2
  }
  
  attributes {
    DisplayName: thing.Name
    
    # ...
  }

  # - A shop could have more than one managers but no more than three managers
  # - A user could manage more than one shops
  adjunct Manager {
    hosts {
      iam.User {
        cardinality to Shop 1..3
      }
    }

    # ...
  }

  adjunct entity Article {
    id {
      prefix MSA
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

  # A shop could have zero to unlimited (?) number of showcases.
  # Showcases are referenceable, e.g., it can be represented by an URL
  #
  # - Showcase or section?
  adjunct entity Showcase {
    id {
    }
  }
  
  # ...
}

# Here we create adjuncts for an entity defined in another module,
# in this case, it's entity User from the iam module.
with iam.User {

  # A cart has one-to-one relationship with a user, and
  # it does not need to be referenceable.
  adjunct Cart {
  }

}

# ...

```

TODO:

- [ ] Shop approval
- [ ] Shop tier (paying shops get more features)
- [ ] Shop id
- [ ] Shop lifecycle
- [ ] Shop ownership (transfer, transfer rules etc.)
- [ ] Shop name constraints (length, how can it be changed)
- [ ] Shop icon and banner
- [ ] Article images constraints
- [ ] Article id
- [ ] Article variations: sizes, colors, bundles, optional parts. Also the related images for each variation.
- [ ] Cart articles
- [ ] Showcase articles
- [ ] Showcase id
- [ ] Order
- [ ] Receipt
- [ ] Review
- [ ] Payment
