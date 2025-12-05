---
date: '2025-12-05T06:31:34+01:00'
draft: false
title: 'Supabase Architecture'
---   

### Single Supabase Project with Future Separation Path

For the initial development of personal Moneypenny, CTL Moneypenny, and Cletho, we will use a single Supabase project to simplify operations and control costs. To preserve future flexibility, each application will be architected as a self-contained module within that shared project.

This design includes:

* A dedicated Postgres schema for each app
* Isolated storage buckets or folders
* Separate Postgres roles and RLS policies
* Migrations grouped or prefixed by application
* No cross-schema dependencies

By enforcing these boundaries from the outset, each app can be cleanly extracted into its own Supabase project later with minimal friction—primarily a matter of exporting its schema, data, storage assets, and configuration. This approach balances near-term simplicity with long-term architectural optionality.

