# Carbon Atlas - Session Brief

---

## What this project is

Carbon Atlas is a carbon pricing jurisdiction intelligence platform. It covers the world's major emissions trading systems and carbon taxes - showing where schemes exist, what they cover, what they cost, and when compliance deadlines fall.

It is a reference resource with commercial ambitions. The audience is corporate sustainability teams, consultants, policy researchers, and journalists who need a clean, reliable overview of the global carbon pricing landscape. The Who's Who section is designed to be "boast-worthy" - making the site sticky through recognition of real practitioners, driving sharing and word-of-mouth within the carbon pricing community.

The site is a sister project to Canopy (canopy-acx.pages.dev). It shares the same design language - white background, system font stack, same card grid, same nav pattern, same detail panel approach - with blue as the primary colour instead of green.

---

## Session Rules

- Files always download to ~/Downloads/. Always provide bash copy commands using `"$(ls -t ~/Downloads/filename*.ext | head -1)"` with quotes around the subshell to handle Mac space-in-filename convention.
- Always show a plan before building. Never start without it.
- Always ask for confirmation after showing the plan. Wait for go-ahead.
- All text must not look AI-written. No em-dashes - use regular hyphens. No apostrophes in JSON summary fields.
- Add to brief when asked. Never present as download unless asked.
- Always give the brief as a .MD file for download.
- When asked for bash code, respond with just the code block. No preamble.
- Do not push to git during development. Push only when session work is complete and confirmed.
- When needing a file from the local repo, give bash code to copy it to Downloads, then wait for upload.
- Always give URLs as clickable hyperlinks.
- When asked to add a rule, add it to the brief. Do not present the revised brief unless asked.
- Never ask two questions at the same time.
- All homepage cards must be fixed at 340px height, overflow hidden. Never use min-height on homepage cards.

---

## Hosting and repo

- **GitHub:** https://github.com/ralphlazar/carbonatlas
- **Live site:** https://carbonatlas.pages.dev
- **Hosting:** Cloudflare Pages, auto-deploys on push to master branch
- **Local repo:** /Users/lisaswerling/RALPH/AI/carbonatlas
- **Branch:** master

### Deploy pattern

```bash
cp "$(ls -t ~/Downloads/index*.html | head -1)" /Users/lisaswerling/RALPH/AI/carbonatlas/index.html
cp "$(ls -t ~/Downloads/map*.html | head -1)" /Users/lisaswerling/RALPH/AI/carbonatlas/map.html
cp "$(ls -t ~/Downloads/schemes*.html | head -1)" /Users/lisaswerling/RALPH/AI/carbonatlas/schemes.html
cp "$(ls -t ~/Downloads/prices*.html | head -1)" /Users/lisaswerling/RALPH/AI/carbonatlas/prices.html
cp "$(ls -t ~/Downloads/timeline*.html | head -1)" /Users/lisaswerling/RALPH/AI/carbonatlas/timeline.html
cp "$(ls -t ~/Downloads/whoswho*.html | head -1)" /Users/lisaswerling/RALPH/AI/carbonatlas/whoswho.html
cd /Users/lisaswerling/RALPH/AI/carbonatlas && git add -A && git commit -m '...' && git push
```

---

## File structure

| File | Contents |
|---|---|
| `index.html` | Homepage - 5 cards: jurisdiction map, compliance calendar, prices, timeline, who's who |
| `map.html` | Full interactive map (Map/List toggle) - 30 schemes, D3 world map, detail panel |
| `calendar.html` | Full compliance calendar - 18 events, grouped by month, filterable by scheme |
| `schemes.html` | Full scheme index - all 30 schemes, filterable by type, detail panel |
| `prices.html` | Price listing - all 27 active schemes grouped by ETS/tax, detail panel |
| `timeline.html` | Interactive SVG timeline + chronological card grid grouped by decade |
| `whoswho.html` | Who's Who - 7 verified profiles of current and recent carbon pricing practitioners |

No build script. No JSON data files - all data is baked into each HTML file as JS objects.

---

## Design system

Lifted directly from Canopy. Key variables:

