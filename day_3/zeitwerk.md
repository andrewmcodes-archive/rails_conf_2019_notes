# Zeitwerk: A new code loader by Xavier Noria

- [Zeitwerk: A new code loader by Xavier Noria](#zeitwerk-a-new-code-loader-by-xavier-noria)
  - [Notes](#notes)
    - [Introduction](#introduction)
    - [Basic Usage](#basic-usage)
    - [Motivation](#motivation)
      - [Brittle requires](#brittle-requires)
    - [Constants refresher](#constants-refresher)
    - [How does Rails autoload](#how-does-rails-autoload)
    - [Technical difficulties](#technical-difficulties)
    - [Integration in Rails 6](#integration-in-rails-6)

## Notes

### Introduction

- What is zeitwerk?
  - Autoloading
  - Eager loading
  - Reloading
- no dependencies
- For any Ruby project

### Basic Usage

- File names -> Constant paths
- Top level:

  ```rb
  user.rb -> User
  user_profile.rb -> UserProfile
  html_parser -> HtmlParser
  ```

- Explicit namespaces

  ```rb
  hotel.rb -> Hotel
  hotel/pricing.rb -> Hotel::Pricing
  ```

- Implicit namespaces

  ```rb
  admin/role.rb -> Admin::Role
  ```

- Usage

  ```rb
  # usual
  loader = Zeritwek::Loader.new
  loader.push_dir(..)
  loader.setup

  # gems
  loader = Zeitwerk::Loader.for_gem
  loader.setup

  # eager loading
  loader.eager_load

  Zeitwerk::Loader.eager_load_all
  ```

- Zeitwerk keeps a registry of all the loaders that have been registered
- Normal gems go not need reloading, will use autoloading or eager loading

  ```rb
  loader.enable_reloading
  loader.setup
  ...
  loader.reload
  ```

### Motivation

- Writing requires manually is brittle
- DRYness
- Improve Rails autoloading

#### Brittle requires

  ```rb
    class Airplane
      include Locatable
    end

    # => NameError: uninitialized constant Locatable
  ```

  ```rb
    include "locatable"

    class Airplane
      include Locatable
    end

    # => Require is global
  ```

### Constants refresher

  ```rb
  # constant assignment - storing instance object
  X = 1

  # constant assignment - storing class object
  class C
  end

  # same as:
  C = Class.new

  # constant - evaluates to class object - returns User instance
  user = User.new

  # same deal
  today = Date.today
  ```

- Constants belong to modules
- Lexical nesting?

```rb
# Hotel is object that has a class object inside that is stored in the Hotel constant
class Hotel
  # module object
  module Pricing
    # Nesting is [Hotel::Pricing, Hotel]
  end
end

# Alternative - class must already be declared
module Hotel::Pricing
  # Nesting is [Hotel::Pricing]
end
```

- Resolution of relative constants (`ERB`)
  - Check nesting outwards
  - Check ancestors upwards
  - Check Object if in a module
  - `const_missing` <- callback
- Resolution of qualified constants (`Rack::Request`)
  - Check ancestors upwards, skips Object since 2.5
  - const_missing

### How does Rails autoload

- Idea: autoload paths and `const_missing`
- Limitations of the classic Rails technique
  - The nesting is unknown
  - Relative/qualified is unknown
  - `const_missing` is the last step
  - Not thread-safe
- ActiveSupport does not have the information to resolve constants like Ruby does

  ```rb
  # hotel.rb
  class Hotel
    include Pricing
  end

  # hotel/pricing.rb
  module Hotel::Pricing
  end

  # pricing.rb
  module Pricing
  end
  ```

- Won't return `const_missing` because it will find a constant called pricing

```rb
module ActiveRecord
  autoload :Base, "active_record/base"
end
```

- Idea: autoload paths and `Module#autoload`

### Technical difficulties

- Module#autoload uses require internally
- There is no API to remove autoloads
- Does not support namespaces
- Chicken-and-egg problem in explicit namespaces

- How does require know if it already loaded user?
  - uses global collection

  ```rb
  require "user" # => true
  require "user" # => false
  ```

  ```rb
  require "user" # => true
  $LOADED_FEATURES.pop
  require "user" # => false
  ```

  ```rb
  Object.autoload(
    :Admin,
    "/Users/.../app/controllers/admin"
  )
  ```

  - Thin wrapper around require and intercepts it

### Integration in Rails 6

- enabled by default
- can remove all `require_dependency`
- `config/initializers/inflections.rb` -> may need to tweak inflector
- `bin/rails zeitwerk:check`
- Not in rc1 but will be in final release

  ```rb
  # config/application.rb

  config.add_autoload_paths_load_path = false
  ```

- opt out if you want
