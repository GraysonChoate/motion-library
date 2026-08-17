# Research Playbook

**Research is the whole job.** Everything downstream — direction, palette, copy,
motion — is a derivative of this phase. Get it wrong and you produce something
confident, polished, and about a company that doesn't exist.

This playbook has four parts, in order:

1. [**Collect**](#part-1--collect) — get real bytes, measure real things
2. [**Complete**](#part-2--complete) — a required-fields schema so gaps are visible
3. [**Verify**](#part-3--verify) — prove it, then try to break it
4. [**Conclude**](#part-4--conclude) — the diagnosis

Fill in `templates/research-card.md` as you go. **A card with blanks is a valid
deliverable. A card with guesses is not.**

---

## The four rules

1. **Never say "scraped" until bytes are on disk.** Report access status before
   findings, every time.
2. **Tag every fact with an evidence tier.** Mixing tiers is how a guess becomes a
   build spec.
3. **Measure colors and brightness. Never eyeball them.**
4. **Anything load-bearing needs two independent sources.** One source is a lead,
   not a fact.

---

## Evidence tiers — tag every claim

| Tier | Source | Use it? |
|---|---|---|
| **A — Measured** | bytes you downloaded and parsed | build on it |
| **B — Verbatim** | their own copy, quoted exactly, with the URL | build on it |
| **C — Human-verified** | screenshot or statement from a person | build on it |
| **D — Search summary** | third-party paraphrase | **lead only** — corroborate to A/B/C before use |
| **E — Inference** | reasoned from A or B | label it, and say what would disprove it |
| **F — Imagination** | your mental model of the brand | **never ship** |

**The cautionary pair, both from the first run:** an *inference* that the site was
Shopify — reasoned from `/collections/` and `/products/` URL patterns — was correct.
A *guess* that the brand was navy survived three rounds of discussion until
measurement killed it. Gold `#E3B245` was dominant the whole time.

The difference wasn't luck. The inference was **falsifiable and got checked**. The
guess was never tested because nothing in the process required testing it. That's
what Part 3 exists for.

---

# Part 1 — Collect

## 1.1 Access check

One probe per source. Write down what you reached and what you didn't.
**A blocked fetch is a finding to report, not a hole to fill with a search summary.**

## 1.2 Route by source type

| Source | Automated fetch | Route to |
|---|---|---|
| Client's own site | ✅ reliable | you, scripted |
| Client's CDN images | ✅ reliable | you + ImageMagick |
| Google / Bing / DuckDuckGo | ❌ shells, bot checks, junk | **a human's browser** |
| Instagram / TikTok / Facebook | ❌ 429 / 400 / empty JS | **a human's browser** |
| Yelp / Google reviews | ⚠️ varies | try once, then a human |

**Two failures on one source means switch source, not technique.** The first run
burned four attempts on Instagram — profile, API, embed, headless browser — when the
answer was one screenshot from a person.

**So batch the human-only asks into your first message:**
1. Google Images screenshot for `"<brand>" interior`
2. Instagram grid screenshot — nine tiles is their whole visual voice
3. Homepage screenshot as they see it
4. Screenshot of the top ~10 Google/Yelp reviews
5. Any brand assets they hold

**For cafés, studios, gyms, salons: the brand lives on Instagram more than the
website.** Skipping it means missing the identity. Ask on day one, not day three.

## 1.3 Scrape the first-party site

```bash
UA="Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 \
(KHTML, like Gecko) Chrome/126.0 Safari/537.36"
D="clientdomain.com"

curl -sL -A "$UA" "https://$D/" -o home.html -w "http=%{http_code} bytes=%{size_download}\n"
for p in pages/about pages/our-story pages/menu pages/faqs; do
  curl -sL -A "$UA" "https://$D/$p" -o "$(basename $p).html" -w "$p http=%{http_code}\n"
done
```

```bash
grep -oiE '(myshopify|cdn\.shopify|squarespace|wix|wp-content)' home.html | sort | uniq -c | sort -rn
grep -ohiE 'font-family:[^;}"]{0,80}' home.html | sort -u          # grep results for "Trial"
grep -ohE '#[0-9a-fA-F]{6}\b' home.html | tr 'A-Z' 'a-z' | sort | uniq -c | sort -rn | head -25
grep -ohE 'href="/[a-z0-9/_.-]{0,50}"' home.html | sort -u          # their real IA
grep -ohE '(cdn/shop/files|/assets)/[A-Za-z0-9_%.-]{3,80}\.(jpg|jpeg|png|webp)' home.html | sort -u
```

## 1.4 Measure the palette

**UI palette** — hex frequency in their HTML. Frequency ranks importance.

**Photographic palette** — from their own images:

```bash
for f in hero.jpg store1.jpg store2.jpg; do
  echo "=== $f brightness=$(convert "img_$f" -colorspace Gray -format '%[fx:int(mean*100)]' info:)% ==="
  convert "img_$f" -resize 140x140! -colors 8 -depth 8 -format %c histogram:info: \
    | sed 's/^ *//' | sort -rn | head -8
done
```

**Mean brightness is a design directive.** One client's rooms measured 31–50%, so a
dark page was *faithful* to them. If a client's rooms measure 80%, a dark page is a costume.

⚠️ **Verify an image depicts the client before measuring it.** An image search once
returned industrial V-belt product photos; the palette math ran perfectly and produced
a fictitious brand palette. Check filename, source domain, dimensions. **Correct
arithmetic on wrong inputs is more dangerous than an error, because nothing looks
broken.**

## 1.5 The customer-voice pass — do not skip

Read 20+ reviews (Google, Yelp, TripAdvisor) and the comments under their top
Instagram posts. You are hunting one specific thing:

> **The gap between how the business describes itself and how customers describe it.**

That gap is where the insight lives. Examples from the first run:

| The brand says | Customers say |
|---|---|
| "our signature blend" | *"this stuff is addictive"* |
| "a distinctive experience" | *"I drive across town for this"* |

**Record the word customers use that the brand never does.** It is almost always more
alive than anything on the site, and it is frequently the headline.

---

# Part 2 — Complete

Research isn't done when you run out of energy. It's done when **every field below is
either filled or explicitly marked NOT FOUND.** Blanks are information. Silence isn't.

Use `templates/research-card.md`. Every field carries a tier and a source URL.

**Identity** — trading name · founding year · founders · location count · HQ ·
ownership model (family / franchise / chain) · **the specific origin event**

**Product** — signature product (the one thing they're known for) · naming system, if
any · full categories · price band · trademarked terms

**Voice** — tagline(s) · your three best verbatim sentences · the vocabulary they own
(recurring distinctive words) · tone register · brand hashtag

**Visual** — measured palette, ranked · declared fonts + licensing flags · photography
style + **mean brightness** · logo + marks · description of their physical space

**Structure** — platform + theme · full nav IA · **latent narrative structure, if they
have one** · what the homepage leads with, in order · every conversion path (cart,
booking, locator, franchise, careers)

**Customer voice** — top three things customers actually praise, verbatim · the word
customers use that the brand doesn't · recurring complaints · why people travel for it

**Market** — nearby direct competitors · what this business does that they don't ·
**seasonal vs evergreen** (flag limited-time promos so nobody mistakes a summer
campaign for core identity)

**Gaps** — list everything you could not find, and why

### Two fields that most often get missed

**Latent narrative structure.** Check whether the client has already written their own
arc. On the one run so far, the story page carried a named three-act structure — a
complete scroll spine, sitting two clicks deep. **Never invent an arc before checking
for theirs.**

**A naming system.** If every product in a range shares a theme, that system **is the
art direction** — already decided, by the client.

---

# Part 3 — Verify

This is the part that didn't exist before, and it's why the palette guess survived.
Nothing here is optional.

## 3.1 The two-source rule

Anything **load-bearing** — a fact that changes the design if it's wrong — needs two
independent sources, or an explicit `SINGLE-SOURCE` flag on the card.

Load-bearing by default: palette · brightness target · tagline · origin story ·
signature product · narrative structure · trademarks · anything you plan to put in a
headline.

"Two sources" means genuinely independent. Their About page and their homepage are one
source (the company). Their site plus a news article is two.

## 3.2 Tier audit

Walk the card. For every field ask: **what tier is this, actually?**

Downgrade ruthlessly. Facts drift upward in confidence as they get repeated in
conversation — the palette guess started as tier F and was being treated as tier A within two
messages, purely through repetition.

**Anything still tier D, E, or F after this pass cannot enter the direction.**

## 3.3 Falsification — try to kill your own read

Before writing direction, attack your own conclusions three ways:

1. **The palette attack.** *If I'm wrong about the dominant color, what would I expect
   to see instead?* Go look for that. Check a page you haven't scraped yet.
2. **The story attack.** *Am I building on something they emphasize, or something I
   find charming?* If the origin story appears once in a footer, it isn't their story
   — it's your preference.
3. **The customer attack.** *Does anything in my read contradict what customers
   actually say?* If the brand's self-image and the reviews disagree, **the reviews
   win.** Customers describe the business that exists.

Write the outcome of all three on the card. "Attempted, survived" is a real result and
takes one line.

## 3.4 Freshness

Note the date you collected. Flag anything seasonal. A "Brew of the Month" promo bar
is not brand identity — but it will look like it if you scrape in August and build in
November.

---

# Part 4 — Conclude

## 4.1 The diagnosis

List what the homepage leads with, in order. List their strongest owned material.
**The gap is the thesis.** One sentence.

From the one run so far:

> **The homepage is a coupon. The story is in the basement.**

**Gate: one sentence.** If it needs a paragraph, you don't have it yet.

## 4.2 Definition of done

Research is complete when all seven are true:

- [ ] Every card field filled or marked NOT FOUND
- [ ] Every fact carries a tier and a source URL
- [ ] Every load-bearing fact has two sources, or a `SINGLE-SOURCE` flag
- [ ] Tier audit done; nothing below C entering the direction
- [ ] All three falsification attacks attempted and recorded
- [ ] Customer-voice pass done; the brand-vs-customer gap written down
- [ ] Diagnosis is one sentence

**If you cannot tick all seven, say so and name which are missing.** Handing over
partial research with the gaps labeled is useful. Handing over partial research that
looks complete is how the whole thing falls apart.

## 4.3 What good looks like

A colleague should be able to read your card and **reach your diagnosis without you in
the room.** If it only makes sense with your narration, the research isn't carrying it
— you are.
