# OcxClient

OcxClient是用Ruby语言编写的OCX API客户端

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'ocx_client'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install ocx_client

## Usage

### REST API client ###

Use `#get` or `#post` to access API after you created a `OcxClient::RestApi`:

```ruby
  require 'ocx_client'

  # Client can be initialized not providing key and sercet, but this client can only access public APIs
  client_public = OcxClient::RestApi.new endpoint: 'https://api.ocx.com'

  # GET public api /api/v2/markets
  client_public.get_public '/api/v2/markets'

  # To build a full functional client which can access both public/private api, access_key/secret_key
  # are required.
  #
  # `endpoint` can be ignored or set.
  #
  # If there's no data received in `timeout` seconds, Net::OpenTimeout will be raised. Default to 60.
  #
  client = OcxClient::RestApi.new access_key: 'your_access_key', secret_key: 'your_secret_key', endpoint: 'https://api.ocx.com', timeout: 60

  # GET private api /api/v2/orders with 'market=btcusdt'
  client.get '/api/v2/orders', market: 'btcusdt'

  # POST to create an order
  client.post '/api/v2/orders', market: 'btcusdt', side: 'sell', volume: '0.11', price: '8000.0'

  # POST to create multiple orders at once
  client.post '/api/v2/orders/multi', market: 'btcusdt', orders: [{side: 'buy', volume: '0.15', price: '8000.0'}, {side: 'sell', volume: '0.16', price: '8001'}]
```

## Development

After checking out the repo, run `bin/setup` to install dependencies. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/[USERNAME]/ocx_client. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.


## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

