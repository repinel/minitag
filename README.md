[![Gem Version](https://badge.fury.io/rb/minitag.svg)](https://badge.fury.io/rb/minitag) [![](https://github.com/bernardoamc/minitag/workflows/continuous-integration/badge.svg)](https://github.com/bernardoamc/minitag/actions?query=workflow%3Acontinuous-integration)

# Minitag

A simple gem that allow developers using minitest to specify tags for their classes and tests, and run their test suite based on these tags.

This gem should be framework agnostic, let me know if you encounter any problems
running this within the framework of your choice.

## When should I use this?

- When there's a need to split a test suite into different CI steps.
- During development, it's helpful to have extra flexibility when running a big
  test suite.
- When there are tests that you want to run only occasionality. For example,
  tests that perform network calls or have expensive side effects.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'minitag'
```

Or install it yourself as:

```
$ gem install minitag
```

## Usage

### Setup

Require `minitag` within `test_helper.rb`:

`require 'minitag'`

### Adding tags

We can tag specific classes or tests with one or more tags.

It is important to point out that tags associated with a class or test have no concept of being inclusive or exclusive. This distinction is only valid for [tag filters](#running-tests-with-tag-filters).

```rb
class MyTest < Minitest::Test
  # Every test within this class will inherit this tag
  tag_namespace 'my_namespace_tag'

  # Only the test below will have this tag
  tag 'my_tag', 'another_tag'
  def test_hello_minitest
    # ...
  end
end
```

### Running tests with tag filters

We can now run our test suite with specific tags:

`$ bundle exec rake test --tag 'unit'`

or even multiple tags:

`$ bundle exec rake test --tag 'unit' --tag 'services' --tag '~model'`

### More on tag filters

Tag filters can be:
  1. `inclusive`
  2. `exclusive` with the `~` prefix:

### Examples
```rb
# Only run tests that are tagged with 'unit'
$ bundle exec rake test --tag 'unit'

# Only run tests that are NOT tagged with 'unit'
$ bundle exec rake test --tag '~unit'

# Only run tests that are tagged with 'unit' and are NOT 'parallel'
$ bundle exec rake test --tag 'unit' --tag '~parallel'
```

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake test` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/bernardoamc/minitag. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).

## Code of Conduct

Everyone interacting in the Minitag project’s codebases, issue trackers, chat rooms and mailing lists is expected to follow the [code of conduct](https://github.com/bernardoamc/minitag/blob/master/CODE_OF_CONDUCT.md).
