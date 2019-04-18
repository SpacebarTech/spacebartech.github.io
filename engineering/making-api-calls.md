---
layout: default
title: Making API Calls
category: engineering
permalink: "/engineering/making-api-calls"
---

# {{ page.title }}

## Anatomy of an API call

Every API call will have a cookie, called `Auth-Token`,
which cannot be an empty string. We use this on the backend
to determine the user who made the API request. From there,
the API will attempt to authenticate the request. If the
authenticate request fails, so will the whole request, and
all subsequent service method calls will be skipped.
Otherwise, the requesting user is retrieved from Firestore
and placed on `res.locals.caller`.

<small>
  Note: A user object may vary on a per-project basis, so
  be sure to take a look at the project documentation to
  determine what to expect in the object.
</small>

Once a token has been authenticated, it will pass onto
Authorization—_does the requesting user have permission to
perform this specific action?_ You can retrieve a user's
permissions (if the project permits per-route authorization)
via `res.locals.caller`.

Once a user request has been both authenticated and
authorized, the controller will then proceed to the Service
method for that route controller. **If you are creating an
entity in the database that requires a** `createdBy`
**field, retrieve the currently auth&auth'd user via**
`res.locals.caller` **and do not pass any additional
parameters that may pertain to the user making the requst.**
If you need to relate two database entities using Objection,
simply add the following key-value to the entity you're
attempting to create:

```js
// Creating a User example

const { usersKey } = res.locals.caller;

// Using the `createdBy` property
{
  createdBy : usersKey,
}

// Or using the `creator` object
{
  creator : {
    usersKey
  }
}
```
