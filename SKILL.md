---
name: bn-alpha-research
description: "Use when researching Binance Alpha / BN Alpha Pre-TGE new tokens for channel-ready #Alpha新币分析 reports, including contract checks, team/funding, tokenomics, VC cost, pre-open pool monitoring, AMM buy-depth estimates, CEX wallet-label observations, and a private decision note."
version: 1.0.0
author: Howe
license: MIT
metadata:
  hermes:
    tags: [crypto, binance-alpha, pre-tge, token-research, chinese-report]
    related_skills: [x-tweet-fetcher]
---

# BN Alpha 新币 Pre-TGE 调研

## Overview

This skill distills Howe's BN Alpha research workflow into a reusable agent skill for Binance Alpha / BN Alpha Pre-TGE tokens. It is designed to produce concise Chinese `#Alpha新币分析` drafts for Telegram channels or research notes, plus a separate private decision note.

Source attribution:

- Howe X: https://x.com/0xcryptoHowe
- Telegram Channel: https://t.me/cryptohowe_treasure
- Telegram Group: https://t.me/cyrptohowe_discussion
- Source thread: https://x.com/0xcryptoHowe/status/1982980551285121407

## When to Use

Use this skill when the user asks to:

- 调研 Binance Alpha / BN Alpha 新币
- 生成 `#Alpha新币分析` 频道草稿
- 分析 Pre-TGE / 上线前项目
- 接入盘前池子监控、买入深度估算、CEX 钱包标签观察
- 形成公开版报告 + 私人决策备注

Do not use it for:

- Post-TGE intraday trading monitoring
- 高频交易信号、盘口技术分析、OI/funding-rate 跟踪
- 自动发 Telegram 频道；默认只生成草稿
- 自动写入 Obsidian / LLM Wiki，除非用户明确要求

## Output Defaults

- Language: Chinese
- Public tag: `#Alpha新币分析`
- Scope: Pre-TGE only
- Public report: concise, channel-ready, no explicit public valuation/trading bands
- Private note: direct, can include participation view and explicit ranges if enough data exists
- Disclaimer: always included

## Required Public Report Structure

