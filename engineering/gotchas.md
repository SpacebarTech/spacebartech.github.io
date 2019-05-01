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

```ts
Model.query()
  .whereBetween( columnName, [after, before] );
```

However, in a SQL query builder, the following is valid:

```sql
select * from public.users
where public.users.last_login
between '2019-04-09' and '2019-04-12';
-- notice the earlier date comes before the later date
-- earlier = after; later = before.
```

## DigitalOcean deployments

### Caching issues

At some point, Tim is going to ask you to push to
production. You may find that the production server either
serves an outdated version, or caches some pages, but not
all, when using Chrome. To fix this, simply open up the dev
tools, head to the `Network` tab, and check the box labeled
`Disable cache`. Leave this open while you navigate the
site.
