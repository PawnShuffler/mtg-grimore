# MTG Grimoire

A zero-dependency, single-file browser utility for Magic: The Gathering decklist management powered by the Scryfall API. Enrich card entries with prices, types, and oracle text, extract decklists from raw prose, and find trade intersections against bulk collections.

[![Scryfall API](https://img.shields.io/badge/Powered%20by-Scryfall%20API-eb6f25)](https://scryfall.com/docs/api)
[![Tech](https://img.shields.io/badge/Stack-Vanilla%20HTML%2FCSS%2FJS-blue)]()
[![Deploy](https://img.shields.io/badge/Deployment-GitHub%20Pages-success)]()

---

## Features

### 1. Grimoire Enrichment
* **Batch Scryfall Lookups:** Queries card sets, collector numbers, or names using Scryfall's `/cards/collection` endpoint in optimized batches of 75 items.
* **Rich Metadata:** Formats entries with collector number, mana cost, card types, oracle rules text (supporting MDFC / split cards), and market pricing (USD/foil/etched).
* **Sorting Modes:** Sort generated outputs by original input order, card name, market price, converted mana cost (CMC), or card type.
* **File Upload & Export:** Import `.txt`, `.csv`, or `.dec` files directly. Export or copy enriched lists with a single click[cite: 2].

### 2. Text-to-Grimoire Extraction
* **Prose Scanning:** Extracts card names, quantities, and set codes embedded inside raw paragraphs, forum posts, or LLM deck write-ups[cite: 2].
* **Regex Fallbacks:** Captures full standard entries (`1 Jet, Freedom Fighter (TLA) 229`), basic lands, and loose card names without set identifiers[cite: 2].
* **Dual Output Formats:** Output immediately as a sanitized plain decklist or pipe directly into Scryfall batch enrichment[cite: 2].

### 3. List Comparison (Bulk & Want List Intersection)
* **Binder Matching:** Compares a want list (List A) against a binder or friend's bulk export (List B) to isolate matching cards[cite: 2].
* **Multi-Format Parsing:** Recognizes standard text lists, `.dec` files, MTG Arena exports, and Moxfield CSV outputs[cite: 2].
* **Value Calculation:** Aggregates matching card counts, resolved quantities, and estimated total financial value[cite: 2].

### 4. Resilient Networking & Debugging
* **Rate-Limit Safe:** Automatic 500ms delay between batches and exponential backoff retry on HTTP 429 or 5xx responses[cite: 2].
* **Session Logs:** Downloadable in-memory operation logs (`Grimoire_Logs.txt`) capturing batch requests, HTTP status codes, and unparsed lines[cite: 2].

---

## Supported Input Formats

The parser recognizes standard MTG formats, delimited lines, and CSV exports[cite: 2]:

```text
# Standard format with set code and collector number
1 Kitsune, Dragon's Daughter (TMT) 41

# Basic lands
12 Plains

# Loose card names
1 Sol Ring

# Embedded prose
"The deck relies on 1 Jet, Freedom Fighter (TLA) 229 to win."

# Moxfield / Arena CSV exports
1,"Agate Instigator",BLC,46
