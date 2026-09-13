# Commonplace

A three-screen product prototype for a personal reading app — *your entire reading life, organized around you*.

This is a proof-of-concept, not a production app: no auth, no backend, no real recommendation engine. Interactions and personal data (statuses, ratings, reviews) are mocked or held in memory for the session so the core product idea can be clicked through and user-tested.

**Live prototype:** https://commonplace-ten-iota.vercel.app

> **Note to reviewer:** Sections 3–5 below were drafted with AI assistance per the assignment's own suggestion ("With AI's help..."), but per Step 7 the final pass on the first-read and predictions should be human — treat the predictions and first-read judgments below as a starting draft to confirm, argue with, or rewrite before this is submitted.

---

## 1. Need, persona, capability, value

| | |
|---|---|
| **Need** | Active readers struggle to keep the books they own, borrow, want, and read organized in one place that reflects how they actually manage their reading life. |
| **Persona** | Avid readers who read regularly, maintain a growing TBR, and get books from a mix of physical purchases, ebooks, and libraries. |
| **Primary capability** | Build and manage one personal library containing every book they own, want, borrow, or read. |
| **Fundamental value** | **Control.** Readers can keep their reading life organized around their own habits, preferences, and tastes instead of scattering it across shelves, apps, lists, and generic book databases. |

## 2. The three screens

| Screen | Single job | Why it earned a slot | Design question it answers |
|---|---|---|---|
| **Library Home** | Show the reader's entire reading life in one organized, personalized place. | The clearest demonstration of the core value: one personalized home for the reader's entire reading life, not a database of books. | Can a first-time user understand within a few seconds that this is a personalized home for their whole reading life? |
| **Book Detail** | Show a book's general info alongside the reader's personal relationship to it (status, rating, review). | Demonstrates the difference between merely looking up a book and making that book part of a personal reading system. | Do users understand that the book is personally managed rather than existing only as a generic database entry? |
| **For You (Recommendations)** | Deliver one thoughtful, reasoned recommendation — not a wall of covers. | Demonstrates the payoff of having the reader's entire reading life in one place: the product can eventually understand taste deeply enough to make a recommendation that feels human and specific rather than generic. | Do readers feel that the recommendation understands *why* they enjoy certain books, rather than simply matching genre or popularity? |

Book data and cover art for Library Home and Book Detail are pulled from a real personal library (Supabase) — including the real `most_wanted`/TBR flag, ownership status, and finished status, not a hand-picked sample. A handful of titles referenced only on the For You screen (the recommendation itself, and its two secondary picks) aren't in that library yet, since they're meant to be new to the reader; their covers come from Open Library instead.

## 3. Feedback question plan

Questions only — no findings yet. Each has a prediction and the part of the prototype it's testing.

**Need**
> "Tell me about the last time you wanted to start a new book but couldn't remember what you already owned, or what you'd put on hold at the library. What did you end up doing?"
- *Prediction:* They'll describe re-buying or re-borrowing something they already had, or checking two or three apps before giving up and just reading whatever was already open on their phone.
- *Rests on:* The Borrowed shelf sitting alongside Owned and Want to Buy on one screen — testing whether the scattered-across-apps problem actually resonates as something they've lived.

**Value**
> "If you could see everything you own, borrow, and want to read in one place, what's the one or two words you'd use for how that would feel? Why?"
- *Prediction:* "Control" or "relief" — testing whether the landing screen's framing and the personal-status card on Book Detail actually deliver that feeling, rather than just being another catalog with a nicer coat of paint.

**Persona**
> "How often do you add a book to some kind of want-to-read list, and where does that list actually live right now?"
- *Prediction:* They'll name a fragmented place — a Notes app, a Goodreads shelf, a mental list — testing whether the app's single "Up Next" shelf feels like a real upgrade over that scatter.

**Capability**
> "I'm going to show you this screen for five seconds, then hide it. What do you think this app does?"
- *Prediction:* "It's my bookshelf" or "everything I'm reading" — testing whether the featured "Continue reading" card and shelf labels carry the capability without the reader needing to read supporting text.

