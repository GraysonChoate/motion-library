# Summer Moon Coffee — locked creative direction

Unofficial concept study. No affiliation with Summer Moon Coffee.
Locked 2026-08-17. Everything here derives from measured data in
`03-summer-moon-research.md` — no invented facts.

---

## The thesis

> **We don't touch the brand. We light it.**

Their identity already contains the whole idea — oak fire, a moon, gold, cream,
"Velvet Blaze," 24 years. Nothing needs inventing. The current site is a Shopify
storefront presenting a *craft fire ritual* as a product grid.

The elevation is entirely **cinematography and motion**, not new brand.
Same palette, same marks, same words — shot properly for the first time.

## The diagnosis, in one sentence

> **The homepage is a coupon. The story is in the basement.**

The homepage opens with three stacked promo bars (a FIRSTBREW discount code, Beach
Fire brew of the month, a free tumbler), then merch tiles. The first real brand
statement sits *below* the merchandising. Meanwhile their best writing — "midnight
alchemy," "A SPARK," "always better, never bitter" — is two clicks deep on
`/pages/about` and `/pages/our-story`.

The fix requires no new brand elements. Move what they already wrote to the top,
and light it.

## Structure — theirs, not ours

`/pages/our-story` is already built in three named acts:

> ### A SPARK. → WILDFIRE. → THE AFTERGLOW.

A fire's full lifecycle. That is the scroll spine, pre-written by the client. It
maps directly onto **COP-03 (sticky set swap)**.

Reinforcing it: every product is named for a state of fire — Velvet Blaze, Inferno,
Afterglow, Billowing, Blue Blazes, En Fuego, Fire Light, Fireside, Glowing Ember,
Spark, Sweet Hearth, Swinging Lantern. **The brand's own naming system is the art
direction.**

## The temperature arc

Fire and moon are opposite temperatures, and the brand is both at once. Oak fire
roasts the bean; Moon Milk cools and sweetens it. The name *is* the product.

The page travels that gradient: **ember at the top, moonlight at the bottom.**

| Beat | Temperature | Techniques |
|---|---|---|
| Hero — "Roasted over oak." | ember, darkest | DEP-01, REA-01, COP-01 |
| A Spark — the 2002 auction | ember → warm | DEP-02, COP-02 |
| Wildfire — every brick by hand | warm, balanced | COP-03, REV-01 |
| The Afterglow — 70 rooms, one fire | cooling | REV-02 |
| Moon Milk® — find your sweet spot | cream, coolest | REV-03 (The Ratio) |
| Locations — "the moon is closer than you think" | slate/moonlight | DEP-03 |

## Signature interaction — The Ratio

Their real menu lets customers order Moon Milk by fraction: **⅛ · ¼ · ½ · ¾**.
Nobody in coffee has an interaction this ownable, and **they already named it**:
*"FIND YOUR SWEET SPOT."*

Picking a ratio floods cream upward through a gradient mask while the stage's colour
temperature travels with it — ember at ⅛, full moonlight at ¾. See **REV-03**.
No video, no images.

## Palette — measured, not chosen

From their own HTML (frequency ranks importance) and their own photography:

| Token | Hex | Source |
|---|---|---|
| gold *(dominant)* | `#E3B245` | 25 occurrences in their HTML — the brand colour |
| teal | `#108474` | 13 occurrences — the cool counterpoint |
| cream | `#FEF9E5` | their pale cream |
| deep gold | `#C08400` | |
| roast brown | `#451C12` | |
| near-black | `#241F21` | dominant colour of their own fire photograph |
| ember orange | `#A45126` | measured from that fire photograph |
| flame tan | `#DEAC82` | measured from that fire photograph |
| slate blue | `#6D7B9D` | **present in all three store photos** |

⚠️ **Do not use navy.** An early guess called this a navy brand; measurement proved
it wrong. The cool axis is **slate-blue and teal** — their moon is dusk-coloured,
not midnight-coloured.

### Brightness is a directive, not a taste call
Their store photographs measure **31% (Burnet Rd), 45% (South First), 50% (Frisco)**
mean brightness. Their rooms are genuinely dark. **A dark page is faithful to them**,
not a style imposed on them. Target that range.

### The one hard rule
**Ember is not neon.** Orange must read as firelight and glowing coal — physical
light with falloff, sitting inside the image. The moment it becomes a CSS glow or a
gradient laser, this turns into every other dark tech site and the wood fire — which
*is* the brand — is gone.

## Copy — use theirs, verbatim

- **"always better, never bitter"** — the tagline
- **"The formulation of Moon Milk is a story of midnight alchemy. Under a summer
  moon, late into the night, we landed on our legendary creamer."**
- "There's a natural affinity between a wood fire and coffee beans."
- "We drew up the plans, laid every brick by hand"
- "Our team of roasters use sight, sound, and smell"
- **"THE MOON IS CLOSER THAN YOU THINK"** — their locator headline
- **"FIND YOUR SWEET SPOT"** — the Moon Milk CTA
- "Time Honored Traditions" · "FROM OUR HANDBUILT ROASTERS TO YOU"
- Brand hashtag: **#COFFEEUNPLUGGED**

## Constraints anyone building this must respect

1. **Moon Milk® is a registered trademark.** Footer: "Logo, Moon Milk, and Related
   Marks are Registered Trademarks of Summer Moon Coffee." Carry the ®.
2. **Shopify**, theme `t/88`. Cart, store locator, and franchise-inquiry paths must
   survive any homepage rework.
3. **`locations.summermooncoffee.com`** is a separate location-page subdomain.
4. ⚠️ **They run trial-licensed fonts in production** — `Plaak5Trial45BoldB`,
   `Plaak6Trial46Bold`. Real liability. Worth raising if this ever reaches them.
5. **No video.** Direction assumes stills + procedural motion only. Every technique
   in the bench works without a single video asset.
6. **Unofficial concept work must be labelled in the page**, and may contain no
   fabricated prices, reviews, testimonials, or claims.

## Explicitly rejected

- **Navy-dominant palette** — measurement disproved it.
- **Scroll-scrubbed video hero** — anonymous stock fire would be the least
  Summer Moon thing on the page. Depth-layer parallax beats it *and* answers the cursor.
- **Importing the reference files' mood.** The Cortex / veldara / Urban Jungle builds
  are cold neural-tech launches. Steal the mechanics; reject the genre. A coffee brand
  rendered in that mood becomes "an AI startup that happens to sell lattes."

## Still open

**Their photography.** Every plate in the bench is procedural — layered gradients
standing in for the roaster, brick, coals. Drop real plates into DEP-01 and DEP-03
and the depth stops being a demonstration and becomes a place.

**Needed:** a screenshot of Google Images for `"summer moon coffee" interior`, and the
IG grid. Instagram and search engines both block automated access from a datacenter IP
(see the method boundary table in `01-research-playbook.md`) — those inputs have to
come through a human's browser.
