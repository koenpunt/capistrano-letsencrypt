# Capistrano::LetsEncrypt [![Gem Version](https://badge.fury.io/rb/capistrano-letsencrypt.png)](http://badge.fury.io/rb/capistrano-letsencrypt)

Let's encrypt support for Capistrano 3.x

Thanks to @unixcharles and @zealot128 for their libraries,
[acme-client](https://github.com/unixcharles/acme-client/) and
[letsencrypt-cli](https://github.com/zealot128/ruby-letsencrypt-cli) for managing
part of the workflow to work with Let's encrypt. This library use both to create
a series of capistrano tasks that should help you create certs on your projects
deployed with capistrano

## Installation

Add this line to your application's Gemfile:

    gem 'capistrano'
    gem 'capistrano-letsencrypt'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install capistrano-letsencrypt

## Usage

Require in `Capfile` to use the default task:

```ruby
require 'capistrano/letsencrypt'
```

You will get the following tasks

```
cap letsencrypt:register            # Register a Let's encrypt account
cap letsencrypt:check_certificate   # Check for validity of certificates
cap letsencrypt:authorize           # Authorize a domain using ACME protocol
cap letsencrypt:cert                # Create certificates and private keys
```

Configurable options (copy into deploy.rb), shown here with examples:

```ruby
# Set the roles where the let's encrypt process should be started
# Be sure at least one server has primary: true
# default value: :web
set :letsencrypt_roles, :letsencrypt

# Optionally set the user to use when installing on the remote system
# default value: nil
set :letsencrypt_user, nil

# Set it to true to use let's encrypt staging servers
# default value: false
set :letsencrypt_test, true

# Set your let's encrypt account email (required)
# The account will be created if no private key match
# default value: nil
set :letsencrypt_email, nil

# Set the path to your let's encrypt account private key
# default value: "#{fetch(:letsencrypt_email)}.account_key.pem"
set :letsencrypt_account_key, "#{fetch(:letsencrypt_email)}.account_key.pem"

# Set the domains you want to register (required)
# This must be a string of one or more domains separated a space - e.g. "example.com example2.com"
# default value: nil
set :letsencrypt_domains, nil

# Set the path from where you are serving your static assets
# default value: "#{release_path}/public"
set :letsencrypt_challenge_public_path, "#{release_path}/public"

# Set the path where the new certs are going to be saved
# default value: "#{shared_path}/ssl/certs"
set :letsencrypt_output_path, "#{shared_path}/ssl/certs"

# Set the local path where the certs will be saved
# default value: "~/certs"
set :letsencrypt_local_output_path, "~/certs"

# Set the minimum time that the cert should be valid
# default value: 30
set :letsencrypt_days_valid, 15
```

## Requirements

This tool needs Ruby >= 2.1 (as the dependency acme-client needs that because of use of keyword arguments).

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## Credits

Thank you [contributors](https://github.com/platanus/capistrano-letsencrypt/graphs/contributors)!

<img src="http://platan.us/gravatar_with_text.png" alt="Platanus" width="250"/>

capistrano-letsencrypt is maintained by [platanus](http://platan.us).

## License

Guides is © 2014 platanus, spa. It is free software and may be redistributed under the terms specified in the LICENSE file.