```css
--bg: #ffffff; --bg2: #fafaf8; --bg3: #f5f5f2;
--border: #e8e8e5;
--blue: #1a3a5c; --blue-pale: #e0eaf5; --blue-mid: #2a5c8a;
--teal: #1a5c5c;
--text: #1a1a18; --text-muted: #5f5e5a; --text-dim: #999896;
--ets-bg: #e0eaf5; --ets-text: #1a3a5c;
--tax-bg: #faeeda; --tax-text: #633806;
--map-ets: #1a3a5c; --map-tax: #b06a00; --map-partial: #4a7fb5; --map-none: #d8d6d0;
```

Logo mark: globe SVG (circle + meridian ellipse + equator line) in white on `--blue` background, 30x30px, border-radius 7px.

Homepage grid: 2 columns desktop, 1 column mobile. All cards fixed at 340px height, overflow hidden.

### Homepage card colours

| Card | Content | Colour |
|---|---|---|
| 1 | Jurisdiction Map | rgba(26,58,92,...) dark blue |
| 2 | Compliance Calendar | rgba(42,92,138,...) mid blue |
| 3 | Prices | rgba(26,90,60,...) blue-green |
| 4 | Timeline | rgba(90,60,20,...) warm amber |
| 5 | Who's Who | rgba(26,92,92,...) teal |

Card numbers: #1a3a5c, #2a5c8a, #1a5a3c, #5a3c14, #1a5c5c

Detail panel: slides in from right, 440px wide, dark overlay behind.

---

## Data - 30 schemes tracked

### Active (27)

| ID | Name | Type | Price | Jurisdiction |
|---|---|---|---|---|
| EU-ETS | EU ETS | ETS | ~EUR 64/t | 27 EU members + Norway, Iceland, Liechtenstein |
| UK-ETS | UK ETS | ETS | ~GBP 44/t | United Kingdom |
| CCA | CCA | ETS | ~USD 30/t | California (linked to Quebec) |
| RGGI | RGGI | ETS | ~USD 14/t | 11 northeastern US states |
| CA-OBPS | Canada | ETS | ~CAD 95/t | Canada (federal backstop) |
| CN-ETS | China ETS | ETS | ~CNY 90/t | China |
| NZ-ETS | NZ ETS | ETS | ~NZD 52/t | New Zealand |
| AU-SM | Australia | ETS | ~AUD 33/t | Australia |
| KR-ETS | Korea ETS | ETS | ~KRW 9,800/t | South Korea |
| SG-CT | Singapore | Tax | SGD 25/t | Singapore |
| JP-GX | Japan GX-ETS | ETS | ~JPY 750/t | Japan |
| CH-ETS | Switzerland ETS | ETS | ~EUR 64/t | Switzerland |
| CO-CT | Colombia | Tax | ~COP 25,000/t | Colombia |
| CL-CT | Chile | Tax | USD 5/t | Chile |
| ZA-CT | South Africa | Tax | ~ZAR 190/t | South Africa |
| MX-ETS | Mexico ETS | ETS | ~MXN 200/t | Mexico |
| KZ-ETS | Kazakhstan ETS | ETS | ~KZT 500/t | Kazakhstan |
| ID-ETS | Indonesia ETS | ETS | ~IDR 30,000/t | Indonesia |
| TW-ETS | Taiwan ETS | ETS | ~TWD 300/t | Taiwan |
| IL-CT | Israel | Tax | ~ILS 60/t | Israel |
| AR-CT | Argentina | Tax | ~USD 6/t | Argentina |
| SE-CT | Sweden | Tax | ~SEK 1,340/t | Sweden |
| NO-CT | Norway | Tax | ~NOK 952/t | Norway |
| BC-CT | BC Carbon Tax | Tax | ~CAD 95/t | British Columbia, Canada |
| AB-TIER | Alberta TIER | ETS | ~CAD 95/t | Alberta, Canada |
| QC-CaT | Quebec C&T | ETS | ~CAD 30/t | Quebec, Canada |
| WA-CI | Washington CCI | ETS | ~USD 55/t | Washington State, USA |

### In development (3)

