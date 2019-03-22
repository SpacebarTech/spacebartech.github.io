# spacebartech.github.io
The JETS Technologies, LLC. company handbook


## TODO: Page Topics

### Code

- [ ] Code Styleguide
  - _"A function should do one thing and one thing only."_
- [ ] How to create a TypeScript library
  - [ ] When to compile TS, etc.
  - [ ] Barrel pattern
- [ ] How to create a TypeScript API
  - [ ] Cloning the template
  - [ ] Docker / Compose
  - [ ] `.env` template
  - [ ] Using Fireabse to handle Auth
  - [ ] Creating services
    - _"Your service defines the roadmap of steps to complete a given task." -- One Smart Boi_
- [ ] Caching data on the frontend with Vuex and IndexDB
- [ ] Making API calls from the frontend
  - [ ] Making branch calls to Firebase and SQL in a single API call
- [ ] Objection
  - [ ] How to relationMappings???
- [ ] Objection models vs. Knex migrations vs. Joi validation
  - why have 3 sources of truth?
- [ ] Gotchas
  - [ ] Jest caching issues
  - [ ] Knex
    - column.string() is the equivalent to `varchar(255)`
    - [Cheatsheet](https://devhints.io/knex)
  - [ ] Using `Promise.all()` in migrations and seeds
    - If not, TS will attempt to use Bluebird's `#then()` instead of native ES6 Promise
      - `(method) Bluebird<any>.then<any>(onFulfill?: (value: any) => any, onReject?: (error: any) => any): Bluebird<any> (+1 overload)`
      - `Property '[Symbol.toStringTag]' is missing in type 'Bluebird<any>' but required in type 'Promise<any[]>'.ts(2741)`
      - Don't use Bluebird if you genuinely don't have to; usually for FilteredCatch and NamedErrors

### Design

- [ ] Figma vs. Sketch/Abstract
- [ ] Embracing the math and science of linear gradients

### Process

- [ ] Forms of communication
- [ ] Contributing docs
- [ ] NodeJS project commands
  - [ ] Using `builder` and `builder-init` by FormidableLabs
  - [ ] List of company `builder` archetypes
    - [ ] Frontend (Vue, etc.)
    - [ ] API (Express, etc.)
    - [ ] Library
    - [ ] Test (API, Library)
    - [ ] Lint (JS)
    - [ ] Lint (TS)
    - [ ] tsc build
    - [ ] barrel
    - [ ] coverage (report, serve)
- [ ] Git-Fu
- [ ] Testing
  - [ ] Service testing
    - all tests should be 100% independent from one another. If you need setup, use `beforeEach` or something
  - [ ] Integration testing
  - [ ] e2e testing
  - [ ] Auth&Auth testing (authentication & authorization)
  - [ ] Configuration
- [ ] Process Styleguide (why we choose to do x or y instead of z)
  - [ ] How we store TZ data in dates with Postgres
  - [ ] table_name.id === working with Firebase
  - [ ] table_name.table_name_key === working with SQL
    - Postgres table names are always plural
- [ ] How to publish to the @jetstech npm scope
  - [ ] `.npmrc` setup
- [ ] How to code review

### Docs

- [ ] Technology used
- [ ] Big data
  - [ ] Datagrip
  - [ ] Grafana
- [ ] Containers
  - [ ] Docker
  - [ ] Compose
  - [ ] K8s
- [ ] Node versioning with NVM
- [ ] Becoming a Trelloist
