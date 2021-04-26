# Marketplace

```
entity Shop {
  id {
    # ...
  }
  
  ownership {
    owner_arity 1
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
    # ...
  }
  
  attributes {
    DisplayName: thing.Name
    
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

