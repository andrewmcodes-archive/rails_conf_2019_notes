# Selfish Programmer by Justin Searls

- [Selfish Programmer by Justin Searls](#selfish-programmer-by-justin-searls)
  - [Notes](#notes)
    - [General](#general)
    - [Antisocial](#antisocial)
      - [Ungrateful](#ungrateful)
      - [Ungenerous](#ungenerous)
      - [Delusional](#delusional)
    - [Egotistical](#egotistical)
      - [Narcissistic](#narcissistic)
      - [Domineering](#domineering)
    - [Irresponsible](#irresponsible)
      - [Untethered](#untethered)
      - [Fickle](#fickle)
      - [Unhelpful](#unhelpful)

## Notes

### General

- `whenkani` gem
- Solving parts of the whole problem
- Separating parts into weekend projects
- incremental accomplishment is motivating

### Antisocial

- Applications are like pyramids: top is application code and the rest is the dependencies
- Outsource your gemfile
- Gemfile in two halves: one half is large, well-maintained gems, other is smaller, less maintained projects
- bycrypt + has_secure_password vs devise
- Gem may be easy to install now but may be difficult to deal with later

#### Ungrateful

- soundproof code: code lives with feature and extracted later if needed
- models are mostly dumb value types
- `git rep MyThing | wc -l`
- No feature logic in models

#### Ungenerous

- write a little extra code in order to give the flexibility of changing it aggressively later

#### Delusional

- Sometimes you have to ship code you shouldn't
- If you never create feature branches you never need pull request reviews
- Delusional because they believe code is done when it works
- Delusional because if it doesn't change then it must be right
- AR can talk to SQL views like they are models
- 4x faster by using DB instead of ruby

### Egotistical

#### Narcissistic

- "How an activity will benefit them before they choose to do it"
- Tests create a safety net, and can elp us express our intentions to our teammates
- A(verage).I. Testing
- Looks at only most recent changes to code and only runs unit tests affected by the change
- Mean time to failure vs mean time to repair
- Maximize MttF.max

#### Domineering

- Most software requires clear, narrow vision
- Someone's idea or someone's problem can solve an issue you don't realize you had

### Irresponsible

#### Untethered

- No_Ops - 0 routine operations work
- Minimize dependencies, follow conventions, less servers
- Heroku deploy pipelines and review apps

#### Fickle

- style doesn't matter to ruby
- standard gem wraps rubocop with locked config
- rely on tool to stay focused on tool

#### Unhelpful

- Solve problems once for all instead of solving issue over and over
- later == never
- `gem install todo_or_die`
