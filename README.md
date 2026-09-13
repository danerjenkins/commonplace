# Commonplace

A three-screen prototype for a personal reading app — *your entire reading life, organized around you*. Proof-of-concept only: no auth, no backend, no real recommendation engine. Data and interactions are mocked/in-memory.

**Live prototype:** https://commonplace-ten-iota.vercel.app

> AI-drafted per Step 7; predictions and first-read below should get a human pass before submission.

## 1. Need, persona, capability, value

| | |
|---|---|
| **Need** | Active readers struggle to keep the books they own, borrow, want, and read organized in one place that reflects how they actually manage their reading life. |
| **Persona** | Avid readers who read regularly, maintain a growing TBR, and get books from a mix of physical purchases, ebooks, and libraries. |
| **Capability** | Build and manage one personal library containing every book they own, want, borrow, or read. |
| **Value** | **Control** — organized around the reader's own habits, not scattered across shelves, apps, and lists. |

## 2. The three screens

| Screen | Job | Why it earned a slot | Design question |
|---|---|---|---|
| **Library Home** | One organized, personalized home for the whole reading life. | Clearest demo of the core value — a personal home, not a book database. | Can a user tell within seconds this is *their* whole reading life, personalized? |
| **Book Detail** | General book info + the reader's personal relationship to it. | Shows the gap between looking a book up and making it part of a personal system. | Does the reader see this as personally managed, not a generic entry? |
| **For You** | One thoughtful recommendation, not a wall of covers. | Shows the payoff of one unified library: taste-aware, human-feeling suggestions. | Does the reader feel *why* understood, not just genre-matched? |

Book/cover data on Home and Book Detail comes from a real Supabase library (real TBR flag, ownership, finished status). The recommendation and its two secondary picks aren't in that library yet by design; their covers come from Open Library.

## 3. Feedback question plan

Questions + predictions only — no findings yet.

- **Need:** *"Tell me about the last time you wanted to start a book but couldn't remember what you already owned or had on hold. What did you do?"* — Predict: re-bought/re-borrowed something they had, or gave up after checking 2-3 apps. Tests whether the Borrowed/Owned/Want-to-Buy shelves sharing one screen actually addresses that.
- **Value:** *"If everything you own, borrow, and want to read lived in one place, what one or two words describe that feeling? Why?"* — Predict: "control" or "relief." Tests whether the landing screen and Book Detail's personal-status card deliver that, not just a nicer catalog.
- **Persona:** *"Where does your want-to-read list actually live right now?"* — Predict: a fragmented spot (Notes app, Goodreads, memory). Tests whether the real-data "Up Next" shelf feels like a real upgrade.
- **Capability:** *"Five-second look at this screen, then I'll hide it — what does this app do?"* — Predict: "my bookshelf" / "everything I'm reading." Tests whether the featured card + shelf labels carry the capability without reading body text.
- **Capability:** *"What would you click first here, and what do you expect to happen?"* — Predict: the featured cover, expecting that book's detail. Tests its click affordance.

## 4. First read

**Signals capability/value at a glance?** Yes — the headline is the largest element and the only other thing above the fold is one featured "Continue reading" card (real cover, real progress), nothing competes with it.

**Does everything earn its place?** Now, yes — wasn't always true (before/after below).

**Grouping (Gestalt), by screen:**
- *Library Home:* **proximity** (tight label→row, generous gap between shelves = distinct groups); **common region** (featured card's own background separates it from the rest); **similarity** (identical card treatment across shelves = one system).
- *Book Detail:* **common region** — the "Your copy" panel visually separates book facts from the reader's own relationship to it.
- *For You:* **common region** groups the recommendation as one object; size hierarchy (one large card vs. two small ones) signals primary vs. secondary.

**Stay on mission / nav back everywhere?** Yes — Book Detail has an explicit back-link plus the nav bar; For You has the nav bar. No screen adds unrelated content (no settings, accounts, upsells).

**Before / after (concrete revision):** Trying to be more compact, an early pass packed shelves into a 3-column grid with ~2px gaps, an abstract "44/12" stat tile instead of a real example, a subhead restating the headline, and a status pill on every card repeating its own shelf's label. Nothing signaled what mattered — everything competed equally. Rebuilt as single-column shelves with a real spacing scale, one featured book as the focal point, and the redundant subhead/pills removed.

**What the AI got wrong/oversimplified, and the fix:**
- Gradient placeholder covers → real cover art from Supabase (Open Library for the few not yet owned).
- A small hand-picked ~17-book set → real `most_wanted`/ownership/finished data (also fixed miscategorized books, e.g. *Six of Crows* was marked "want to read" but is actually owned and finished).
- Native scrollbar under shelf rows clashed with the rest of the design → custom arrow buttons.
- "Book" sat in top nav despite being a drill-down, not a destination → removed; reachable only by clicking a cover.

## Running locally

Static single HTML file, no build step:
```
python -m http.server 8000
```
Then open `http://localhost:8000`.
