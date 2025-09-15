On UPDATE / DELETE Postgres does NOT overwrite.
Instead it creates a new version and marks the old version as obsolete.

Effect:
1. Wasted Disk Space
2. Slower Queries
3. Bloating Indexes

Vacuuming is the process of cleaning up these dead tuples.