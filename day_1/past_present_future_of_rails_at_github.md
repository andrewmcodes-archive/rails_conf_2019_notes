# The Past, Present, and Future of Rails at GitHub by Eileen Uchitelle

- [The Past, Present, and Future of Rails at GitHub by Eileen Uchitelle](#the-past-present-and-future-of-rails-at-github-by-eileen-uchitelle)
  - [Slides](#slides)
  - [Notes](#notes)
    - [General](#general)
    - [GitHub's Issues](#githubs-issues)
    - [Costs for you](#costs-for-you)
    - [When upgrading you should...](#when-upgrading-you-should)
    - [Regrets](#regrets)
    - [Things to remember](#things-to-remember)
    - [Benefits](#benefits)
    - [Future for GitHub](#future-for-github)
    - [Multiple Rails Versions](#multiple-rails-versions)
      - [Gemfile](#gemfile)
      - [Features](#features)

## Slides

https://speakerdeck.com/eileencodes/railsconf-2019-the-past-present-and-future-of-rails-at-github

## Notes

### General

- Rails is born in 2004
- "Frameworks are extracted, not built" -DHH
- Rails 1.0 in 2005
- GitHub is born 2007
- Github launches in 2008
- Rails 2.3 in 2009
- Github forked Rails between 2009 and 2010
  - Had different features than Rails
- Rails 3.0 in 2010
  - Large performance hits
  - ActiveRecord was 5x slower than Rails 2
- GitHub started 3.0 upgrade in 2011 based on their own fork
- Rails 3.2 in 2012 fixed lots of performance issues and GitHub upgrade had stalled
- GitHub upgrade 3.0 in 2014 still on custom fork
- GitHub started migrating to 4.0 and Rails 5.0 was released in 2016
- Eileen started in 2017
- 4.2 in prod 2018
- 5.2 in prod 6 months later
  - First time in 10 years not on a fork
  - First time up to date with Rails master
- Cost of not upgrading is immeasurable and will cost more money because of tech debt
- Key to upgrading is incrementally shave off technical debt

### GitHub's Issues

- Hiring issues
- Security backports
- Dependencies were brittle
- Development was painful

### Costs for you

- Have to manually update security backports
- You loose out on new talent from college and bootcamps
- Have to fork gems and now you have even more tech debt
- Have to build more infrastructure to support your old app
- Minor changes can lead to major refactoring
- Biggest cost is that someday you will realize Rails is a mistake (and rewrite in microservices)

### When upgrading you should...

- Build a team for the upgrade
- Consider hiring a contractor for a small team
- Take time to plan your upgrade
- Two branches vs dual-bootable CI
- Fix deprecation warnings early
- Invest in tooling

### Regrets

- You may regret forking Rails
  - Single most expensive decision for GitHub
- Falling behind security supported versions
- Using old, unsupported gems
  - Upgrade dependencies often
- Using Rails private APIs
  - No deprecations for using private APIs

### Things to remember

- Pay down debt down incrementally
- Remove monkey patches
- Remember that you are not alone
  - Find others for support (Like GitHub asking Shopify)
- Upgrades are worth it

### Benefits

- Improved APIs
- Improves security
  - Rails adds new security features, Rails 6 has improved AREL security
- Better performance
- New libraries
  - ActionText, ActionMailbox, Zeitwerk
- Keep line between your app ends and framework begins
- Chance to contribute upstream
  - Difficult to fix bugs when you are on an old version

### Future for GitHub

- GitHub can now contribute features upstream to Rails
- 75+ PR's from GitHub to Rails 6
- Extract features to reduce complexities in the application like multiple DB's
- Continuous upgrades and makes future upgrades easier
- GitHub can now help pioneer the future of Rails
- Helps keep app focused on product
- Have responsibility to support Rails

### Multiple Rails Versions

#### Gemfile

```ruby
# Gemfile.lock (Rails 3.2)
rails server
rails test tests/models/issue_test

# Gemfile_rails4.lock
RAILS4=1 rails server
RAILS4=1 rails test tests/models/issue_test
```

#### Features

```ruby
if GitHub.rails_3_2?
  ....
else
  ....
```