> "What would you click first on this screen, and what do you expect to happen?"
- *Prediction:* They click the featured book cover — the largest, most personal element on the page — expecting to land on more detail about that specific book, testing whether it reads as obviously clickable.

## 4. Design justification and first read

*Opening the live URL as if I'd never seen it:*

**Does the landing screen signal the primary capability and value at first glance, before reading?** Mostly yes. The headline ("Your entire reading life, organized around you") is the largest text on the page and the only thing above the fold besides one featured book — there's no second competing headline, stat block, or call-to-action fighting for the same attention. The featured "Continue reading" card is the concrete proof: a real cover, a real progress bar, one click to the book. It's the single strongest signal on the page for "this is *my* library," which is the capability.

**Does every element earn its place, or does something compete?** After the last revision, yes — but it wasn't always true. See the before/after below.

**What belongs together on each screen, and which Gestalt principle communicates it?**
- *Library Home:* each shelf uses **proximity** — the label sits tight against its row of books, but the gap to the *next* shelf is deliberately much larger, so six shelves read as six distinct groups instead of one long list. The featured card uses **common region** (its own tinted background and border) to separate "this one book, right now" from "everything else." Every card across every shelf shares the same cover frame, shadow, and type treatment — **similarity** — so the whole screen reads as one system even though the content underneath varies wildly (a Hemingway paperback next to a sci-fi doorstopper).
- *Book Detail:* **common region** again — the "Your copy" panel (status, rating, review) sits in its own bordered card, physically separating "facts about this book" from "your relationship to this book," which is the entire point of the screen.
- *For You:* **common region** groups the whole recommendation into one object, and a clear size hierarchy (one large card vs. two small "also worth a look" cards) signals primary vs. secondary instead of presenting three equal-weight options.

**Do screens 2 and 3 stay on mission, and can you return to Library from everywhere?** Yes. Book Detail has an explicit "← Back to library" link in addition to the nav bar; For You only has the nav bar, which is sufficient since it's a top-level screen, not a drill-down. Neither screen introduces content that competes with its stated job (no settings, no account menu, no upsell).

**What did the AI initially get wrong, skip, or oversimplify — and what changed?**
1. First pass used generated color-gradient placeholders instead of real cover art. Changed to pull actual cover images from the Supabase library (and Open Library for the few titles not yet owned).
2. First data pass used a small, hand-authored set of ~17 books rather than the library's real signal for what's actually next to read. Changed to use the real `most_wanted` flag, ownership status, and finished status — which also surfaced a few miscategorizations (e.g., *Six of Crows* had been marked "want to read" when the real data shows it as owned and finished).
3. In trying to make the page more compact, the AI overcorrected into a dense 3-column shelf grid with a 2px gap between rows and a redundant status label repeated on every single card. **This is the concrete before/after:**
   - *Before:* multiple shelves side-by-side with almost no gap between them, an abstract "44 / 12" stat tile instead of a real example, a subhead paragraph that just restated the headline in different words, and a text pill on every card repeating its shelf's own label (an "Owned" shelf full of cards each individually labeled "OWNED"). Nothing signaled which element mattered most — everything was competing at the same visual weight.
   - *After:* single-column shelves with a real spacing scale, one featured book as the dominant focal point, the redundant subhead and pills removed entirely.
4. The native browser scrollbar under each shelf row clashed with the rest of the hand-designed visual system. Changed to small custom arrow buttons that match the site's palette and disappear when a shelf doesn't need to scroll.
5. "Book" sat in the top nav even though it's a drill-down from a specific cover, not a real top-level destination a user would navigate to directly. Removed it — Book Detail is now reached only by clicking a cover, which is a more honest signal of what kind of screen it is.

Each of these changes was motivated by a specific signaling or grouping problem, not a preference — that's the distinction the assignment asks for.

## Running locally

This is a static, dependency-free single HTML file — no build step.

```
python -m http.server 8000
```

Then open `http://localhost:8000`.
