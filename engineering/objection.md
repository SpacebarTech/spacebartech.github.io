---
layout: default
title: ObjectionJS
category: engineering
permalink: "/engineering/objectionjs"
---

# {{ page.title }}

> A SQL-friendly ORM for Node.js
>
> See the [docs](https://vincit.github.io/objection.js/)

For a very long time, we used [Firebase](https://firebase.google.com/)
for our database needs. Whether we had NoSQL needs, or
relational needs, this was our go-to. Now, the common
pitfall across the board, of course, is the potential for
duplicate data when using a BSON-schema as an ORM. There
were many ways around this, but we learned very quickly
that the most effective route was to use SQL instead.

> _"Why are we still here? Just to suffer? Every night I
> feel my leg, my arm, even my fingers: the body I've lost;
> the comrades I've lost. Won't stop hurting. It's like
> they're all still there. You feel it, too, don't you?"_

Initially, we learned about the glorified [knex](https://github.com/tgriesser/knex)
by [tgriesser](https://github.com/tgriesser). This allowed
us to automate migrations, seeds, and simply keep working
in JS-land instead of writing hard-coded SQL. This, however,
was not an excuse to not learn SQL and we had a blast
learning about just how powerful it really was when it came
to relational data.

## The problem

While Knex satisfied all our "batteries-included" needs, we
noticed that several things were lacking. We had no way of
keeping track of table references in the form of `Models`,
and making relations was quite an arduous task. We
initially looked into Bookshelf, but a fellow developer can
[tell you all about why that's a bad idea](https://bramanti.me/bookshelf-is-dead/).

> Press "F" to pay respeccs

## The solution

That same developer introduced ObjectionJS to the team,
allowing us to define models around the database tables,
and define their relationships to one another. This also
greatly simplified the process of joins through the
powerful [eager methods](https://vincit.github.io/objection.js/api/query-builder/eager-methods.html#eager-methods).

We've since incorporated ObjectionJS into our newer
projects, leaving behind the Old and setting the stage for
the New.
