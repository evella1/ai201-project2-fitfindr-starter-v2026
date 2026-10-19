# FitFindr

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first** — setup, every
> command, and what to do when something breaks.
>
> Once `python test.py` passes:
>
> ```bash
> python app.py listings --full -n 6      # read the data (Milestone 1)
> python app.py fields                    # what you can filter on
> python app.py ask 'vintage graphic tee under $30'
> ```
>
> All three tools are stubs, so that last command will do nothing useful yet.
> That's the starting position.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     HOW TO USE THIS FILE

     This is your submission. Fill each section in as you finish the milestone
     it belongs to — don't leave it all to the end.

     Unit 3 asks for the first five sections. Unit 4 adds the five below them.
     Leave the unit 4 sections alone until then; they're here so you know
     what's coming.

     Everything is pasted as TEXT. No screenshots, no images, no video links.
     A typed block of output gets full credit; a picture of the same output
     gets none.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 3 — THE BUILD ═══════════════════════ -->

## What This Does

<!-- Three or four sentences: what a user asks for, and what they get back. -->



---

## Tool Inventory

<!-- Four lines per tool. This is worth 2 points and it's the single most
     common place students lose them.

     "Returns a list" earns NOTHING. The description has to say what is IN
     the list.

     The empty case isn't optional either — it's the thing your loop branches
     on, and if you don't decide it here you'll discover it as a crash in
     Milestone 5. -->

### `search_listings`

- **What it does:**  searches the listings file and returns matches
- **Inputs:**  description (string), size (string), max_price (float)
- **Returns:** listing (list[dict])
- **When it has nothing:** an empty list

### `suggest_outfit`

- **What it does:** takes an item and a wardrobe, returns outfit ideas
- **Inputs:** new_item (dictionary), wardrobe (dictionary)
- **Returns:** outfit (string)
- **When it has nothing:** general styling advice

### `create_fit_card`

- **What it does:** what it does: writes a short caption someone would actually post.
- **Inputs:** outfit (string), new_item (dictionary)
- **Returns:** fit_card (string) - 2-4 sentences
- **When it has nothing:** descriptive message

---

## Planning Loop

<!-- Your branch rule, stated as a rule — the condition AND both paths — plus
     the file and function that holds it.

     Like this:
       "If search_listings returns an empty list, put a message in the session
        and stop. Otherwise take the first result and go to suggest_outfit."
        — agent.py::run_agent

     The grader checks your code against what you claim here, so the file and
     function have to be real. -->

**Branch rule:**

**Where it lives:** `agent.py::run_agent`

**How the query is parsed:** <!-- regex, string splitting, or asking the model — say which -->

**What moves through the session:** <!-- which fields, in what order -->

---

## Sample Run

<!-- Two things go here.

     1. One FULL query and its output, pasted as text.
     2. Your three per-tool terminal tests — the command and what it printed. -->

**One full query**

```
$ python app.py ask '...'

```

**The three tools, tested one at a time**

```
$ python -c "from tools import search_listings; print(search_listings('graphic tee', max_price=30))"

```

```
$ python -c "from tools import suggest_outfit; ..."

```

```
$ python -c "from tools import create_fit_card; ..."

```

---

## How I Used AI

<!-- Two specific moments. What you asked, what came back, what you changed.

     "I used Claude to help me code" is not enough.

     "I gave Claude my search_listings spec. It returned None on no match
     instead of an empty list, so I changed it" is the level we want. -->

**Moment 1**

- *What I asked for:*
- *What came back:*
- *What I changed:*

**Moment 2**

- *What I asked for:*
- *What came back:*
- *What I changed:*

<!-- ═══════════════════════ UNIT 4 — THE TEST ═══════════════════════

     Don't fill these in during unit 3.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Run Log — Before

<!-- Five criteria, five tries each, in this exact format.

     Five, because your criteria are written out of five. Mark each try PASS
     or FAIL, count the passes, and read that count against your target — a
     row targeting 4 of 5 with three PASS cells is MISSED (3/5).

     `python run_eval.py --label before` runs everything and writes the table
     into results/. Paste it here and fill in the verdicts. -->

