# Grounded Labs Toolroom

Everything we've learned about making a website feel like the business it belongs to,
kept in one place so nobody learns it twice.

**This is internal.** It is never shown to clients. If a client needs to see a
reference, show them a real site in their industry.

A toolroom isn't where product gets made — it's where the jigs, fixtures and gauges get
made. That's this. Not client work; the tooling that makes client work come out
consistently good.

| | |
|---|---|
| **Build** *(in the library page)* | the trigger phrase, the twenty-minute procedure, the bad-input playbook and the audit — the **procedure** |
| **[`research/`](research/)** | how to find out what's actually true about a client, and prove it — the **gauge** |
| **[`effects/`](effects/)** | working, debugged interaction code you can lift — the **fixtures** |
| **Patterns** *(in the library page)* | the two questions that place any business — the **classifier** |
| **Copy** *(in the library page)* | headline formulas, voice by register, word budgets, copy crimes — the **words** |
| **Kit** *(in the library page)* | tokens, layout archetypes, utility components, photo treatment, edge language — the **furniture** |
| **[`standards/`](standards/)** | accessibility, performance, and demo-vs-ship values — the **tolerances** |

**New here?** Open **[`effects/effects-library.html`](effects/effects-library.html)** in a
browser. It opens on the **Build** tab — the procedure — and everything else is reference the
procedure sends you to. Then go to **Effects** and move your cursor through every stage. Then read
[`research/README.md`](research/README.md) and fill in a research card for a business you
already know — a café near you, your gym. Doing it once on something familiar is the
fastest way to see what the card catches that intuition misses.

> ⚠️ **Status: unvalidated, v1.** The research half has been run once against a real
> client. **The build half has never been run.** Nobody has taken research from this
> process through to a finished page, so there is no evidence yet that it produces
> better work than taste would have. Treat it as a hypothesis you are helping test.

---

## 1. What we actually do

We take a small business with a real identity and a website that undersells it, and we
**elevate the execution without rebranding the company**.

> **We don't touch the brand. We light it.**

Almost every local business already owns everything needed — an origin story, a
distinctive product, colors, a vocabulary, a tagline. It's usually buried under promo
bars and product grids. The job is to find what they own, move it to the front, and give
it dimension.

**What this is not:** not a rebrand, not a copywriting exercise (their words are usually
better than ours), and not a template. If the output could belong to a different client,
start over.

---

## 2. The workflow

Seven phases. **Do them in order.** Each has a gate — don't start the next until the gate
passes. Most of the damage in the first run came from skipping ahead.

| # | Phase | Time | Output |
|---|---|---|---|
| 1 | Access check | 10 min | a stated list of what you can and can't reach |
| 2 | First-party scrape | 30 min | their raw HTML/CSS on disk |
| 3 | Measure | 20 min | palette + brightness table, all measured |
| 4 | Mine words & structure | 30 min | verbatim copy, latent structure |
| 5 | Diagnosis | 15 min | **one sentence** |
| 6 | Direction | 45 min | constraints, no code |
| 7 | Build | varies | the page |

Phases 1–6 are [`research/README.md`](research/README.md) in full detail. Phase 7 is
[`effects/`](effects/) and [`standards/`](standards/).

**Two gates worth calling out:**

- **Phase 1's gate is a written statement of what you couldn't reach.** A blocked fetch
  is a finding to report, not a hole to paper over with a search summary. The worst
  failure of the first run was describing research in a way that implied a site had been
  read when every fetch had been blocked — everything downstream inherited that.
- **Phase 5's gate is one sentence.** If the diagnosis needs a paragraph, you don't have
  it yet.

---

## 3. Evidence tiers — tag every fact

The discipline that prevents the most expensive mistakes.

| Tier | Source | Use it? |
|---|---|---|
| **A — Measured** | bytes you downloaded and parsed | build on it |
| **B — Verbatim** | their own copy, quoted exactly, with the URL | build on it |
| **C — Human-verified** | screenshot or statement from a person | build on it |
| **D — Search summary** | third-party paraphrase | **lead only** — corroborate first |
| **E — Inference** | reasoned from A or B | label it; say what would disprove it |
| **F — Imagination** | your mental model of the brand | **never ship** |

**The cautionary pair, both from the first run:** an *inference* that a site ran on
Shopify — reasoned from its URL patterns — was correct. A *guess* about the brand's
dominant colour survived three rounds of discussion until measurement killed it; the
guessed colour wasn't even in their palette.

The difference wasn't luck. The inference was falsifiable and got checked. The guess was
never tested, because nothing in the process required testing it.

---

## 4. Tool reality — route by source type

Automation and humans have different reach. This table saves the most time of anything
here.

| Source | Automated fetch | Route to |
|---|---|---|
| Client's own site | ✅ reliable | you, scripted |
| Client's CDN images | ✅ reliable | you + ImageMagick |
| Google / Bing / DuckDuckGo | ❌ shells, bot checks, junk | **a human's browser** |
| Instagram / TikTok / Facebook | ❌ 429 / 400 / empty JS | **a human's browser** |
| Yelp / Google reviews | ⚠️ varies | try once, then a human |

**Two failures on one source means switch source, not technique.** The first run burned
four attempts on Instagram — profile, API, embed, headless browser — when the answer was
one screenshot from a person.

**Batch the human-only asks into your first message:** Google Images for
`"<brand>" interior`, the Instagram grid, the homepage as they see it, the top ~10
reviews, and any brand assets they hold.

**For cafés, studios, gyms and salons the brand lives on Instagram more than the
website.** Skipping it means missing the identity. Ask on day one.

---

## 5. Known failure modes

Every one of these happened in the first run.

1. **Claiming a fetch succeeded when it was blocked.** Poisons everything downstream.
2. **Shipping a tier-F guess.** The palette guess.
3. **Measuring an unverified image.** An image search returned unrelated product photos;
   the palette math ran perfectly and produced a fictitious brand palette.
4. **Trying one blocked source four ways** instead of switching sources.
5. **Generating paid assets with no visual reference.** Text-only prompts produce stock
   that could belong to any competitor.
6. **Not confirming the medium first.** Assets were generated one message before that
   entire medium was ruled out.
7. **Importing a reference's mood along with its mechanics.**
8. **Shipping demo-amplitude motion.** See [`standards/`](standards/).

---

## 6. What to send back

The workflow is unproven, so your friction is data. When you finish a client, report:

- Where the phase gates were wrong — too slow, too strict, wrong order
- Anything in §4 that has changed — platforms adjust their blocking constantly
- Ship values you had to retune, and for what kind of content
- Failure modes not in §5 — add them
- How long each phase actually took versus §2

Open a PR. The docs are the product as much as the code is.

---

## 7. Legal and ethical floor

Most of what we make starts as **unsolicited concept work**. Normal practice, with rules:

1. **Label concept work in the page** — visible and persistent, so nobody can mistake it
   for a live site.
2. **Invent nothing.** No prices, reviews, testimonials, classes, credentials, claims or
   links you haven't verified. Tier A–C only.
3. **Respect marks.** Registered trademarks carry their ®.
4. **Use their real links.** Verify; don't guess a URL pattern.
5. **Never imply a relationship that doesn't exist.**
