# Mudmap sub-account overview

A rough idea of what this change should achieve.

- `groups` is has a collection of users
- `users` has a relation to `permissions`
- `device` belong to `groups`, not `users`
- Existing `users`'s must be attached to a `groups` (probably by creating a `groups` using the
  `user.Name` field as `group.Name` and adding them as a `users` to that group)
- `groups` owners can update `groups` info
- `permissions` should be a Many-to-Many. `users` can have many `permissions` and the same
  permission can belong to many `users`.
- Auth0 should also be aware of `users` and `groups`
- Auth0 should also be aware of permissions
- Auth0 should place `permissions` within the token (if possible)
- Updates to the `permisions` table must also be reflected in Auth0
- Updates to the `groups` table must be reflected in Auth0 

**Next Steps**

1. Test assumptions with Auth0's Authorization and Group tooling 
2. Create `permissions` and `groups` table
3. Update `users` table to have relation with `groups` 
4. Create change `devices` relation from `users` to `groups`
5. Write sync methods so that the DB and Auth0 remain in sync 
6. Middleware for checking a user can access a device based on JWT token fields

This is a decent sized change with a few moving parts. I can possibly 
remove the Auth0 lock-in but I see no good way of doing this without
forcing a DB lookup for each request (check permission and group). If
I use Auth0 I can hopefully keep it sync'd with the DB and embed that
data in the `app_metadata` field of the token. A assumption I need to 
test fully before too much investment in code.

Related:

- [20220505024039 Mudmap sub-accounts](/20220505024039/)

Tags:

    #mudmap #planning