| Criterion | Target | Try 1 | Try 2 | Try 3 | Try 4 | Try 5 | Verdict |
|---|---|---|---|---|---|---|---|
| 1. matching query completes | 4 of 5 | PASS | PASS | PASS | PASS | PASS | MET (5/5) |
| 2. impossible query stops early | 5 of 5 | PASS | PASS | PASS | PASS | PASS | MET (5/5) |
| 3. state persists across tools | 5 of 5 | PASS | PASS | PASS | PASS | PASS | MET (5/5) |
| 4. fit card shows exact price | 4 of 5 | PASS | PASS | PASS | PASS | PASS | MET (5/5) |
| 5. general advice with empty wardrobe | 4 of 5 | FAIL | FAIL | FAIL | FAIL | FAIL | MISSED (0/5) |


**Real output from one try**, pasted as text, naming the file and function
that produced it:

Criterion 1, Try 1

```
[1] parse_query
      in:  vintage graphic tee under $30
      out: dict with keys: description, size, max_price
[2] search_listings (via MCP)
      in:  dict with keys: description, size, max_price
      out: 10 items: Y2K Baby Tee — Butterfly Print, Graphic Tee — 2003 Tour Bootleg Style, Vintage Band Tee — Faded Grey … +7 more
      →    10 match(es)
[3] select_item
      out: Y2K Baby Tee — Butterfly Print ($18.0, depop)
[4] suggest_outfit
      in:  Y2K Baby Tee — Butterfly Print ($18.0, depop)
      out: Hey there! This baby tee is an absolute steal for $18, and that butterfly print is so nostalgic. Here are two …
      →    10 wardrobe item(s)
[5] create_fit_card
      in:  Y2K Baby Tee — Butterfly Print ($18.0, depop)
      out: Found this cute Y2K butterfly baby tee on Depop for just $18 and I am obsessed! Styled it two ways: either run…
```

Criterion 5, Try 1

```
Nothing in the listings matched description 'Leather Belt between and $12', under $10.
Things to change: try broader words — 'jacket' finds more than 'cropped corduroy jacket'; raise the price ceiling above $10.
```

---

## Verdicts and Diagnoses

<!-- MET or MISSED per criterion against LAST UNIT's target, plus a sentence on
     how you decided.

     Then, for every miss: which of the four places it happened — a tool, the
     loop's branch, the session, or the model's output — AND the mechanism.

     Not a diagnosis:  "The fit card was bad."
     A diagnosis:      "The fit card criterion missed on 2 of 5 items. Both had
                        an empty brand field. My prompt puts the brand in the
                        first sentence, so the card opened with a blank and read
                        like a fragment. The tool worked; the prompt assumed a
                        field that isn't always there."

     Look for a pattern. Three misses on the same tool is one problem, not
     three. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 | Matching query completes | 4 of 5 | MET (5/5) | Every try returned a fit card. |
| 2 | Impossible query stops early | 5 of 5 | MET (5/5) | Every try stopped before suggest_outfit. |
| 3 | State preserved between tools | 5 of 5 | MET (5/5) | Same item reached both tools every time. |
| 4 | Fit card mentions exact price | 4 of 5 | MET (5/5) | Every card said "$30". |
| 5 | General advice with empty wardrobe | 4 of 5 | MISSED (0/5) | Search always came back empty. |

**Diagnoses**

**Criterion 5 missed 0/5 — a tool (agent.py::parse_query).** The parser
takes the first price in 'Leather Belt between $10 and $12' as the max ($10)
and leaves the rest in the description, so search finds nothing and
suggest_outfit never runs. The empty-wardrobe path works (diagnostic row
passed 5/5); the parser just can't handle price ranges.

**Pattern:** the earlier run missed criterion 5 for the same reason, so it's one
problem. Criteria 3 and 4 passed easily — I'd tighten 3 to check the item's id.


---

## Loop Trace

<!-- One full run, printed step by step, with the MCP call visible in it.

     `python app.py ask '...' --trace` once you've added the trace.step()
     calls in Milestone 2.

     Worth pasting BOTH the happy path and the empty-search path. The empty
     one should be visibly shorter, because it stops. If your two traces are
     the same length, your branch isn't working — and this is the fastest way
     anyone will ever find that out. -->

**Happy path**

