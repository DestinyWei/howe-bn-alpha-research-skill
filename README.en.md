# BN Alpha Research Skill Usage Guide

This repository documents the `bn-alpha-research` skill: a reusable workflow for Binance Alpha / BN Alpha Pre-TGE token research.

The default repository README is intentionally kept in Chinese. This English document is provided for non-Chinese readers and contributors.

## Author and Sources

- Author / Curator: Howe
- X/Twitter: [@0xcryptoHowe](https://x.com/0xcryptoHowe)
- Telegram Channel: [cryptohowe_treasure](https://t.me/cryptohowe_treasure)
- Telegram Group: [cyrptohowe_discussion](https://t.me/cyrptohowe_discussion)
- WeChat: `Howe_Wei` (please mention `调研Skill` when adding)
- Source thread: [Alpha Research Workflow List](https://x.com/0xcryptoHowe/status/1982980551285121407)

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
│   ├── report-format.md
│   └── slx-solstice-ca-verification-2026-05-25.md
├── templates/
│   ├── alpha-report-template.md
│   ├── alpha-report-template.en.md
│   ├── decision-reminder-template.md
│   └── decision-reminder-template.en.md
├── examples/                          # Full example outputs covering sections 1-10
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
- Key risks
- Decision-assist and pre-open reminder checklist

This workflow is for **Pre-TGE / pre-listing research**, not post-launch intraday trading monitoring.

---

## Default Output Style

The default output is a concise Chinese public channel draft with the fixed `#Alpha新币分析` tag and a disclaimer.

---

## Recommended Prompt

```text
Use bn-alpha-research to research NEX in our #Alpha新币分析 format. Include pre-open pool monitoring and decision-assist key reminders.
```

If you already have links or contracts:

```text
Use bn-alpha-research to research this BN Alpha token:
Project: Nexus / NEX
BSC CA: 0x...
ETH CA: 0x...
CMC: [CoinMarketCap link]
Official website: [official website link]
X: [official X link]
```

---

## Public Report Structure

```text
#Alpha新币分析｜Project Name / SYMBOL

> 本 BN 新币调研 Skill 由 [@0xcryptoHowe](https://x.com/0xcryptoHowe) 制作，欢迎关注反馈！

一、项目概况
二、合约地址与链上信息
三、基本面与叙事
四、Tokenomics 与流通情况
五、团队背景
六、融资背景与 VC 成本推算
七、盘前价 / 池子价
八、估值与开盘观察
九、主要风险
十、决策辅助与开盘前重点提醒

免责声明：以上内容仅为个人研究记录，不构成任何投资建议。新币开盘波动较大，请自行判断风险。
```

Important rules: `合约地址与链上信息` must come before `基本面与叙事`; `项目概况` should stay short: project, `$SYMBOL`, Alpha123-prioritized UTC+8 launch/airdrop time, and one-line positioning only. Add the project's official X/Twitter handle at the end of the project line as a clickable markdown link when available, without an `X：` label. The public draft also includes Howe's attribution quote after one blank line below the title.

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
  LinkedIn：单独一行链接（不要这样写）
```

---

## Funding Source Links

Funding, incubation, public-sale, no-VC-allocation, valuation/FDV, and investor claims must include concrete source links in the report. Avoid vague labels like “RootData shows” without a URL. Embed links in readable source names such as `[RootData project page](url)` / `[official tokenomics](url)` instead of pasting a series of naked URLs.

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

## Decision-Assist and Key Reminder Format

The public version may keep a `决策辅助与开盘前重点提醒` section, but it should only list key risks and information to re-check. Do not include concrete trading strategies, buy/sell prices, position sizing, or strong trading instructions.

Example:

```text
十、决策辅助与开盘前重点提醒
- Tokenomics: re-check initial circulation, unlock schedule, and airdrop claim timing to assess possible opening sell pressure.
- Contract and on-chain: verify the final CA against Binance Alpha / official channels to avoid same-symbol or provisional-pool mistakes.
- Pre-open / pool: check whether MEXC pre-market volume is meaningful, DEX liquidity is sufficient, and the main pool matches the depth-estimation pool.
- Funding and cost: verify funding sources and valuation / FDV methodology; do not treat equity valuation as token FDV without evidence.
- CEX and labels: wallet-label hits are on-chain observations only, not official deposit or listing confirmation.
- Pre-open re-check: final Tokenomics, CA, pool liquidity, pre-market price, and official announcements.
```

---

## Launch-Time Source Priority

For hour-level Alpha / listing / airdrop time, prefer Alpha123 when available. Treat Alpha123 UI/API times as UTC+8 unless the source explicitly states otherwise. Binance Alpha official pages and official X should be used to cross-check project identity and date; a date-only official X post should not overwrite Alpha123's hour-level time. Credible third-party chain monitors can be referenced only as supplemental third-party monitoring.

---

## Security

Environment variables may include:

```bash
ETHERSCAN_API_KEY=your_etherscan_api_key_here
BSCSCAN_API_KEY=your_bscscan_api_key_here
ROOTDATA_API_KEY=your_rootdata_api_key_here
BN_ALPHA_MONITOR_DATA_DIR=./data/monitor_snapshots
```

Where to get the API keys:

- RootData API: apply for / enable OpenAPI from the RootData website. Start from the [RootData API docs](https://www.rootdata.com/ApiDoc) or [RootData CN API docs](https://cn.rootdata.com/ApiDoc). It is used for project, team, funding, and investor data.
- Etherscan API: register / log in to Etherscan and create a key on the API Keys page: `https://etherscan.io/myapikey`; docs: `https://docs.etherscan.io/`. Etherscan API V2 can query ETH / BSC and other chains via `chainid`; this workflow defaults to `ETHERSCAN_API_KEY`, with `BSCSCAN_API_KEY` as an optional BNB Chain override.

Quota notes:

- Both RootData API and Etherscan API provide free quota / free-tier usage.
- For normal BN Alpha new-token research, team/funding checks, contract-transfer observation, and pool evidence verification, the free tiers are usually enough for daily use.
- Consider paid tiers only if you later run high-frequency automated monitoring, scan many projects in bulk, or serve multiple users from one shared key.

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
- [ ] Launch/airdrop time uses Alpha123 first when available and is written as UTC+8 without double conversion
- [ ] Contract section appears before fundamentals
- [ ] BSC CA shown first when available
- [ ] Founder LinkedIn links are attached directly to names
- [ ] Tokenomics missing data is explicitly labeled
- [ ] Funding/incubation/public-sale/no-VC claims include concrete source links embedded in readable text
- [ ] VC cost includes unit cost + FDV when calculable
- [ ] Pool block uses monitor output where available
- [ ] Main pool and depth-estimation pool are separated
- [ ] Buy-depth tiers are shown as separate indented bullets
- [ ] CEX wallet labels are not described as official confirmations
- [ ] Decision-assist section only lists key reminders, not concrete trading actions
- [ ] Disclaimer included
- [ ] No real API keys committed
