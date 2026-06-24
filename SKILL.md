---
name: bn-alpha-research
description: "Use when researching Binance Alpha / BN Alpha Pre-TGE new tokens for channel-ready #Alpha新币分析 reports, including contract checks, team/funding, tokenomics, VC cost, pre-open pool monitoring, AMM buy-depth estimates, CEX wallet-label observations, and decision-assist key reminders."
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

This skill distills Howe's BN Alpha research workflow into a reusable agent skill for Binance Alpha / BN Alpha Pre-TGE tokens. It is designed to produce concise Chinese `#Alpha新币分析` drafts for Telegram channels or research notes, plus decision-assist key reminders that only highlight risks and re-check items.

Source attribution:

- X/Twitter: [@0xcryptoHowe](https://x.com/0xcryptoHowe)
- Telegram Channel: [cryptohowe_treasure](https://t.me/cryptohowe_treasure)
- Telegram Group: [cyrptohowe_discussion](https://t.me/cyrptohowe_discussion)
- WeChat: `Howe_Wei` (please mention `调研Skill` when adding)
- Source thread: [Alpha Research Workflow List](https://x.com/0xcryptoHowe/status/1982980551285121407)

## When to Use

Use this skill when the user asks to:

- 调研 Binance Alpha / BN Alpha 新币
- 生成 `#Alpha新币分析` 频道草稿
- 分析 Pre-TGE / 上线前项目
- 接入盘前池子监控、买入深度估算、CEX 钱包标签观察
- 形成公开版报告 + 决策辅助重点提醒

Do not use it for:

- Post-TGE intraday trading monitoring
- 高频交易信号、盘口技术分析、OI/funding-rate 跟踪
- 自动发 Telegram 频道；默认只生成草稿
- 自动写入 Obsidian / LLM Wiki，除非用户明确要求

## Output Defaults

- Language: Chinese
- Public tag: `#Alpha新币分析`
- Scope: Pre-TGE only
- Public report: concise, channel-ready, with disclaimer
- Attribution: immediately below the title, add the markdown quote `> 本 BN 新币调研 Skill 由 [@0xcryptoHowe](https://x.com/0xcryptoHowe) 制作，欢迎关注反馈！` and ensure one visible blank line before `【01｜一分钟速览】`. Telegram may collapse raw blank lines after quote blocks, so use two raw newline gaps if needed.
- Front matter: add `【01｜一分钟速览】`, `【02｜关键数据卡】`, and `【03｜完整调研内容】` before the original long-form body
- Public visual summary: optional and off by default; generate only when explicitly requested
- Decision assist: key reminders only; see dedicated section for public-safety limits
- Disclaimer: always included

## First-use Optional API Key Guidance

This skill must remain usable without any API keys. If `ROOTDATA_API_KEY` or `ETHERSCAN_API_KEY` is missing, continue with public pages, official sources, CMC, DEX aggregators, and clearly labeled limitations instead of blocking the report.

For users installing the public skill for the first time, proactively explain that three optional keys improve data quality:

1. `ROOTDATA_API_KEY` — improves project profile, team, funding-round, investor, and ecosystem-label lookups. Users can apply for / enable OpenAPI from RootData API docs: `https://www.rootdata.com/ApiDoc` or `https://cn.rootdata.com/ApiDoc`.
2. `ETHERSCAN_API_KEY` — improves ETH and other Etherscan-supported chain contract-transfer and explorer checks through Etherscan API V2. Users can create a key after logging in at `https://etherscan.io/myapikey`; docs: `https://docs.etherscan.io/`.
3. `BSCSCAN_API_KEY` — improves BNB Chain / BSC contract-transfer and explorer checks when BSC is the main evidence chain. Users can create it from BscScan's API Keys page.

Never request keys in-chat unless the user explicitly wants help configuring their local environment; tell users to put keys in local `.env` or secure environment variables and never commit real keys.

## Required Public Report Structure

```text
#Alpha新币分析｜项目名 / SYMBOL

> 本 BN 新币调研 Skill 由 [@0xcryptoHowe](https://x.com/0xcryptoHowe) 制作，欢迎关注反馈！


【01｜一分钟速览】
说明：以下为 AI 基于公开资料生成的研究摘要，不代表作者本人建议，也不构成投资建议。
一句话结论：...
核心看点：...
最大风险：...
数据完整度：高 / 中 / 低
开盘前最该看：...

【02｜关键数据卡】
基础信息：...
供应与流通：...
融资与成本：...
价格参考：...
公开观察：...
风险标签：...

【03｜完整调研内容】

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
```

Important ordering rule: `合约地址与链上信息` must appear before `基本面与叙事`. Keep the original full body after `【03｜完整调研内容】`; the summary and data card are additions, not replacements.

## Front Matter Blocks

### 【01｜一分钟速览】

Place this immediately after the attribution quote. It must include the AI-generated-summary disclosure line and use compact label rows instead of an all-bullet list. Keep it public-safe: no buy/sell ranges, position sizing, or wording that sounds like author advice.

### 【02｜关键数据卡】

This is a structured extraction from the body report. Every field must be traceable to the same evidence set as the body. Use shortened CA in this text card only, e.g. `BSC｜0x1234...abcd`; full CA remains in section 二.

Recommended groups: 基础信息、供应与流通、融资与成本、价格参考、公开观察、风险标签.

### 【03｜完整调研内容】

Insert this separator after the data card and before `一、项目概况`. Do not add helper subtitles under `【01】/【02】/【03】`.

## Optional Public Visual Summary

Default: off. Generate an image only when the user explicitly asks for a public visual summary, 总结图, 配图, 数据表格, Tokenomics 图, or 图表.

Default path: deterministic HTML/CSS rendering to a 16:9 PNG via a headless browser when available. Do not require another infographic skill or model-native image generation for data-heavy charts. Do not use PIL/manual drawing as the default path.

Supported public visual modes:

- `summary_dashboard` — default recommendation for a channel-ready landscape public summary.
- `data_table` — structured key-field table image built from `【02｜关键数据卡】` and the same evidence set.
- `tokenomics_chart` — tokenomics allocation chart when public allocation data is complete; if allocation is incomplete, render a disclosure-status chart instead of inventing percentages.

Public visual rules:

- Build from `【01｜一分钟速览】` and `【02｜关键数据卡】`, not from private decision notes.
- Keep all modes visually consistent with `summary_dashboard`: dark dashboard/card-grid style, 16:9 landscape, visible section numbers, colored accents, readable Chinese, and footer disclaimer.
- Keep the image header clean: title + concise subtitle only. Do not add decorative top-right badge / pill boxes such as `HTML/CSS 16:9`, `Public Visual`, `Data Table`, `Tokenomics`, or `No Fake Ratio`.
- Do not include private trading bands, buy/sell ranges, position sizing, or strong trading instructions.
- Do not display CA / contract addresses in public summary images unless the user explicitly requests it.
- Do not write meta-placeholder copy in the image such as `不展示合约地址`, `图中不展示 CA`, or `合约地址已隐藏`; simply omit contract-address fields.
- For `tokenomics_chart`, do not force a pie/donut if data is incomplete. Label missing fields as `待披露`, `待核验`, or `无法计算`.
- Include a compact footer such as `非投资建议｜AI 基于公开资料生成｜数据以文字报告为准｜@0xcryptoHowe`.
- Verify Chinese legibility, no obvious overlap/cropping, and complete footer before returning the image; especially check for silent bottom-line cropping from `overflow:hidden`.

## Section Rules

### 一、项目概况

Keep it short. Include only:

- Project name, with the official X/Twitter handle appended as a clickable markdown link when available, without an `X：` label, e.g. `项目：ProjectName｜[@handle](https://x.com/handle)`
- `$SYMBOL`
- Alpha/listing/airdrop time in UTC+8, preferring Alpha123 hour-level time when available
- One-sentence positioning

Do not put detailed narrative, website, docs, tokenomics, or funding here. Do not add a separate `X：...` line; the official handle belongs at the end of the project line.

### 二、合约地址与链上信息

- Show BSC CA first whenever available
- Then ETH / SOL / other chains
- Each chain should include only CA + explorer link, plus a short caution if needed
- Do not dump explorer metadata such as holders/transfers/decimals/proxy unless user asks

### 三、基本面与叙事

Briefly cover sector, problem statement, product maturity, traction, narrative fit, and market attention. Avoid encyclopedia-style intros.

### 四、Tokenomics 与流通情况

Use compact blocks. Missing data must be explicit, e.g. `官方暂未披露完整 Tokenomics`, but do not conclude that tokenomics is missing from webpage extraction alone.

```text
Tokenomics：
- 总量：...
- 初始流通：...
- Team：...
- Investors：...
- Treasury / Ecosystem：...
```

Tokenomics source-check comments:

- If the official site/docs/CMC link to a whitepaper, litepaper, or PDF, download it and text-extract it before labeling Tokenomics as missing. Prefer PyMuPDF / `fitz` when available.
- Search extracted text for `allocation`, `genesis`, `tokenomics`, `unlock`, `vesting`, `circulating supply`, and inspect nearby figure/table text.
- If allocation/unlock/circulation data is embedded in PDF charts or screenshots, use OCR or vision on the relevant page/image.
- Follow snippets like `<SYMBOL> allocation at genesis`, `Figure ... allocation`, or `whitepaper ... tokenomics` back to the original source and verify directly.
- Distinguish `Allocation`, `Available Supply`, `Circulating Supply`, and `TGE unlock`; unlocked governance/future-activation pools may not equal immediate opening sell pressure.

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

If valuation/allocation data is missing, do not force a VC cost. The financing section must include concrete source links for `raised`, `incubated by`, `backed by`, `public sale`, `no VC allocation`, valuation/FDV, and investor claims; do not rely on vague source labels only. Put links on readable source names such as `[RootData 项目页](url)` / `[官方 Tokenomics](url)`, not as a naked URL list.

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

## Decision-Assist Key Reminders

Use a public-safe reminder section that highlights risks and items to re-check. Do not include concrete trading strategies, buy/sell prices, position-sizing advice, or strong trading instructions.

```text
十、决策辅助与开盘前重点提醒
- Tokenomics：重点复核初始流通、解锁节奏、空投领取时间，判断开盘抛压是否可能集中。
- 合约与链上：复核最终 CA 是否与 Binance Alpha / 官方渠道一致，避免同名项目或临时池子误判。
- 盘前 / 池子：关注 MEXC 盘前成交量是否有效、DEX 池子流动性是否足够、主池和深度估算池是否一致。
- 融资与成本：确认融资来源、轮次估值 / FDV 口径是否可靠，避免把 equity valuation 误当 token FDV。
- CEX 与链上标签：CEX 钱包标签只作为链上观察，不等同官方充值或上线确认。
- 临开盘复核：最终 Tokenomics、CA、池子流动性、盘前价、官方公告是否有新增变化。
```

## Security Rules

- Never commit real API keys, tokens, secrets, `.env`, raw credentials, private keys, or seed phrases
- Use `.env.example` placeholders only
- If docs mention API variables, values must be placeholders like `your_etherscan_api_key_here`
- RootData API keys can be requested / enabled from the [RootData API docs](https://www.rootdata.com/ApiDoc) or [RootData CN API docs](https://cn.rootdata.com/ApiDoc); RootData provides free quota suitable for normal daily project/team/funding lookups.
- Etherscan API keys can be created after logging in on the [Etherscan API Keys page](https://etherscan.io/myapikey); docs: [Etherscan API docs](https://docs.etherscan.io/). Etherscan API V2 provides free-tier usage that is usually enough for daily BN Alpha contract-transfer and explorer checks; configure it as `ETHERSCAN_API_KEY`, with `BSCSCAN_API_KEY` only as an optional BNB Chain override.
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
9. **Generating public visuals by default.** Public images are optional; generate them only when explicitly requested.
10. **Writing `不展示合约地址` inside images.** Public visuals should simply omit CA fields rather than explaining that the CA is hidden.
11. **Letting Telegram eat the blank line after attribution.** Ensure one visible blank line between the attribution quote and `【01｜一分钟速览】`; use an extra raw newline if needed.

## Verification Checklist

- [ ] `#Alpha新币分析` included
- [ ] Attribution quote appears below the title, with one visible blank line before `【01｜一分钟速览】`
- [ ] `【01｜一分钟速览】`, `【02｜关键数据卡】`, and `【03｜完整调研内容】` are present
- [ ] `【01｜一分钟速览】` includes the required AI-generated-summary disclosure and no private trading advice
- [ ] `【02｜关键数据卡】` only extracts fields supported by the body/evidence set
- [ ] Project overview is short, uses `$SYMBOL`, and appends the official X/Twitter handle to the project line when available
- [ ] Alpha/listing/airdrop time uses Alpha123 first when available and is normalized to UTC+8 without double conversion
- [ ] Contract section before fundamentals
- [ ] BSC CA first, CA + explorer only
- [ ] Team limited to founders/co-founders by default
- [ ] LinkedIn links directly on names
- [ ] Tokenomics missing data labeled explicitly
- [ ] Financing/incubation/public-sale claims include concrete source links embedded in readable text
- [ ] VC cost includes unit cost + FDV when computable
- [ ] Pool block uses monitor output where available
- [ ] Main pool and depth-estimation pool separated
- [ ] Buy-depth levels are separate indented bullets
- [ ] CEX wallet labels include non-official-confirmation note
- [ ] Public body has no explicit trading bands, concrete trading strategy, or position-sizing advice
- [ ] Decision-assist section only lists key reminders and contains no strong trading instructions
- [ ] Disclaimer included
- [ ] Optional public image generated only on request, excludes CA/private decision content, and has no `不展示合约地址` placeholder text
- [ ] Public visual was QA-checked for Chinese legibility, no overlap/cropping, and complete footer
- [ ] No `.env` or real API keys committed
