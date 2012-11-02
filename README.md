# ActiveResource::Server
Adds [ActiveResource](https://github.com/rails/activeresource) compatible endpoints to Rails models. 

### Motivation:
Say you're working in a [Service Oriented Architecture](http://en.wikipedia.org/wiki/Service-oriented_architecture), and you need easy access to a few central models in another app. 
#### [ActiveResource](https://github.com/rails/activeresource) to the Rescue!
```
# In Your App  
# Setup the Resource
class User < ActiveResource::Base
  self.site = "http://account-management-service.com/ares"
end

# Find
tyler = User.find(1)

# Create
tyler = User.new(:first => 'Tyler')
tyler.new?  # => true
tyler.save  # => true
tyler.new?  # => false
tyler.id    # => 2

# Update
tyler = User.find(1)
tyler.first # => 'Tyler'
tyler.first = 'Tyson'
tyler.save  # => true

# Delete
tyler = User.find(1)
tyler.destroy  # => true
tyler.exists?  # => false
User.delete(2)  # => true
User.exists?(2) # => false
```

#### But...
ActiveResource falls flat unless the other app implemented the required REST interface.  ActiveResource compatibility means:
* tons of boilerplate code  
* creating controllers for each model  
* the risk of regressions as development continues on these controllers    


#### Solution
``ActiveResource::Server`` dynamically adds RESTful, namespaced endpoints for your Rails' models.  
Simply add the gem to an application, and for only 3 easy payments of $29.95 it is ready for ActiveResource integration.  
New models are included automatically.  WOW!!!  


## Installation

Add this line to your application's Gemfile:

    gem 'activeresource-server'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install activeresource-server

## Usage

### Security
I **HIGHLY** recommend restricting access to this service (otherwise consider publishing your MySQL credentials).    
That said, authentication is mostly outside the scope of this gem.  I have included a small HTTP Basic Auth option, but you may want to use Devise/Sorcery/Authlogic/etc.
  

### Configuration
**namespace**(default:'activeresource'): the base of the path (domain.com/:namespace/:resource/:id)  
**skip_models**(default:false): An array of models to skip when serving up resources  
**http_auth**(default:false): An ['username', 'password'] array. Off by default.  

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

<hr />
