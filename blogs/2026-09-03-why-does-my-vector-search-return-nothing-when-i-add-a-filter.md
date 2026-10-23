---
title: "Why does my vector search return nothing when I add a filter?"
url: "https://surrealdb.com/blog/why-does-my-vector-search-return-nothing-when-i-add-a-filter-2"
date: "2026-09-03"
feed_url: "https://surrealdb.com/feed/blog.rss"
---
A filter applied after an HNSW walk can only remove rows, so a selective one comes back empty. Three measured SurrealDB fixes, plus the schema that avoids them.
