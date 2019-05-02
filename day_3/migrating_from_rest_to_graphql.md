# New HotN+1ness - Hard lessons migrating from REST to GraphQL by Eric Allen

- [New HotN+1ness - Hard lessons migrating from REST to GraphQL by Eric Allen](#new-hotn1ness---hard-lessons-migrating-from-rest-to-graphql-by-eric-allen)
  - [Notes](#notes)
    - [General](#general)
    - [Eager Loading](#eager-loading)
    - [Delegation](#delegation)
    - [Retro](#retro)
      - [Gained](#gained)
      - [Lost](#lost)
    - [How can we approach our decisions differently?](#how-can-we-approach-our-decisions-differently)
  - [Questions](#questions)

## Notes

### General

- `gem graphql`
- [graphql site](https://graphql.org)
- Rest has serializers, GraphQL has types
- Serializers we define attributes and relationships, Type objects have fields

### Eager Loading

- Eager loading not respected same way in GraphQL vs REST
- Eager loading in GraphQL is an antipattern because you will be loading a lot more data than you need
- `gem 'graphql-batch'` to batch queries

### Delegation

- Record loader object returns promise, then call `.then` to batch queries together

### Retro

#### Gained

- Flexibility
- Less changes to the API
- Free documentation
- New dependencies - `graphql` & `graphql-batch`

#### Lost

- Confidence
- HTTP response codes - GraphQL always responds with 200 and error key in the object
- Granularity in performance monitoring
- Feature work

### How can we approach our decisions differently?

- "Thinking in bets" by Annie Duke
- Remove opinions that are presented as facts
- Say "I don't know" or "I'm not sure" more often
- Embrace uncertainty
- Focus on the process
- Remove bias based on the desire to learn a new tool
- Embrace mistakes - hold each other accountable

## Questions

- Would you do it again?
  - Best to use with multiple clients
  - Good developer tools
  - Would do it again
- Is the API in the same codebase?
  - API is in the same codebase
- Authorization?
  - GraphQL gem has support for pundit
- How to deal with errors?
  - Failovers - interactor pattern
  - Handle on the frontend if error key is in the GraphQL object
- Mutational queries - not just reading data, but writing data
  - Use interactor pattern
  - Call action from GraphQL instead of controller
- GraphQL Pro?
  - No, but it has been considered
