# Database Design for Beginners by David Copeland

- [Database Design for Beginners by David Copeland](#database-design-for-beginners-by-david-copeland)
  - [Contact](#contact)
  - [Thought experiment](#thought-experiment)
  - [Notes](#notes)
    - [General](#general)
    - [What is a database?](#what-is-a-database)
    - [What facts do we want to record?](#what-facts-do-we-want-to-record)
    - [How?](#how)
    - [Primary keys](#primary-keys)
    - [Physical vs Logical Model](#physical-vs-logical-model)
      - [Logic to Physical](#logic-to-physical)
      - [On Types](#on-types)
    - [General guidance](#general-guidance)
    - [Closing thoughts](#closing-thoughts)

## Contact

- Dave Copeland
- @davetron5000

## Thought experiment

1. Your app's source code goes away forever with no backup possible
2. Your database goes away forever with no backups

## Notes

### General

- Data > Source Code

### What is a database?

- OLTP: online transaction processing
- An OLTP is the source of truth - it records facts about the world
- Database design is how we ensure our database is the source of truth

### What facts do we want to record?

- A wrestler may have a finishing move
- A wrestler might wrestle on a show
- A wrestler may be cleared to compete on one or more matches of a show
- A show may have a title belt that is defended on a show

- Nouns are keys
- Anomalies: when the data model prevents the storage of certain facts, allows ambiguity to exist, or requires deleting one fact
- Normalization is the process by which we remove anomalies from our design
- Normal forms are mathematical truths about a data model that prove what sorts of anomalies have been removed
- [Boyce-Codd normal form](https://en.wikipedia.org/wiki/Boyce–Codd_normal_form)
  - Meaning our data models have no anomalies based on our functional dependencies
- A relation requires:
  - no duplicate rows
  - each field has a single value
  - fields in the same column are of the same type
- Null is not a value, therefore null us not an allowed value, therefore no field can be null
- [First normal form](https://en.wikipedia.org/wiki/First_normal_form)
- Capture business rules as functional dependencies and keys
- Functional dependency is when the value of a column unambiguously implies the value of another column, based on business rules
- A key is a subset of columns that is uniquely identifies a row
- A relation can have many keys, but always has at least one
- This process is called Heath's theorem, which proves we removed anomalies and didn't loose data

### How?

- What facts do we want to record
- Create relations
- Identify functional dependencies and keys
- Extract new tables/apply Heath's theorem

### Primary keys

- Uniquely identify the row
- They are called natural keys or sometimes business keys
- They are handy because they represent facts and are easily understood
- But what if we rename a show or a wrestler? We have to change the key values everywhere and it is messy
- To get around this Rails makes the ID field, it is called the synthetic/surrogate key

### Physical vs Logical Model

#### Logic to Physical

- The tables ie migrations are the implementation of the design
- Primary concerns
  - enforcing keys
  - enforcing associations
  - enforcing types
- keys can be enforced with unique indexes
- associations can be enforced with foreign key constraints
- Types are harder and potentially impossible to get perfect depending on your database

#### On Types

- Tradeoffs
  - How likely is bad data to be input
  - How bad is it if it happens
- Database constraints
- Postgres trim
- Rails validations
  - `validates :name, presence: true, uniqueness: { case_sensitive: false }`

### General guidance

- Create unique indexes for all business keys
- Use foreign key constraints
- Default to not-null
- Comment nullable fields
- Use database constraints if the downside of bad data is really bad, otherwise validations

### Closing thoughts

- Boyce-Codd Normal form does not eliminate all anomalies, but it eliminates many
- When editing your model, edit your design, then flow through to the physical
- Start with business rules, ie functional dependencies and keys
- Never forget the data is more important than your app in most cases
- Agile Web Development with Rails 6 - `RailsConf2019_rails6`