```
[1] parse_query
      in:  track jacket size M under $50
      out: dict with keys: description, size, max_price
[2] search_listings (via MCP)
      in:  dict with keys: description, size, max_price
      out: 2 items: 90s Track Jacket — Navy/White Stripe, Shacket — Olive Canvas
      →    2 match(es)
[3] select_item
      out: 90s Track Jacket — Navy/White Stripe ($45.0, poshmark)
[4] suggest_outfit
      in:  90s Track Jacket — Navy/White Stripe ($45.0, poshmark)
      out: Hey there! That 90s Champion track jacket is an absolute goldmine—navy and white is such a classic combo, and …
      →    10 wardrobe item(s)
[5] create_fit_card
      in:  90s Track Jacket — Navy/White Stripe ($45.0, poshmark)
      out: scored this vintage 90s champion track jacket on poshmark for just $45 and i am obsessed 🤌🏼 tossing it over ba…
```

**Empty search**

```
empty search

[1] parse_query
      in:  designer ballgown size XXS under $5
      out: dict with keys: description, size, max_price
[2] search_listings (via MCP)
      in:  dict with keys: description, size, max_price
      out: [] (empty)
      →    0 match(es)
[3] branch
      →    search returned []: stopping before suggest_outfit

Nothing in the listings matched description 'designer ballgown', size XXS, under $5.
Things to change: try broader words — 'jacket' finds more than 'cropped corduroy jacket'; drop the size, or try a neighbouring one; raise the price ceiling above $5.
```

**empty wardrobe**
```
[1] parse_query
      in:  vintage band tee under $25
      out: dict with keys: description, size, max_price
[2] search_listings (via MCP)
      in:  dict with keys: description, size, max_price
      out: 10 items: Graphic Tee — 2003 Tour Bootleg Style, Vintage Band Tee — Faded Grey, Y2K Baby Tee — Butterfly Print … +7 more
      →    10 match(es)
[3] select_item
      out: Graphic Tee — 2003 Tour Bootleg Style ($24.0, depop)
[4] suggest_outfit
      in:  Graphic Tee — 2003 Tour Bootleg Style ($24.0, depop)
      out: Hey there! Oh, a faded bootleg tee is an absolute thrift-store holy grail—that worn-in cotton feel is just unb…
      →    0 wardrobe item(s)
[5] create_fit_card
      in:  Graphic Tee — 2003 Tour Bootleg Style ($24.0, depop)
      out: scored this 2003 tour bootleg style graphic tee on depop for just $24 and the worn-in cotton is literally unma…
  Found:    Graphic Tee — 2003 Tour Bootleg Style — $24.0 on depop

  Outfit:   Hey there! Oh, a faded bootleg tee is an absolute thrift-store holy grail—that worn-in cotton feel is just unbeatable. Since it has that effortless, grungy streetwear energy, here are two super easy ways to style it depending on your vibe:

**The Off-Duty Cool Look:** Pair the tee with some relaxed, mid-rise light wash denim (a little distressing or carpenter-style pockets would look amazing here) to lean into that 2000s slouchy silhouette. Throw on a pair of beat-up canvas sneakers or chunky retro skate shoes, and accessorize with a simple silver chain necklace and a black nylon shoulder bag to tie the whole effortless vibe together.

**The Edge-meets-Ease Look:** Tuck the boxy tee into a black pleated tennis skirt or a distressed denim midi skirt to play with proportions. Layer an oversized, boxy zip-up hoodie over top (leave it unzipped so the graphic peeks through), and finish it off with some platform combat boots and cozy crew socks.It’s equal parts edgy and comfortable, perfect for running errands or hitting up a concert!

  Fit card: scored this 2003 tour bootleg style graphic tee on depop for just $24 and the worn-in cotton is literally unmatched. styling it with slouchy light wash denim and beat-up sneakers for the ultimate off-duty grunge look. absolute holy grail find!
```

**model unavailable**
```
[1] parse_query
      in:  oversized denim jacket for a rainy day
      out: dict with keys: description, size, max_price
[2] search_listings (via MCP)
      in:  dict with keys: description, size, max_price
      out: 10 items: Denim Jacket — Light Wash, Cropped, Vintage Levi's 501 Jeans — Medium Wash, Oversized Flannel Shirt — Plaid Red/Black … +7 more
      →    10 match(es)
[3] select_item
      out: Denim Jacket — Light Wash, Cropped ($42.0, poshmark)
[4] model unavailable
      →    stopping, search results kept

The model couldn't be reached, so the outfit and caption steps didn't run. The search worked — 10 listing(s) were found. Check GEMINI_API_KEY in your .env, then run the same query again.
What the service said: The model rejected your API key. Check GEMINI_API_KEY in your .env file, or create a fresh key at aistudio.google.com.
```