```text
#Alpha新币分析｜项目名 / SYMBOL

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

Important ordering rule: `合约地址与链上信息` must appear before `基本面与叙事`.

## Section Rules

### 一、项目概况

Keep it short. Include only:

- Project name
- `$SYMBOL`
- Alpha/listing/airdrop time in UTC+8, preferring Alpha123 hour-level time when available
- One-sentence positioning

Do not put detailed narrative, website, X, docs, tokenomics, or funding here.

### 二、合约地址与链上信息

- Show BSC CA first whenever available
- Then ETH / SOL / other chains
- Each chain should include only CA + explorer link, plus a short caution if needed
- Do not dump explorer metadata such as holders/transfers/decimals/proxy unless user asks

### 三、基本面与叙事

Briefly cover sector, problem statement, product maturity, traction, narrative fit, and market attention. Avoid encyclopedia-style intros.

### 四、Tokenomics 与流通情况

Use compact blocks. Missing data must be explicit, e.g. `官方暂未披露完整 Tokenomics`.

```text
Tokenomics：
- 总量：...
- 初始流通：...
- Team：...
- Investors：...
- Treasury / Ecosystem：...
```

### 五、团队背景

Only cover founders / co-founders / CEO-level core people by default.

If LinkedIn is available, link it directly on the person's name:

```text
- [Daniel Marin](https://www.linkedin.com/in/danielmarin)：Co-founder / CEO，负责项目整体战略与产品方向。
```

Do not use a separate `LinkedIn：https://...` line.

### 六、融资背景与 VC 成本推算

Use compact blocks and label calculation precision.

```text
融资情况：
- Seed：$xM｜Lead：...｜投资人：...
- Series A：$xM｜Lead：...｜投资人：...
- 总融资：$xM

VC 成本：
- 可计算性：精确 / 粗略 / 无法计算
- 成本价：$...
- 对应 FDV：$...
- 计算口径：...
- 限制：...
```

If valuation/allocation data is missing, do not force a VC cost.

### 七、盘前价 / 池子价

Prefer the local monitor tool when available.

```bash
cd /home/ubuntu/bn-alpha-monitor
PYTHONPATH=src python -m bn_alpha_monitor.cli snapshot-from-listing \
  --source binance-alpha \
  --symbol <SYMBOL> \
  --no-save \
  --report-block
```

Report rendering rules:

- Separate `主池` from `深度估算池`
- Buy-depth tiers should be one line each
- Default tiers are roughly 2x / 3x / 5x current FDV
- CLMM/V3/Infinity pool TVL must not be used as if it were ordinary x*y=k depth
- Third-party depth evidence has priority when supplied, but must be labeled as third-party monitoring

Example:

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

### CEX 钱包标签

Use wording that cannot be mistaken for official CEX listing/recharge confirmation:

```text
- CEX 钱包标签命中：Coinbase / Kraken / KuCoin（链上转账观察）
- 说明：以上仅表示命中已知交易所钱包标签，不等同官方上线/充值确认
```

Avoid older wording like `CEX 痕迹：... 有转账痕迹`.

## Data Source Priority

See `references/data-source-priority.md` for the full source order.

Short version:

1. Alpha123 first for hour-level Alpha/listing/airdrop time; treat its displayed time as UTC+8 unless explicitly stated otherwise
2. Binance Alpha official page/API and official X for project/date cross-checking; a date-only X post should not overwrite Alpha123's hour-level time
3. Official website/docs/X for authoritative project and CA claims
4. CoinMarketCap for supply/contract metadata, cross-checked with official sources
5. RootData and LinkedIn for team/funding
6. Local `bn-alpha-monitor`, Dexscreener, GeckoTerminal, Dextools, and explorer APIs for pool/on-chain evidence

## Private Decision Note

Use a clearly separated private section:

```text
【私人决策备注】
参与倾向：低 / 中 / 高
适合策略：不追高 / 小仓博弈 / 等回调 / 只观察
关键观察：
- ...
放弃条件：
- ...
```

Explicit trading bands and valuation ranges belong here, not in the public body.

## Security Rules

- Never commit real API keys, tokens, secrets, `.env`, raw credentials, private keys, or seed phrases
- Use `.env.example` placeholders only
- If docs mention API variables, values must be placeholders like `your_etherscan_api_key_here`
- RootData API keys can be requested / enabled from the RootData API docs: `https://www.rootdata.com/ApiDoc` or `https://cn.rootdata.com/ApiDoc`; RootData provides free quota suitable for normal daily project/team/funding lookups.
- Etherscan API keys can be created after logging in at `https://etherscan.io/myapikey`; docs: `https://docs.etherscan.io/`. Etherscan API V2 provides free-tier usage that is usually enough for daily BN Alpha contract-transfer and explorer checks; configure it as `ETHERSCAN_API_KEY`, with `BSCSCAN_API_KEY` only as an optional BNB Chain override.
- Run a secret scan before committing

## Common Pitfalls

1. **Putting LinkedIn on a separate line.** Link directly on the person's name.
2. **Mixing official confirmation with chain observation.** CEX wallet labels are not official listing/recharge confirmation.
3. **Using CLMM total liquidity for buy-depth.** CLMM/V3/Infinity requires tick/range liquidity.
4. **Burying contract info.** Contract/on-chain section must come before fundamentals.
5. **Forcing VC cost.** If valuation/allocation data is absent, write `无法计算`.
6. **Overloading the public channel body.** Keep detailed raw evidence in JSON/references, not the Telegram draft.
7. **Publishing without confirmation.** Return a draft only unless explicitly asked to publish.
8. **Misreading Alpha123 time zones.** Alpha123 times are treated as UTC+8 in this workflow. Do not convert them again as if they were UTC; if Alpha123 shows `20:00`, report `20:00 UTC+8`.

## Verification Checklist

- [ ] `#Alpha新币分析` included
- [ ] Project overview is short and uses `$SYMBOL`
- [ ] Alpha/listing/airdrop time uses Alpha123 first when available and is normalized to UTC+8 without double conversion
- [ ] Contract section before fundamentals
- [ ] BSC CA first, CA + explorer only
- [ ] Team limited to founders/co-founders by default
- [ ] LinkedIn links directly on names
- [ ] Tokenomics missing data labeled explicitly
- [ ] VC cost includes unit cost + FDV when computable
- [ ] Pool block uses monitor output where available
- [ ] Main pool and depth-estimation pool separated
- [ ] Buy-depth levels are separate indented bullets
- [ ] CEX wallet labels include non-official-confirmation note
- [ ] Public body has no explicit trading bands by default
- [ ] Private decision note separated
- [ ] Disclaimer included
- [ ] No `.env` or real API keys committed
