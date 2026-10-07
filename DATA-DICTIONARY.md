# AI Visibility Index for Trading Brands: data dictionary

One file per edition: `data/{edition}/ai-visibility-index-{edition}.csv`. UTF-8, comma separated, header on the first line, one row per edition, category, market, source and brand. Seventeen columns.

Definitions below are taken from the scoring code that produced the file (method v1.1), not written from memory.

## Columns

| # | Column | Type | What it means |
|---|---|---|---|
| 1 | `period` | text | The edition, for example `2026-Q3`. |
| 2 | `category` | text | `forex` (forex and CFD brokers), `prop` (prop trading firms) or `crypto` (crypto exchanges). |
| 3 | `geo` | text | The market. A two-letter country code (`GB`, `NG`, `MY`), a region (`EUROPE`, `LATAM`), or `all` for every market in the edition combined. |
| 4 | `engine` | text | Where the answer came from. See the source list below. `all` combines every source. |
| 5 | `brand` | text | Brand name after alias matching, so one company is counted once. |
| 6 | `brand_slug` | text | Stable brand ID. Matches the brand page `https://pipswire.com/intelligence/brands/{slug}/`. |
| 7 | `visibility` | number, 0 to 100 | The AI Visibility Score. `100 × (0.40 × mention_rate + 0.30 × rec_rate × position_score + 0.15 × sentiment_score + 0.15 × own_cite_rate)`, rounded to one decimal. |
| 8 | `mention_rate` | number, 0 to 1 | Share of answers that name the brand. Only answers to questions that name no brand count here. |
| 9 | `rec_rate` | number, 0 to 1 | Share of those same answers that recommend the brand, not just mention it. |
| 10 | `position_score` | number, 0 to 1 | How high the brand sits when it is recommended. In a list: `1 − (position − 1) ÷ max(list length, 5)`, so first place is 1. A recommendation in plain text with no list counts as 0.6. Averaged over the answers that recommend the brand. |
| 11 | `sentiment_score` | number, 0 to 1 | How the brand is described, averaged over every answer that names it (including questions that name the brand). Positive 1.0, neutral 0.6, caution 0.3, negative 0. |
| 12 | `own_cite_rate` | number, 0 to 1 | Share of the answers that name the brand in which the source cites the brand's own website. |
| 13 | `share_of_voice` | number, 0 to 1 | The brand's mentions divided by all brand mentions in the same category, market and source. |
| 14 | `n` | whole number | Answers in this cut to questions that name no brand. The denominator for `mention_rate` and `rec_rate`. The same for every brand in a cut. |
| 15 | `n_mentions` | whole number | How many of those `n` answers name the brand. |
| 16 | `ci_low` | number, 0 to 100 | Low end of the score's range: the score with the mention rate at the low end of its 95% Wilson interval. |
| 17 | `ci_high` | number, 0 to 100 | High end of the score's range, built the same way. A wide range means few answers, not a weak brand. |

## Sources (`engine`)

| Value | Source |
|---|---|
| `openai` | ChatGPT: the OpenAI API with web search |
| `anthropic` | Claude: the Anthropic API with web search |
| `gemini` | Gemini: the Gemini API with Google Search grounding |
| `perplexity` | Perplexity: the Sonar API |
| `google_ai_mode` | Google AI Mode, collected through a search data provider |
| `google_ai_overview` | Google AI Overviews. Only counted when Google showed one, so `n` is small |
| `google_organic` | Google's top 10 standard results for the same question, kept as a baseline |
| `all` | Every source above combined |

## Markets (`geo`) in edition 2026-Q3

`AE` United Arab Emirates, `AU` Australia, `BR` Brazil, `DE` Germany, `GB` United Kingdom, `KE` Kenya, `MX` Mexico, `MY` Malaysia, `NG` Nigeria, `PH` Philippines, `TH` Thailand, `US` United States, `VN` Vietnam, `ZA` South Africa, `EUROPE` (region), `LATAM` (Latin America, region), and `all`.

A market is measured for a product only where residents can legally use it. The United States has prop firm and crypto rows but no forex and CFD broker rows.

## Reading tips

- Use `geo = all` and `engine = all` for the headline table of each category.
- Compare brands only inside the same category, market and source. `n` differs between cuts.
- Treat a cut with `n` below 6 as a rough reading.
- `rec_rate` is close to `mention_rate` for most brands in 2026-Q3. Check the method page before you use them as two separate signals.

Method: https://pipswire.com/intelligence/methodology/ · Corrections: info@pipswire.com
