---
layout: default
title: Gotchas
category: engineering
permalink: "/engineering/gotchas"
---

# {{ page.title }}

## `knex.whereBetween`

Using `whereBetween` can sometimes be tricky. If you find
yourself getting back an empty response when you should be
getting back at least one row, make sure that your `after`
date comes before your `before` date, like so:

```js
Model.query()
  .whereBetween( 'created_at', ['after_date', 'before_date'] );
```

However, in a SQL query builder, the following is valid:

```sql
select * from public.users
where public.users.last_login
between '2019-04-09' and '2019-04-12';
-- notice the earlier date comes before the later date
-- earlier = after; later = before.
```

## Add a row to a pivot table

When using Objection for a `ManyToManyRelationship`, it's
important to note that a couple things have to happen. If
you need to relate two entities as a row of a pivot table,
follow the example below:

```ts
class MyService extends MyRepo {
  // Make a `create` function for inserting into the db.
  // Assume `Entity` is some Objection Model, and
  // `otherEntity` is a table in the database.
  static create: (entity: Partial<Entity>) => Bluebird<Partial<Entity>> =
    Bluebird.method(async (entity: Partial<Entity>) => {
      // Get the Model's Knex instance for the transaction
      const knex: Knex = Entity.knex();

      // Begin a transaction, passing in `knex`.
      return objection.transaction(knex, async(trx: objection.Transaction) => {
        // Destructure the `pk`, separating the pk to
        // relate from the rest of the object (as there's
        // no column on the `entities` table for that pk;
        // rather, it's on the pivot table). This assumes
        // that the left table has a row `where id =
        // 'otherEntityId'`
        const { otherEntityId, ...ent } = entity;

        // Firstly, insert the `entity` into the db. We use
        // `insertGraph` here to insert any other relations.
        const insertedEntity = await Entity.query()
          .insertGraph(ent, { relate: true });

        // Once we've inserted it, we want to start a
        // related query, joining the two tables together.
        // `#relate()` is what actually inserts the row
        // into the pivot table, using the supplied
        // `otherEntityId` and the `entityId` from the
        // `insertedEntity`.
        insertedEntity.$relatedQuery('otherEntity', trx).relate(otherEntityId);

        return insertedEntity;
      })
    });
}
```

If you want to return the entire relation, you can chain
`.eager('[...]')` to the end of the `return` statement.

Note the `$` in front of `relatedQuery`. Do not call
`relatedQuery` on the `Model` itself. You _must_ call it on
the instance.

## DigitalOcean deployments

### Caching issues

At some point, Tim is going to ask you to push to
production. You may find that the production server either
serves an outdated version, or caches some pages, but not
all, when using Chrome. To fix this, simply open up the dev
tools, head to the `Network` tab, and check the box labeled
`Disable cache`. Leave this open while you navigate the
site.

If that still doesn't solve the issue, it's most likely
because of service worker caching. There are two ways to
reset the cache.

1. Open the current window in a browser that has never
   visited that link.

2. Bump the version number in the application's
   `manifest.json` (this is the preferred way).
