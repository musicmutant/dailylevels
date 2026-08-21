# Daily options chain

Per-strike options chain data for the products tracked by the Blahtech GL
pipeline. Regenerated each trading day.

## Layout

    index.json              manifest: latest date, products, generated time
    latest/<PID>.json       most recent chain per product (stable URL)
    <YYYY-MM-DD>/<PID>.json dated archive

Stable raw URL pattern:

    https://raw.githubusercontent.com/musicmutant/dailylevels/main/chain/latest/CL.json

## Product IDs

    ES, NQ  index futures
    GC, HG, SI  metals
    CL  crude
    DY  DAX

## Schema

Each file is a JSON object. Summary fields describe the session; the two chain
arrays carry every strike.

| Field | Meaning |
|---|---|
| `spot` | Underlying future price at scrape time |
| `atm_iv` | At-the-money implied volatility, percent |
| `dte` | Days to expiry for the quoted series |
| `call_oi_total` / `put_oi_total` | Summed open interest |
| `pc_ratio` | Put/call open-interest ratio |
| `gamma_flip` | Gamma flip level |
| `gamma_env` | `POSITIVE` or `NEGATIVE` gamma environment |
| `net_gex_at_spot` | Net gamma exposure at spot |
| `bias` | `BULLISH`, `BEARISH`, or `NEUTRAL` |
| `call_gamma_wall` / `put_gamma_wall` | Dominant gamma walls |
| `chop_hi` / `chop_lo` | Expected chop band |
| `iv_trend` | Direction and delta vs prior session |
| `full_chain_calls` | Every call strike |
| `full_chain_puts` | Every put strike |
| `top_calls` / `top_puts` | Five highest-weighted levels, with `wt` and `type` |

Chain entries are objects of:

    {"strike": 6.5, "oi": 618, "iv": 19.1, "gamma": 2.323491,
     "gex": 35897935.95, "oi_iv": 11807.54}

`iv` is percent. `gex` is gamma exposure. `oi_iv` is open interest times IV,
the weighting input used to rank levels.

## Notes

Derived analytics computed from public options quotes. Provided as-is for
research and educational use, with no warranty of accuracy, timeliness, or
completeness. Nothing here is a trade recommendation.
