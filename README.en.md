# BN Alpha Research Skill Usage Guide

This repository documents the `bn-alpha-research` skill: a reusable workflow for Binance Alpha / BN Alpha Pre-TGE token research.

The default repository README is intentionally kept in Chinese. This English document is provided for non-Chinese readers and contributors.

## Author and Sources

- Author / Curator: Howe
- X: https://x.com/0xcryptoHowe
- Telegram Channel: https://t.me/cryptohowe_treasure
- Telegram Group: https://t.me/cyrptohowe_discussion
- Source thread: https://x.com/0xcryptoHowe/status/1982980551285121407

This skill distills Howe's X thread and Howe's Telegram Alpha token research content into a structured Pre-TGE research workflow for BN Alpha tokens.

---

## Repository Structure

```text
howe-bn-alpha-research-skill/
├── README.md                         # Chinese default README
├── README.en.md                      # English guide
├── SKILL.md                          # Hermes-compatible skill definition
├── references/
│   ├── bn-alpha-monitor-tool-notes.md
│   ├── data-source-priority.md
│   └── report-format.md
├── templates/
│   ├── alpha-report-template.md
│   ├── alpha-report-template.en.md
│   ├── private-note-template.md
│   └── private-note-template.en.md
├── examples/
│   ├── nexus-nex.md
│   └── nexus-nex.en.md
├── .env.example
├── .gitignore
└── LICENSE
```

## Purpose

`bn-alpha-research` is used to generate channel-ready research drafts for Binance Alpha / BN Alpha Pre-TGE tokens.

It covers:

- Binance Alpha / Alpha123 listing discovery
- Project overview and one-line positioning
- Contract and on-chain information
- Fundamentals and narrative
- Tokenomics and circulating supply
- Founder/team background and LinkedIn checks
- Funding and VC cost estimation
- Pre-open pool monitoring
- AMM buy-depth estimation
- CEX wallet-label observations
- Key risks and pre-open watchlist
- A separate private decision note

This workflow is for **Pre-TGE / pre-listing research**, not post-launch intraday trading monitoring.

---

## Default Output Style

The default output is Chinese and includes two parts:

1. **Public channel draft**
   - Includes the fixed `#Alpha新币分析` tag
   - Concise and Telegram-ready
   - No explicit public trading bands or fair-value ranges by default
   - Includes a disclaimer

2. **Private decision note**
   - More direct and opinionated
   - May include participation bias, valuation ranges, and abandon conditions
   - Not intended for public channel posting

---

## Recommended Prompt

```text
Use bn-alpha-research to research NEX in our #Alpha新币分析 format. Include pre-open pool monitoring and a private decision note.
```

If you already have links or contracts:

```text
Use bn-alpha-research to research this BN Alpha token:
Project: Nexus / NEX
BSC CA: 0x...
ETH CA: 0x...
CMC: https://coinmarketcap.com/...
Official website: https://...
X: https://x.com/...
```

---

## Public Report Structure

```text
#Alpha新币分析｜Project Name / SYMBOL

一、项目概况
二、合约地址与链上信息
三、基本面与叙事
四、Tokenomics 与流通情况
五、团队背景
六、融资背景与 VC 成本推算
七、盘前价 / 池子价
八、估值与开盘观察
九、主要风险
十、开盘前观察重点

免责声明：以上内容仅为个人研究记录，不构成任何投资建议。新币开盘波动较大，请自行判断风险。

【私人决策备注】
...
```

Important rules:

- `合约地址与链上信息` must come before `基本面与叙事`.
- `项目概况` should stay short: project, `$SYMBOL`, UTC+8 launch time, and one-line positioning only.
- The public report should not show explicit trading bands or fair-value ranges by default.

---

## Team and LinkedIn Format

LinkedIn links should be attached directly to names.

Correct:

```text
- [Daniel Marin](https://www.linkedin.com/in/danielmarin)：Co-founder / CEO，responsible for overall strategy and product direction.
```

Avoid:

```text
- Daniel Marin：Co-founder / CEO
  LinkedIn：https://www.linkedin.com/in/danielmarin
```

---

## Pre-Open Pool Monitoring Format

The skill can use the local `bn-alpha-monitor` tool when available.

```bash
cd /home/ubuntu/bn-alpha-monitor
PYTHONPATH=src python -m bn_alpha_monitor.cli snapshot-from-listing   --source binance-alpha   --symbol NEX   --no-save   --report-block
```

Expected report block style:

```text
盘前 / 池子：Nexus / $NEX
- 主池：BSC pancakeswap-infinity-clmm；当前 FDV $19.9M；流动性 $1.5M
- 深度估算池：BSC uniswap pool
- 买入深度：按池子流动性估算
  - 约 $19.22k 可推至 $39.75M FDV
  - 约 $33.97k 可推至 $59.62M FDV
  - 约 $57.35k 可推至 $99.37M FDV
- 风险标记：买入深度为普通 AMM 公式估算，未计入手续费/MEV/动态流动性
```

Rules:

- Separate the main pool from the depth-estimation pool.
- If the main pool is CLMM / V3 / Infinity, do not infer buy-depth from TVL alone.
- Buy-depth tiers default to roughly 2x / 3x / 5x current FDV.
- Each target FDV should be displayed on its own line.
- Third-party depth evidence has priority, but must be labeled as third-party chain monitoring.

---

## CEX Wallet-Label Wording

Use wording that cannot be mistaken for official exchange confirmation.

Recommended:

```text
- CEX 钱包标签命中：Coinbase / Kraken / KuCoin（链上转账观察）
- 说明：以上仅表示命中已知交易所钱包标签，不等同官方上线/充值确认
```

Avoid:

```text
- CEX 痕迹：Coinbase 有转账痕迹，链上观察，不等同官方确认
```

---

## Security

Environment variables may include:

```bash
ETHERSCAN_API_KEY=your_etherscan_api_key_here
BSCSCAN_API_KEY=your_bscscan_api_key_here
ROOTDATA_API_KEY=your_rootdata_api_key_here
BN_ALPHA_MONITOR_DATA_DIR=./data/monitor_snapshots
```

Rules:

- Keep real keys only in local `.env` files or secure environment variables.
- Never commit `.env`.
- Only commit `.env.example` placeholders.
- Never put real keys in README, tests, examples, templates, reports, or skill files.

---

## Final Checklist

- [ ] `#Alpha新币分析` included
- [ ] Project overview is concise
- [ ] `$SYMBOL` format is correct
- [ ] Time converted to UTC+8
- [ ] Contract section appears before fundamentals
- [ ] BSC CA shown first when available
- [ ] Founder LinkedIn links are attached directly to names
- [ ] Tokenomics missing data is explicitly labeled
- [ ] VC cost includes unit cost + FDV when calculable
- [ ] Pool block uses monitor output where available
- [ ] Main pool and depth-estimation pool are separated
- [ ] Buy-depth tiers are shown as separate indented bullets
- [ ] CEX wallet labels are not described as official confirmations
- [ ] Public report has no explicit trading bands by default
- [ ] Private decision note is separated from public report
- [ ] Disclaimer included
- [ ] No real API keys committed
