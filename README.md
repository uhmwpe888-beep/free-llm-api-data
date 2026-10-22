# Free LLM API Data

Machine-readable LLM API pricing and free-tier data — 109 models across 17 providers,
plus all 12 permanent free LLM API tiers with rate limits, quotas and credit-card requirements.

> This data powers [**LLM Cost Hub**](https://llmcosthub.wiki/) — the free LLM API pricing
> calculator and comparison site. If you find the data useful, the site is the live,
> always-current version with cost calculators for every model:
>
> - **All 109 models, sortable with monthly-cost calculator:** <https://llmcosthub.wiki/>
> - **Free LLM API tiers compared (limits, quotas, no-credit-card):** <https://llmcosthub.wiki/free-llm-api/>

## Files

| File | Contents | Verified |
|---|---|---|
| [`data/models.json`](data/models.json) | 109 models: input/output price per 1M tokens, context window, provider, tier, status (current/legacy/preview) | see `"updated"` field |
| [`data/free_tiers.json`](data/free_tiers.json) | 12 permanent free LLM API tiers (rate limit, quota, card required, endpoint, key-guide steps) + 6 trial-credit offers | see `"verified"` field |

## Schema highlights

**models.json** — one entry per model:

```json
{
  "id": "kimi-k3",
  "name": "Kimi K3",
  "provider": "Moonshot AI",
  "input": 2.82,
  "output": 14.08,
  "context": 262144,
  "tier": "frontier",
  "status": "current"
}
```

- Prices are **list prices in USD per 1M tokens** (standard tier, no batch/cache discounts)
- `status`: `current` (actively sold) / `legacy` (superseded, still billable) / `preview`
- A common blended figure is `(3 × input + output) ÷ 4` — see the
  [methodology](https://llmcosthub.wiki/about/)

**free_tiers.json** — one entry per free-tier provider, including the fine print
(`"catch"` field: data-training opt-ins, non-commercial limits, prototyping-only terms).

## Update cadence

Pricing and free-tier limits are re-verified weekly against provider docs and
independent trackers. Data date is embedded in each file — always check it before use.

## Use it

The JSON files are plain UTF-8 JSON — no dependencies:

```python
import json, urllib.request

models = json.load(urllib.request.urlopen(
    "https://raw.githubusercontent.com/<you>/free-llm-api-data/main/data/models.json"))
cheapest = sorted(models["models"], key=lambda m: (3*m["input"]+m["output"]) / 4)[:5]
```

## License

Data released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) —
use it anywhere, just credit **[llmcosthub.wiki](https://llmcosthub.wiki/)** as the source.

## Contributing

Spot a stale price or a changed rate limit? Open an issue or a PR.
Corrections ship to the site in the next weekly update.