**On the MCP move:** <!-- what changed in your code, and whether anything
behaved differently afterwards. If the rewire didn't work, say exactly where it
broke — the error text and the last thing that worked. That earns the point in
full. -->



---

## The Improvement

<!-- What you changed, why your diagnosis pointed at it, and the after-run in
     the same table format. One change, measured properly.

     `python run_eval.py --label after` -->

**What I changed:** parse_query now recognises price ranges
between $10 and $12, $10-$12, $10 to $12) and uses the upper bound as
max_price, removing the range from the description.

**Which failure it was meant to fix:** Criterion 5 — the range was misread, so
search returned nothing and suggest_outfit never ran.

### Run Log — After

| Criterion | Target | Try 1 | Try 2 | Try 3 | Try 4 | Try 5 | Verdict |
|---|---|---|---|---|---|---|---|
| 1. matching query completes | 4 of 5 | PASS | PASS | PASS | PASS | PASS | MET (5/5) |
| 2. impossible query stops early | 5 of 5 | PASS | PASS | PASS | PASS | PASS | MET (5/5) |
| 3. state persists across tools | 5 of 5 | PASS | PASS | PASS | PASS | PASS | MET (5/5) |
| 4. fit card shows exact price | 4 of 5 | PASS | PASS | PASS | PASS | PASS | MET (5/5) |
| 5. general advice with empty wardrobe | 4 of 5 | PASS | PASS | PASS | PASS | PASS | MET (5/5) |


**Did it help, and how do I know:** Yes. Criterion 5 went from 0/5 to 5/5 with
the same query. The search now finds the belt, and suggest_outfit gives
general advice with an empty wardrobe. The other four criteria didn't change.

```
[1] parse_query
      in:  Leather Belt between $10 and $12
      out: dict with keys: description, size, max_price
[2] search_listings (via MCP)
      in:  dict with keys: description, size, max_price
      out: 1 items: Leather Belt — Brown, Braided
      →    1 match(es)
[3] select_item
      out: Leather Belt — Brown, Braided ($12.0, thredUp)
[4] suggest_outfit
      in:  Leather Belt — Brown, Braided ($12.0, thredUp)
      out: Hey there! Oh, a braided leather belt is absolute gold for a thrifted wardrobe—it adds just enough texture to …
      →    0 wardrobe item(s)
[5] create_fit_card
      in:  Leather Belt — Brown, Braided ($12.0, thredUp)
      out: Found this vintage braided leather belt on thredUP for just $12, and it’s about to live on my straight-leg jea…
```


---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped where
     you did. "I ran out of time" is fine if it's true. Pretending nothing is
     left is not. -->

All five criteria are met, but some things are still weak:

- In an earlier run, criterion 1 dropped to 3/5 because of 503 UNAVAILABLE  errors, and the error message wrongly tells the user to check
  GEMINI_API_KEY. I'd add a retry and a clearer message.
- Search only accepts a max price, so '$10-$12' really means "up to $12".
- 'floral dress size M for less than $40' leaves "for" in the description. It still matches, but it could break other queries.
- Criteria 3 and 4 always passed. I'd tighten 3 to compare the item id and 4 to an exact price string.



<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 3

       [ ] criteria.md has five numbered criteria, each with a target
       [ ] Each criterion has a reason underneath it
       [ ] All five unit 3 sections above have real content
       [ ] Tool Inventory: all three tools, inputs WITH TYPES, a specific
           return value, and the empty case
       [ ] Planning Loop names the branch rule and agent.py::run_agent
       [ ] Sample Run: one full query plus the three per-tool tests, as text
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN, you submit the same one
           next unit

     SUBMISSION CHECKLIST — unit 4

       [ ] mcp_server.py exists with one tool registered
           (or a written record of exactly where the rewire broke)
       [ ] Run Log — Before, five criteria, five tries each
       [ ] Real output pasted underneath, naming file and function
       [ ] A verdict on every criterion
       [ ] A diagnosis for every miss, naming a place AND a mechanism
       [ ] Loop Trace, with the MCP call visible in it
       [ ] All three failure modes triggered and handled
       [ ] One improvement, with Run Log — After in the same format
       [ ] What's Still Broken
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository. Your commit history is what
     shows your criteria existed before your results did.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
