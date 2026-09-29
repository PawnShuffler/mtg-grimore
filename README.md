# MTG Grimoire

A zero-dependency, single-file browser utility for Magic: The Gathering decklist management powered by the Scryfall API. Enrich card entries with prices, types, and oracle text, extract decklists from raw prose, and find trade intersections against bulk collections.

[![Scryfall API](https://img.shields.io/badge/Powered%20by-Scryfall%20API-eb6f25)](https://scryfall.com/docs/api)
[![Tech](https://img.shields.io/badge/Stack-Vanilla%20HTML%2FCSS%2FJS-blue)]()
[![Deploy](https://img.shields.io/badge/Deployment-GitHub%20Pages-success)]()

---

## Features

### 1. Grimoire Enrichment
* **Batch Scryfall Lookups:** Queries card sets, collector numbers, or names using Scryfall's `/cards/collection` endpoint in optimized batches of 75 items.
* **Rich Metadata:** Formats entries with collector number, mana cost, card types, oracle rules text (fully supporting MDFC / split cards), and market pricing (USD/foil/etched).
* **Sorting Modes:** Sort generated outputs by original input order, card name, market price, converted mana cost (CMC), or card type.
* **Multi-File Upload & Export:** Select and upload multiple `.txt`, `.csv`, or `.dec` files at once to instantly merge them. Export or copy enriched lists with a single click.
* **Mobile-Responsive UI:** Fully fluid and touch-friendly interface for managing your collection on the go.

### 2. Text-to-Grimoire Extraction
* **Prose Scanning:** Extracts card names, quantities, and set codes embedded inside raw paragraphs, forum posts, or AI/LLM deck write-ups.
* **Regex Fallbacks & Header Skips:** Captures full standard entries (`1 Jet, Freedom Fighter (TLA) 229`), basic lands, and loose card names without set identifiers, while intelligently ignoring conversational fluff and CSV header rows.
* **Dual Output Formats:** Output immediately as a sanitized plain decklist or pipe directly into Scryfall batch enrichment.

### 3. List Comparison (Bulk & Want List Intersection)
* **Binder Matching:** Compares a want list (List A) against a binder or friend's bulk export (List B) to isolate matching cards and automatically cap quantities to what's available.
* **Robust Multi-Format Parsing:** Recognizes standard text lists, `.dec` files, MTG Arena exports, and directly parses native CSV exports from **ManaBox**, **Moxfield**, and **Deckbox**.
* **Value Calculation:** Aggregates matching card counts, resolved quantities, and estimated total financial value using real-time Scryfall market data.

### 4. Resilient Networking & Debugging
* **Rate-Limit Safe:** Automatic 500ms delay between batches and exponential backoff retry on HTTP 429 or 5xx responses.
* **Session Logs:** Downloadable in-memory operation logs (`Grimoire_Logs.txt`) capturing batch requests, HTTP status codes, and unparsed lines.

---

## Supported Input Formats

The parser automatically detects and supports standard MTG formats, delimited lines, and various collection manager exports:

```text
# Standard format with set code and collector number
1 Kitsune, Dragon's Daughter (TMT) 41

# Basic lands
12 Plains

# Split / MDFC Cards
1 Woodwork Prodigy // Soul Tether (FRA) 165

# Loose card names
1 Sol Ring

# Embedded prose
"The deck relies on 1 Jet, Freedom Fighter (TLA) 229 to win."

# Native CSV Exports (ManaBox, Moxfield, Deckbox)
Name,Set code,Set name,Collector number,Foil,Rarity,Quantity,...
Extinguisher Battleship,EOE,Edge of Eternities,242,normal,rare,1,...
```
