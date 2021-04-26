# Marketplace

```
entity Shop {
  id {
    prefix MSh

    # ...
  }
  
  ownership {
    transfer enabled {
      #TODO: rules. does it need verification?
    }

    owner_arity 1..2
  }
  
  attributes {
    DisplayName: thing.Name {
      #TODO: rules like how frequent the name can be changed, the length constraints, who can change the name, etc.
    }
    
    # ...
  }
  
  # ...
}

# - A shop could have more than one managers but no more than three managers (TODO)
# - A user could manage more than one shops
adjunct Manager {
  hosts {
    Shop
    iam.User
  }
  
  # ...
}

adjunct entity Article {
  hosts {
    Shop
  }
  
  id {
    prefix MAr

    # ...
  }
  
  attributes {
    DisplayName: thing.Name
    Images: set {
        #TODO: constraints for the 'set', e.g., min max
      } of media.Image {
        #TODO: constraints for the 'media.Image', e.g., max size in bytes
      }
    
    # ...
  }
  
  # ...
}

# - Showcase or section?
adjunct entity Showcase {
  hosts {
    Shop
  }
  
  id {
    # ...
  }
  
  #TODO: articles
  
  # ...
}

adjunct Cart {
  hosts {
    iam.User
  }
  
  #TODO: items
  
  # ...
}

# ...

```

