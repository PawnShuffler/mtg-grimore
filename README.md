# MTG Grimoire

A zero-dependency, single-file browser utility for Magic: The Gathering decklist management powered by the Scryfall API. Enrich card entries with prices, types, and oracle text, extract decklists from raw prose, and find trade intersections against bulk collections.

[![Scryfall API](https://img.shields.io/badge/Powered%20by-Scryfall%20API-eb6f25)](https://scryfall.com/docs/api)
[![Tech](https://img.shields.io/badge/Stack-Vanilla%20HTML%2FCSS%2FJS-blue)]()
[![Deploy](https://img.shields.io/badge/Deployment-GitHub%20Pages-success)]()

---

## Features

### 1. Grimoire Enrichment
* **Batch Scryfall Lookups:** Queries card sets, collector numbers, or names using Scryfall's `/cards/collection` endpoint in optimized batches of 75 items.
* **Special Printings & Flavor Names Fallback:** Automatically resolves Universes Beyond, Secret Lair, and special printing skin names (e.g. *Black Panther's Claws* → *Hammer of Nazahn*, *Godzilla*, *Dracula* series). When Scryfall's bulk collection endpoint misses a flavor name, the engine executes a targeted single-card fallback via `/cards/named` to recover the canonical Oracle card identity, collector number, and market price.
* **Rich Metadata:** Formats entries with collector number, mana cost, card types, oracle rules text (fully supporting MDFC / split cards), and market pricing (USD/foil/etched).
* **Sorting Modes:** Sort generated outputs by original input order, card name, market price, converted mana cost (CMC), or card type.
* **Multi-File Upload & Export:** Select and upload multiple `.txt`, `.csv`, or `.dec` files at once to instantly merge them. Export or copy enriched lists with a single click.
* **Mobile-Responsive UI:** Fully fluid and touch-friendly interface for managing your collection on the go.

### 2. Text-to-Grimoire Extraction
* **Prose Scanning:** Extracts card names, quantities, and set codes embedded inside raw paragraphs, forum posts, or AI/LLM deck write-ups.
* **Regex Fallbacks & Header Skips:** Captures full standard entries (`1 Jet, Freedom Fighter (TLA) 229`), set-only lines (`1 Sol Ring (C19)`), basic lands, and loose card names without set identifiers, while intelligently ignoring conversational fluff and CSV header rows.
* **Dual Output Formats:** Output immediately as a sanitized plain decklist or pipe directly into Scryfall batch enrichment.

### 3. List Comparison (Bulk & Want List Intersection)
* **Binder Matching:** Compares a want list (List A) against a binder or friend's bulk export (List B) to isolate matching cards and automatically cap quantities to what's available.
* **Robust Multi-Format Parsing:** Recognizes standard text lists, `.dec` files, MTG Arena exports, and directly parses native CSV exports from **ManaBox**, **Moxfield**, and **Deckbox**.
* **Value Calculation:** Aggregates matching card counts, resolved quantities, and estimated total financial value using real-time Scryfall market data.

### 4. Diff Precon (Upgrade Tracker)
* **Precon Upgrade Analysis:** Paste your modified decklist and instantly compare it against the original preconstructed deck to see exactly which cards you cut and which ones you added.
* **Live MTGJSON Integration:** Search and fetch the official decklist for every Commander, Brawl, and Challenger precon ever printed using a native, searchable dropdown powered by MTGJSON—no third-party proxies or backend required.
* **Set-Agnostic Matching:** Intelligently ignores set codes and collector numbers during the comparison, so upgrading a basic land or swapping a card's art version won't falsely flag as a "cut" and "addition."

### 5. Wanted List & What's Missing (.xlsx & PDF)
* **What's Missing Calculator:** Paste a list of cards you want (e.g. a deck you are building) and optionally paste a list of cards you already own. The app automatically subtracts your owned cards and calculates exactly what you still need to acquire.
* **Visual Shopping List:** Instantly preview your missing cards in a visual grid with direct Scryfall card links.
* **Interactive Card Deletion:** Remove individual cards directly from the generated preview grid using the `×` button to fine-tune your list prior to generating exports.
* **Copy Plaintext Names:** One-click copy of missing card names as plaintext without quantities or prices, perfect for pasting into trade forums or card stores.
* **Direct Image Copying:** Copy a compiled grid of card images directly to your OS clipboard to paste into Discord, Notion, or MS Word. 
* **Native Excel Export:** Generates a zero-dependency `.xlsx` file entirely in the browser. The spreadsheet includes embedded physical card art (dynamically sized), quantities, Scryfall links, and interactive Yes/No dropdowns to track your shopping progress.
* **Printable PDF:** Generates a print-ready PDF in the browser with 3×3 cards per page at real card size (63×88 mm), card names above each image, and a plain white background to save ink. Supports A4 and US Letter (Letter scales cards down slightly to fit). Scryfall JPEGs are embedded as-is, so they keep their full quality.

### 6. Collection Codex (CSV Ingestion & Analytics)
* **ManaBox / Moxfield / Deckbox CSV Parsing:** Ingests complete collection backups and tracks exact printings using Scryfall IDs, quantities, foil statuses, and purchase prices.
* **Interactive Analytics:** Generates real-time color pie donuts, top sets volume histograms, non-land mana curves, and "The Vault" (top 5 most valuable cards).
* **Search & Sortable Database:** Browse your collection via a paginated table view or visual card grid with real-time text search, rarity, color pip filters, and column sorting.

### 7. Land Station (Commander Land Base Explorer)
* **Targeted Land Base Generator:** Dynamic Scryfall questionnaire tailored for Commander deck building with golden attire styling.
* **Color Identity Mapping:** Select individual mana colors (W, U, B, R, G, C) or choose from standard Guild, Shard, and Wedge presets, mapped directly to Scryfall's `ci<=` syntax.
* **Color Match Mode (Commander Legality vs. Strict Match):** Toggle between searching *Any Selected Colors* (allows 2-color duals, triomes, and rainbow lands legal in the identity) and *Must Produce ALL Selected* (`produces>=`), which returns only lands capable of tapping for all selected colors simultaneously (e.g. 5-color rainbow lands or Esper tri-lands, completely excluding 2-color duals).
* **Speed & ETB Condition Toggles:** Filter by Always Untapped (painlands, filterlands, horizons, duals), Conditional Untapped (shocklands, fastlands, checklands, slowlands, bondlands), and Always Tapped (triomes, bouncelands, scrylands). When searching 3+ colors in strict mode, ETB clauses dynamically adapt to prevent cycle collisions.
* **Cycle-Specific Overrides:** Checkbox controls for individual land cycles (Fetchlands, Shocklands, Painlands, etc.) with smart on-color basic land type matching for fetches.
* **Budget & Live In-Browser Filtering:** Pre-filter with `usd<1`, `usd<5`, `usd<10`, or `usd<20`, then fine-tune results post-fetch with a client-side max price slider, text search, speed selector, sort dropdown, and a live "Produce All Selected" checkbox.
* **Seamless Export:** One-click "+Want" integration with Tab 5 (Wanted List), clipboard decklist copying, and live Scryfall query generation.

### 8. Resilient Networking & Debugging
* **IndexedDB Multi-Alias Caching:** Fast 7-day client-side cache storing cards under canonical name, flavor/alternate names, set/collector numbers, and UUIDs.
* **Rate-Limit Safe:** Automatic delay between batches and exponential backoff retry on HTTP 429 or 5xx responses.
* **Session Logs:** Downloadable in-memory operation logs (`Grimoire_Logs.txt`) capturing batch requests, HTTP status codes, resolution fallbacks, and unparsed lines.

---

## Supported Input Formats

The parser automatically detects and supports standard MTG formats, delimited lines, and various collection manager exports:

```text
# Standard format with set code and collector number
1 Kitsune, Dragon's Daughter (TMT) 41

# Set code without collector number
1 Black Panther's Claws (MSC)

# Basic lands
12 Plains

# Split / MDFC Cards
1 Woodwork Prodigy // Soul Tether (FRA) 165

# Alternate / Universes Beyond / Secret Lair flavor names
1 Black Panther's Claws
1 Black Panther's Claws [Hammer of Nazahn]

# Loose card names
1 Sol Ring

# Embedded prose
"The deck relies on 1 Jet, Freedom Fighter (TLA) 229 to win."

# Native CSV Exports (ManaBox, Moxfield, Deckbox)
Name,Set code,Set name,Collector number,Foil,Rarity,Quantity,...
Extinguisher Battleship,EOE,Edge of Eternities,242,normal,rare,1,...
```
