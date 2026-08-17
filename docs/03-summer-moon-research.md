# Summer Moon Coffee — Research Dossier
Unofficial concept study. No affiliation with Summer Moon Coffee.
Gathered 2026-08-17. Method: curl + ImageMagick via Higgsfield cloud sandbox
(local egress proxy blocks all outbound fetches).

## Verification status
| Source | Status |
|---|---|
| summermooncoffee.com/ | ✅ 265,567 bytes, HTTP 200 |
| /pages/our-story | ✅ 187,357 bytes, HTTP 200 |
| /pages/about | ✅ HTTP 200 |
| /pages/standard-menu-summer-moon-coffee | ✅ HTTP 200 |
| theme base.css (t/88) | ✅ 67,871 bytes |
| Their own photography (7 files) | ✅ downloaded + palette-measured |
| **instagram.com/summermooncoffee** | ❌ **FAILED — see gap** |

## Platform
- **Shopify.** 143 `shopify` refs, `cdn.shopify`, `myshopify`. Theme `t/88`.
- Judge.me reviews app (`JudgemeStar` icon font).
- `locations.summermooncoffee.com` = separate location-page subdomain.
- Copyright line: "Copyright © 2026, Summer Moon Coffee"

## Measured palette

### UI colors (homepage inline styles, by frequency)
| Hex | Count | Reading |
|---|---|---|
| `#e3b245` | 25 | **Gold / amber — dominant brand color** |
| `#ffffff` | 18 | white |
| `#108474` | 13 | **teal — the cool counterpoint** |
| `#000000` | 7 | black |
| `#fef9e5` | 4 | pale cream |
| `#7b7b7b` | 4 | mid gray |
| `#fffaf0` | 2 | floral white |
| `#c08400` | 2 | deep gold |
| `#1e1e1e` / `#241f21` | 2 / 1 | near-black |
| `#451c12` | 1 | **dark roast brown** |
| `#fbcd0a` | 1 | bright yellow |
| `#2e66b0` | 1 | blue |

### Photographic palette (ImageMagick, their own images)
**`fire_c6dd69c6…jpg`** — their og:image, 1498×842. Literally a fire.
`#241E1F` near-black (dominant) · `#5B5254` warm gray · `#4E413F` brown-gray ·
`#532F25` roast brown · `#A45126` **burnt orange** · `#AB5D3D` terracotta ·
`#DEAC82` flame tan

**Store interiors** (their three flagship photos):
- South First Original (1500×1000, **45% brightness**): `#5F4935` `#38281F` `#8C705A` `#AA906E` warm woods; `#D8D2CF` plaster; **`#566C95` slate blue**
- Burnet Rd (1500×1125, **31% brightness**): `#1A140E` near-black; `#966F45` `#C69D65` `#AA8B5C` amber lighting; **`#73848B` slate**
- Frisco (1500×1000, **50% brightness**): `#C6B3A0` cream; `#CEA06D` `#B18F6E` `#94603F` warm woods; **`#6D7B9D` slate blue**

### Conclusions
1. **Gold `#e3b245` is the dominant brand color**, not navy.
2. **The cool axis is slate-blue / teal** (`#108474`, `#566C95`, `#6D7B9D`, `#73848B`) — present in *all three* store photos. NOT navy.
3. **Their spaces are genuinely dark** — 31–50% mean brightness. A dark page is faithful, not a stylistic imposition.
4. Fire imagery = near-black + burnt orange + flame tan. Ember palette confirmed by measurement.

## Typography (real, from font-family declarations)
- `Plaak5Trial45BoldB`, `Plaak6Trial46Bold` — display. ⚠️ **"Trial"** in production = licensing exposure.
- `MonotypeAlbertusNovaBlack` — flared inscriptional serif; carved / hearth character.
- `Interstate` — signage sans.
- `trade-gothic-next` — condensed workhorse.
- `Assistant` — Shopify fallback.

## The story arc — already theirs
`/pages/our-story` is structured in three named acts:

> ### A SPARK. → WILDFIRE. → THE AFTERGLOW.

A fire's full lifecycle. This is the scroll structure, pre-written by the client.

## Verbatim copy worth keeping
- og:title — "Summer Moon | Texas' Original Oak Roasted Coffee"
- "Time Honored Traditions"
- "It was a spark of Texas pioneer spirit that led to the oak roasted coffee that is Summer Moon."
- **"always better, never bitter"** ← the tagline
- **"The formulation of Moon Milk is a story of midnight alchemy. Under a summer moon, late into the night, we landed on our legendary creamer."**
- "That's the magic of moon milk."
- "There's a natural affinity between a wood fire and coffee beans."
- "We drew up the plans, laid every brick by hand"
- "Our team of roasters use sight, sound, and smell"
- **"THE MOON IS CLOSER THAN YOU THINK"** ← location headline
- "FROM OUR HANDBUILT ROASTERS TO YOU"
- "atmospheres that inspire the warmth of cozy evenings under a summer moon"
- **"FIND YOUR SWEET SPOT"** ← Moon Milk CTA = the ratio, already named
- "Our Standard Goes Beyond Coffee"
- Founded by "a closely-knit family in the Texas Hill Country"

