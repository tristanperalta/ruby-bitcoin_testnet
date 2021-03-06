# BitcoinTestnet

Makes development with Bitcoin a little easier. It has helpers that can be used to start, stop, clean the testnet.

## Usage

First, require the library in your  `test_helper`/`spec_helper`:

    require 'bitcoin_testnet'

Now, you have access to `BitcoinTestnet`.

Second, you have to tell BitcoinTestnet where the testnet in a box directory is. I prefer to keep it in the test folder of my project. For example, with RSpec:

    git submodule add https://github.com/freewil/bitcoin-testnet-box spec/testnet

See the readme of `bitcoin-testnet-box` to see what version of `bitcoind` to install. The test net you download is configured with a certain version of the bitcoin daemon.

Then, in your `test_helper`/`spec_helper`:

    BitcoinTestnet.dir = "spec/testnet"

Third, tell `BitcoinTestnet` when to do its work:

- Before each spec, call `BitcoinTestnet.start`. This will start and clean the Testnet, so it looks like it did the first time you started the Testnet.
- After the test suite is finished, call `BitcoinTestnet.stop`. This turns off the Testnet.

Sample with RSpec:

    RSpec.configure do |config|
      config.before(:each) { BitcoinTestnet.start }
      config.after(:suite) { BitcoinTestnet.stop }
    end


### RSpec and VCR

Cleaning the Testnet every time is slow. If you have VCR, you can make this a lot faster by calling `BitcoinTestnet.configure_with_rspec_and_vcr!` in your spec helper. With this, you won't need to call `BitcoinTestnet#start` and `BitcoinTestnet#stop`.

## Installation

Add this line to your application's Gemfile:

    gem 'bitcoin_testnet'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install bitcoin_testnet

## Tip

To make integration tests faster, use something like [VCR](https://github.com/vcr/vcr) to record the communication between your project and the Testnet.

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
