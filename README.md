# Polymarket Smart-Money Trade History · Free Sample

[Polymarket smart-money trade history](https://outcometick.com/polymarket-smart-money-data) from [OutcomeTick](https://outcometick.com),
built by our partner [PMWallets](https://pmwallets.com): every day, Polymarket traders are ranked on the previous
30 days of settled markets, and the day's on-chain fills of the ones on the list go into one file. This repository
hosts a **free sample**: three real UTC days (2026-10-08 to 2026-10-10), each holding that day's fills by the traders
ranked 901 to 1000 on that day's frozen list, in the same file format as the paid files.

> **中文：** 本仓库是 [OutcomeTick](https://outcometick.com/zh) 的 [Polymarket 聪明钱成交历史](https://outcometick.com/zh/polymarket-smart-money-data)
> 的**免费样本**，数据由合作伙伴 [PMWallets](https://pmwallets.com/zh) 生成：每天依据此前 30 天已结算的市场给交易者排名，
> 把上榜者当天的链上成交写进一个文件。样本是三个真实 UTC 日（2026-10-08 到 2026-10-10），每天一个文件，内容是当天正式冻结名单里排名第 901 到 1000 名的交易者
> 当天的成交，文件格式与付费文件一致。

> Each day uses that day's frozen list, built from data through 23:59:59 UTC of the previous day — the same list the
> paid file for that day uses. Traders who ranked 1–900 on any frozen list from 2026-10-08 to 2026-10-11 are left out
> and not replaced (58, 65 and 73 of them on the three days), so the days hold 42, 35 and 27 traders.
>
> 每天用的都是当天的正式冻结名单（数据截至前一天 23:59:59 UTC），与当天付费文件用的是同一份。2026-10-08 到 10-11
> 任一份冻结名单中进过前 900 名的交易者已剔除且不补（三天分别 58、65、73 个），所以三天分别是 42、35、27 个交易者。

Also on [Kaggle](https://www.kaggle.com/datasets/ligengxin96/polymarket-smart-money-trades-sample) (decompressed CSV) and
[Hugging Face](https://huggingface.co/datasets/Ligengxin96/polymarket-smart-money-trades-sample).

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
| `2026-10-08/sample-2026-10-08.csv.zst` | 18,755 fills by 42 traders (75 wallets), zstd-compressed CSV with a header row |
| `2026-10-08/sample-2026-10-08.json` | that day's manifest: the ranking it was built from, its traders and their wallets |
| `2026-10-09/sample-2026-10-09.csv.zst` | 5,357 fills by 35 traders (60 wallets) |
| `2026-10-09/sample-2026-10-09.json` | that day's manifest |
| `2026-10-10/sample-2026-10-10.csv.zst` | 13,276 fills by 27 traders (48 wallets) |
| `2026-10-10/sample-2026-10-10.json` | that day's manifest |

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
- Community / 社区: [Discord](https://discord.gg/ZDMqkptwm5) (English and 中文) · [Telegram](https://t.me/+TcK_hJOzOz5mZTk1)

For research only; not investment advice. / 仅供研究，不构成投资建议。
