# Data Guide

(中文版见 数据使用说明.md)

## Layout

```
polymarket-smart-money-data-samples/
  <date>/sample-<date>.csv.zst    fills, zstd-compressed CSV with a header row
  <date>/sample-<date>.json       the sample's manifest
```

Read it with `zstd -d` (or `zstdcat`), or in Python:

```python
import pandas as pd   # needs the zstandard package: pip install zstandard
df = pd.read_csv("sample-2026-10-06.csv.zst", compression="zstd", dtype=str)
```

Read every column as text: `tokenId` is a 77-digit integer and loses precision as a number.

## sample-&lt;date&gt;.csv.zst — fills

Each row is one on-chain `OrderFilled` log, i.e. the fill of one order, and `wallet` is the owner of that order.
Rows are sorted by `block`, `logIndex`, `wallet`.

| column | meaning |
|---|---|
| ts | block time, UTC, `YYYY-MM-DD HH:MM:SS` (to the second, no timezone suffix) |
| block · blockHash | Polygon block of the fill |
| txHash · logIndex | transaction and log position; together they identify the fill on chain |
| exchange | contract that matched the fill (see below) |
| side | direction of this wallet's own order: `BUY` = paid USDC for `tokenId`, `SELL` = sold it |
| role | whether this wallet's order was the `taker` or a `maker` |
| tokenId | outcome token id, as a decimal string |
| price | `usdc / shares`, truncated to at most 6 decimal places |
| shares | outcome tokens filled; non-negative integer at 1e6 precision (divide by 1e6) |
| usdc | USDC paid (`BUY`) or received (`SELL`); non-negative integer at 1e6 precision |
| fee | fee charged on this order, integer at 1e6 precision; `0` = not charged |
| feeUnit | unit of `fee`: `collateral` (USDC) or `shares` |
| wallet | lowercase address that owns the order |
| entityId | the trader the wallet belongs to (one of its wallets' addresses) |
| rank | that trader's rank on the list the file was built from |

### exchange

- `pm_ctf_v2` — Polymarket CTF Exchange (v2), which matches binary markets.
- `pm_negrisk_v2` — Polymarket NegRisk CTF Exchange (v2), which matches multi-outcome (negative-risk) markets.
- `pm_unknown_v2` — contract `0xe3333700ca9d93003f00f0f71f8515005f6c00aa`, deployed 2026-05-26. It emits the same
  `OrderFilled` events as the v2 exchanges but not `OrdersMatched` / `FeeCharged`, and its identity is unconfirmed.
  Its `tokenId` is not a CTF position id and does not map to a market. Its fills are included, but they are not used
  in ranking. They are a small share of rows.

Only these three values occur today. Older exchange contracts are recognised but have produced no rows.

### Taker, makers and fees

- One taker order can match several maker orders, so one match is 1 taker row plus k maker rows. A maker can be on
  the same `tokenId` in the opposite direction (an ordinary trade), or on the complementary `tokenId` in the same
  direction: both `BUY` mints a new position, both `SELL` merges one. No column says which; group by `txHash` to
  rebuild a match.
- A match between two listed traders appears once for each side, in their own rows.
- Fees are charged per order and are paid mostly by takers. Makers are usually `0`, but not always.
- On the current v2 contracts every fee is in USDC (`feeUnit = collateral`). `shares` is kept for older contracts and
  does not occur in current files.

## sample-&lt;date&gt;.json — the sample's manifest

| field | meaning |
|---|---|
| schema | `pmwallets-smart-sample/1` |
| day | the UTC day of the fills |
| ranks | the rank range the sample was drawn from |
| forbiddenTop · forbiddenFrom · forbiddenTo | traders in the top `forbiddenTop` of the rankings in that period are left out |
| dropped | how many traders in `ranks` were left out (not replaced) |
| source | the ranking the list came from: `runId`, the block window `b0`–`b1`, the source daily build |
| trades | the fills: start of the day (`from`), `columns`, and `file` with `name`, `rows`, `bytes`, `sha256` |
| entities | `[{rank, entityId, wallets}]`, including traders with no fills that day |
| note | how this sample differs from the product |

The paid files carry a manifest of their own per list and day, naming the frozen list (rule version, ranking run,
data cut-off), the traders and wallets, and the file's rows, bytes and sha256. If a day's list cannot be built in
time, that day is not published and the manifest says why.