| ID | Name | Type | Status |
|---|---|---|---|
| UA-ETS | Ukraine ETS | ETS | Pilot from 2026; subject to end of martial law |
| TR-ETS | Turkey ETS | ETS | Climate Law July 2025; pilot planned 2026-2027 |
| BR-ETS | Brazil SBCE | ETS | Law Dec 2024; full compliance ~2030 |

US (840) treated as partial/sub-national - coloured separately on map.

### Map colouring notes
- Sweden and Norway already coloured via EU ETS isos (752, 578) - their carbon taxes show in scheme list only
- BC, Alberta, Quebec, Washington sub-national within already-coloured countries
- Development schemes not coloured on map

---

## Who's Who - 7 verified profiles

Curation model: editorial selection of verified, documented contributors to major schemes. Start editorially, expand carefully. Outreach approach: notify people they've been included - do not ask permission first. Do slowly and carefully.

Revenue potential: premium placement, verified badges, event partnerships, direct outreach to firms wanting to reach this audience.

### Current profiles

| Name | Role | Scheme |
|---|---|---|
| Wopke Hoekstra | Commissioner for Climate, Net Zero and Clean Growth - European Commission | EU ETS |
| Christiana Figueres | Former Executive Secretary (2010-2016) - UNFCCC | Paris Agreement |
| Jos Delbeke | Former DG CLIMA Director-General (2010-2018); EIB Chair at EUI Florence | EU ETS |
| Connie Hedegaard | Former EU Commissioner for Climate Action (2010-2014); OECD Round Table Chair | EU ETS |
| Mary Nichols | Former CARB Chair (2007-2020) | CCA |
| Lauren Sanchez | Chair - California Air Resources Board | CCA |
| Dirk Forrister | President and CEO - IETA | Global |

**Design notes:** Cards use initials avatar (dark navy circle), name, role, organisation, scheme badge, 2-sentence bio, link to official source. No detail panel - the card is the profile. Editorial note on page explains curation criteria.

---

## Page structure and navigation

All pages share the same mobile hamburger nav. Full nav includes:
Home | Jurisdiction Map | Compliance Calendar | Scheme Index | Prices | Timeline | Who's Who

Map page: has Map/List toggle. Map view is default. List view shows all 30 schemes with filter chips. No separate list page - the list lives within map.html.

Schemes page: separate from map list view. Has summary stat bar, type filters, arrow column.

Prices page: active schemes only (27), grouped ETS then Carbon Tax. Methodology note at top.

Timeline page: SVG timeline (ETS above axis blue, tax below amber, clickable dots) + chronological card grid by decade.

---

## Homepage layout (5 cards, 2-col grid)

Row 1: Map (card 1) | Calendar (card 2)
Row 2: Prices (card 3) | Timeline (card 4)
Row 3: Who's Who (card 5) | [empty slot for future card]

Card 5 shows 3 name previews (Hoekstra, Figueres, Delbeke) + "+ 4 more profiles" - no longer locked.

---

## Update cadence

- **Prices:** monthly. Approximate indications only.
- **Calendar:** update when regulators confirm new dates, roughly 4-5 times per year.
- **Scheme detail:** update when schemes reform - handful of times per year.
- **Who's Who:** add profiles slowly and carefully. Verify everything before publishing.
- **In-development schemes:** update status as pilot launches or laws progress.

Total maintenance: approximately 30-45 minutes per month once stable.

---

## On the horizon

- Custom domain (name decision still deferred)
- Who's Who expansion - research and verify more profiles before adding. Priority: UK ETS official, NZ ETS, Korea ETS, one from World Bank carbon pricing team
- Who's Who outreach strategy - notify people they're included. Very slowly, one at a time, only once the section looks authoritative
- Revenue paths: premium placement, verified badges, event partnerships, direct outreach
- Price history charts in scheme detail panels
- Map improvements - click-to-zoom
- Data files (JSON) - currently baked into HTML; extract when update cadence makes it worth it
- Historical "Thinkers" section (Nordhaus, Sandor, Delbeke, etc.) - pocketed as future editorial feature
- Sectors page - deferred; may be a rich card rather than a full page
- Calendar.html nav not yet updated to include Prices/Timeline/Who's Who (file not edited this session)
