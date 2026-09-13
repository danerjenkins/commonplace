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

**Before / after (concrete revision):** Trying to make Home less sparse, an early pass packed shelves into a 3-column grid with ~2px gaps between them. That was the opposite failure — proximity broke down because *everything* was close together, so six distinct shelves read as one dense block with no dominant element. Called out directly as "spacing mashed together... no visual signal of what is most important... poor use of whitespace." Rebuilt with a real spacing scale (tight label-to-row, generous gap between shelves) and one dominant focal point — a single featured "Continue reading" card — instead of a same-weight stat tile competing with it.

**Revision log — what was flagged, and the fix:**
- *"Populate more books, use the tbr lists from Supabase"* → library grew from ~17 hand-picked titles to 44, driven by the real `most_wanted`, ownership, and finished fields (this also caught miscategorized data, e.g. *Six of Crows* had been marked "want to read" but is actually owned and finished).
- *"Too much telling... less words, more thoughtful design details"* → cut the subhead paragraph that just restated the headline, and the status pill repeated on every card even though its own shelf header already says the same thing (an "Owned" shelf where every card was also individually labeled "OWNED"). Status is now communicated once, by grouping, not per-card text.
- *"The scroll bar doesn't mesh with the design... maybe just an arrow on the side"* → the native browser scrollbar was the one un-styled, generic element in an otherwise custom system. Replaced with small circular arrow buttons in the site's own palette that fade out when a shelf doesn't overflow.
- *"'Your Library' is too close to the nav bar"* → the gap between the sticky nav and page content was increased twice (52px, then 72px) until it read as intentional breathing room rather than a layout accident.
- *"Remove Book from the nav bar, only reachable by clicking the image"* → Book Detail is a drill-down from a specific cover, not something a user chooses to navigate to directly, so keeping it as a top-level tab misrepresented the app's own structure. Removed; nav now only lists real top-level destinations (Library, For You).

## Running locally

Static single HTML file, no build step:
```
python -m http.server 8000
```
Then open `http://localhost:8000`.
