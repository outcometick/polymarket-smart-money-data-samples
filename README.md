# Polymarket Smart-Money Trade History · Free Sample (Preview)

[Polymarket smart-money trade history](https://outcometick.com/polymarket-smart-money-data) from [OutcomeTick](https://outcometick.com),
built by our partner [PMWallets](https://pmwallets.com): every day, Polymarket traders are ranked on the previous
30 days of settled markets, and the day's on-chain fills of the ones on the list go into one file. This repository
hosts a **free preview sample**: one real UTC day (2026-10-06) of the traders ranked 901 to 1000, in the same file
format as the paid files.

> **中文：** 本仓库是 [OutcomeTick](https://outcometick.com/zh) 的 [Polymarket 聪明钱成交历史](https://outcometick.com/zh/polymarket-smart-money-data)
> 的**免费预览样本**，数据由合作伙伴 [PMWallets](https://pmwallets.com/zh) 生成：每天依据此前 30 天已结算的市场给交易者排名，
> 把上榜者当天的链上成交写进一个文件。样本是一个真实 UTC 日（2026-10-06）里排名第 901 到 1000 名的交易者的成交，文件格式与付费文件一致。

> **Preview, not the final sample.** This file was built before daily lists were frozen, so the list it uses
> already includes the day itself, which the product never does (a day's file always uses the list as of the end of
> the previous UTC day). Traders who ranked 1–900 in any of the three most recent 30-day rankings are left out and
> not replaced, so the file holds 65 traders, not 100. It will be replaced by a fixed three-day sample at launch.
>
> **这是预览，不是正式样本。** 它生成于每日名单冻结之前，所用名单已包含当天本身，正式产品不会这样（某天的文件总是用前一个 UTC 日结束时的名单）。
> 最近三轮 30 天排名中进过前 900 名的交易者已剔除且不补，所以文件里是 65 个交易者而不是 100 个。开售时将由固定的三天样本取代。

## Download / 下载

**[polymarket-smart-money-data-samples.tar.gz](https://github.com/outcometick/polymarket-smart-money-data-samples/releases/latest/download/polymarket-smart-money-data-samples.tar.gz)**

```bash
curl -L https://github.com/outcometick/polymarket-smart-money-data-samples/releases/latest/download/polymarket-smart-money-data-samples.tar.gz | tar xz
```

Sizes and sha256: [`samples/manifest.json`](samples/manifest.json).
Field reference: [DATA_GUIDE.md](DATA_GUIDE.md) · 中文字段说明：[数据使用说明.md](数据使用说明.md)

## Files in this sample / 样本包含的文件

| path | contents |
|---|---|
| `2026-10-06/sample-2026-10-06.csv.zst` | 30,861 fills by 65 traders (107 wallets), zstd-compressed CSV with a header row |
| `2026-10-06/sample-2026-10-06.json` | the sample's manifest: the ranking it was built from, its traders and their wallets |

## How the list is chosen / 名单怎么选

- The ranking window is the 30 days ending at the previous UTC midnight.
- A trader qualifies with a trade in the window, at least 10 settled markets won or lost, at least $1,000 bought,
  and a realized profit that stays positive after their single most profitable market is removed.
- Qualifiers are ranked by that remaining profit. This reduces the weight of one lucky bet; it does not detect
  wash trading.
- Wallets that can be shown to belong together are ranked as one trader. Separate wallets run by one person are
  not merged.

> **中文：** 窗口是截至前一个 UTC 日结束的 30 天。入选条件：窗口内有成交、至少 10 个分出胜负的已结算市场、买入额至少 $1,000，
> 且去掉其最赚钱的单个市场后已实现利润仍为正。按剩余利润排名，这能减少单笔运气的影响，但不能识别对倒。
> 能证明属于同一交易者的钱包合并排名；同一个人控制的多个独立钱包不会被合并。

## Learn more / 了解更多

- [Polymarket smart-money trade history](https://outcometick.com/polymarket-smart-money-data) — the product page · [中文](https://outcometick.com/zh/polymarket-smart-money-data)
- [OutcomeTick](https://outcometick.com) — prediction-market data for Polymarket and Predict.fun · [中文站](https://outcometick.com/zh)
- [PMWallets](https://pmwallets.com) — our partner's smart-money leaderboard, where you can pick individual wallets and date ranges

For research only; not investment advice. / 仅供研究，不构成投资建议。