## Trademark constraint
**Moon Milk® is a registered trademark.** Footer: "Logo, Moon Milk, and Related
Marks are Registered Trademarks of Summer Moon Coffee." Must carry ®.

## Product line = a complete fire lexicon
Velvet Blaze (balanced house blend) · Inferno (toasted dark, hint of smoke) ·
Afterglow · Billowing · Blue Blazes · En Fuego · Fire Light · Fireside ·
Glowing Ember · Spark · Sweet Hearth · Swinging Lantern
Seasonal: **Beach Fire** (Brew of the Month, August 2026)

Every single product is named for a state of fire. The brand's own naming
system is the creative direction.

## Social
- Primary: `@summermooncoffee`
- Secondary: `SIPSUMMERMOON`
- **Brand hashtag: `#COFFEEUNPLUGGED`**
- Homepage has a `#COFFEEUNPLUGGED` block — but it is a plain link, no embedded feed.

## Information architecture
- **Shop** — Our Coffee, Top Sellers, Bundles, Dark, Medium, Light, Pods, Cold Brew, Origin, Decaf, Merch, Gifts, Subscribe
- **Locations**
- **Contact** — Contact Us, Franchise Inquiry, FAQs, Order Ahead
- **About Us** — Our Story, Brew Guides, Meet The Makers, Coffee Shop Menu
- Cart · Log in

## Flagship locations (on homepage)
- South Austin — 3115 S 1st St #1b, Austin TX 78704
- North Austin — 11005 Burnet Rd #112, Austin TX 78758
- San Antonio — 11831 Culebra Rd #106, San Antonio TX 78253
- Dallas-area — 6943 Main St, Frisco TX 75034
- 70+ locations total.

## Diagnosis
The homepage opens with **three stacked promo bars** (FIRSTBREW code, Beach Fire
brew of the month, free tumbler) then "Brew of the Month" and "New arrivals /
summer merch" tiles. First real brand statement is "OAK ROASTED COFFEE BEANS /
FROM OUR HANDBUILT ROASTERS TO YOU" — below the merchandising.

Their best writing — "midnight alchemy," "A SPARK," "always better, never
bitter" — is two clicks deep on /pages/about and /pages/our-story.

**The homepage is a coupon. The story is in the basement.**

## Instagram — partial, via user screenshot
Confirmed from a Google SERP screenshot supplied by the user:
- **@summermooncoffee — 59.3K+ followers.** Bio: "Official Summer Moon Coffee
  Account Celebrating 24 Years Founded in Austin, TX Oak Roasted Coffee + Moon Milk"
- **@summermoonfrisco — 9.7K+.** "Oak Roasted Coffee + Moon Milk in Frisco, TX!
  Rail District | 6943 W Main St. AND 1377 Legacy Drive Ste. 100" → **two Frisco locations**
- **@summermoonfortworth — 8.2K+.** "Our Summer Moon Coffee **Trailer** offers an
  espresso bar, Cold Brew, Nitro Cold Brew, and Drip coffee to keep your guests
  dancing all night long" → **mobile/events catering arm, previously unknown**

Per-location accounts have real followings (8–10K each). The brand is a
federation of local accounts, not one national feed.

### Still missing: the actual grid imagery
Follower counts and bios are text. What remains unobtained is the **visual
language** — grading, brightness, whether social matches the dark/amber
31–50%-brightness store photography or runs bright and commercial.

## METHOD BOUNDARY (important for future runs)
The Higgsfield sandbox has internet but a datacenter IP. Results split cleanly:

| Source | Sandbox | Notes |
|---|---|---|
| Brand's own Shopify site | ✅ works | full HTML/CSS/images; palettes measurable via ImageMagick |
| Instagram profile | ❌ HTTP 429 | |
| IG web_profile_info API | ❌ HTTP 400 | Meta schema error |
| IG /embed/ | ❌ empty | 607KB JS shell, no captions/alts/urls |
| Playwright | ❌ absent | not installed, node or python |
| Bing Images | ❌ junk | returned unrelated SKF V-belt product shots |
| Google Images | ❌ shell | 92KB, zero extractable image URLs |
| DuckDuckGo HTML | ❌ HTTP 202 | bot check |

**Conclusion: use the sandbox for first-party sites only. Route search engines
and social platforms through the user's own browser via screenshot — a real
browser with a residential IP and logged-in session succeeds instantly where
automation fails.** Ask for those screenshots up front rather than after
exhausting automated routes.
