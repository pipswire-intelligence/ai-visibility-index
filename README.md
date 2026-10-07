# AI Visibility Index for Trading Brands

When a trader asks an AI assistant "which forex broker should I use?", which brands does it name? This dataset measures that, every quarter.

PipsWire Intelligence asks ChatGPT, Claude, Gemini, Perplexity and Google the questions traders ask about forex and CFD brokers, prop trading firms and crypto exchanges. It then scores every brand the answers name, from 0 to 100, by market and by source.

The index is free, the method is public and the data is open under CC BY 4.0.

| | |
|---|---|
| Publisher | PipsWire Intelligence, the data unit of PipsWire (Catalinq LLC, San Francisco, California) |
| Author | David Ispiryan |
| Live index | https://pipswire.com/intelligence/ |
| Dataset page | https://pipswire.com/intelligence/dataset/ |
| Method | https://pipswire.com/intelligence/methodology/ |
| DOI, all editions | https://doi.org/10.5281/zenodo.23210742 |
| Licence | CC BY 4.0 |
| Updated | Every quarter |

## Editions

| Edition | Published | Method | Brands | Markets | Answers | File |
|---|---|---|---|---|---|---|
| 2026-Q3 | 16 September 2026 | 1.1 | 288 (119 forex and CFD brokers, 76 prop firms, 93 crypto exchanges) | 16 | 7,062 | `data/2026-Q3/ai-visibility-index-2026-Q3.csv` |

"Answers" counts answers to questions that name no brand, across all sources. Each new edition adds a folder and a row here. Old editions never change, except through a dated correction in `CHANGELOG.md`.

## What is in each file

One CSV with 17 columns and one row per edition, category, market, source and brand. Full definitions are in [`DATA-DICTIONARY.md`](DATA-DICTIONARY.md).

- **Score:** `visibility`, from 0 to 100, with a range (`ci_low`, `ci_high`).
- **Parts of the score:** `mention_rate` (40%), `rec_rate` times `position_score` (30%), `sentiment_score` (15%), `own_cite_rate` (15%).
- **Counts:** `n` answers in the cut and `n_mentions` that name the brand, plus `share_of_voice`.
- **Cuts:** `category`, `geo` (market) and `engine` (source). Use `geo = all` and `engine = all` for the headline table.

## How it is measured

- Twelve fixed question templates. Seven name no brand, five name one.
- Each question is asked at least twice, so every score has a range.
- Sources: ChatGPT, Claude, Gemini and Perplexity through their APIs with web search, plus Google AI Mode, Google AI Overviews and Google's top 10 results.
- Brand names are matched with alias lists, so one company counts once.
- A market is measured for a product only where residents can legally use it.

## Three findings from 2026-Q3

1. Two brokers lead by a wide margin. Pepperstone is named in 59% of 2,552 answers about forex and CFD brokers, IC Markets in 48%.
2. AI answers rarely cite the brands' own websites. Among the top six brokers, the best own-site citation rate is 9%.
3. Named most does not mean scored highest. FundedNext is named in 60% of 2,344 prop firm answers and FTMO in 58%, yet FTMO scores higher (47.5 against 45.6), because position, tone and own-site citation also count.

## Cite this data

> PipsWire Intelligence (2026). *AI Visibility Index for Trading Brands* [Data set]. PipsWire, Catalinq LLC. CC BY 4.0. https://doi.org/10.5281/zenodo.23210742

To cite one edition, use its own DOI. Edition 2026-Q3: https://doi.org/10.5281/zenodo.23210743

Short credit for a chart:

> Source: PipsWire AI Visibility Index (pipswire.com/intelligence), CC BY 4.0.

`CITATION.cff` gives the same data to GitHub's "Cite this repository" button.

## Corrections

Write to info@pipswire.com. We answer within five working days and publish every correction with its date in `CHANGELOG.md` and on the live index.

## Disclosure

Catalinq LLC also owns Ranxy, a marketing agency, and BrokerCatalogue and ExchangeCatalogue, two comparison sites. They are labelled wherever they appear and are never scored. Nobody can pay to change a score.

B2B marketing data. Not investment advice, and not a recommendation to trade or to use any broker, exchange or prop firm.
