# KARA cloud connection setup

KARA POS and Kitchen Display need a shared online database so separate devices see the same orders. The selected backend is Supabase (hosted PostgreSQL + Realtime + staff authentication).

## What is prepared in this repository
- `supabase/schema.sql`: database tables, order statuses, indexes, staff-only Row Level Security policies, and Realtime publication setup.
- `supabase/config.example.js`: safe placeholder for the public project URL and anon key. Never put a service-role key in browser code.

## One-time setup
1. Create a Supabase project at https://supabase.com/dashboard.
2. Choose a project region close to Oman / the Gulf if available.
3. Open SQL Editor in the new project, paste all of `supabase/schema.sql`, and run it.
4. Open Project Settings -> API. Copy the Project URL and the anon/public key.
5. Copy `supabase/config.example.js` to `supabase/config.js` and fill in those two public values.
6. In Authentication -> Users, create staff login accounts for the cashier and kitchen. Use separate accounts and keep passwords private.
7. Do not publish or commit private passwords, database passwords, or the service-role key.

## Important status
This repository now contains the database blueprint and setup guide. The current POS/KDS pages are still demo prototypes using browser local storage; they are not yet connected to Supabase. Do not use the prototype to process real customer payments or production orders.

## Next development step
Update POS and KDS to load the Supabase client, require staff sign-in, write/read orders from the cloud, and subscribe to Realtime order changes. Then test with two separate devices before live operation.

## Security note
The SQL policies restrict staff operations to authenticated Supabase users. Customer online checkout should later be implemented through a trusted server/Edge Function with server-side validation, not by exposing privileged database keys in the public website.
