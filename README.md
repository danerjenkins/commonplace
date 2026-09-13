# Commonplace

A three-screen product prototype for a personal reading app — *your entire reading life, organized around you*.

This is a proof-of-concept, not a production app: no auth, no backend, no real recommendation engine. Interactions and personal data (statuses, ratings, reviews) are mocked or held in memory for the session so the core product idea can be clicked through and user-tested.

## Screens

1. **Library Home** — every book you own, borrow, want, or are reading, grouped into shelves.
2. **Book Detail** — a book's general info alongside your personal relationship to it (status, rating, review).
3. **For You** — a single, reasoned recommendation delivered like a note from someone who knows your taste, with a simulated "thinking" state instead of a real AI backend.

Book data and cover art are sourced from a real personal library (Supabase), with a few additional real covers pulled in for recommended titles not yet in the library.

## Running locally

This is a static, dependency-free single HTML file — no build step.

```
python -m http.server 8000
```

Then open `http://localhost:8000`.
