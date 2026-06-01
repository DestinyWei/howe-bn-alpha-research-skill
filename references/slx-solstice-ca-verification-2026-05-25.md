# SLX / Solstice CA verification notes (2026-05-25)

Use this as a case study when a Binance Alpha symbol collides with an older token or when the user provides a CA before official confirmation.

## What happened

User asked for `$SLX 0x02bcc4c181b83a8c0a342bc003389cbecb4bc54d`.

Naive `bn-alpha-monitor snapshot-from-listing --source binance-alpha --symbol SLX` returned the older **SLIMEX / SLX** listing:

- Name: SLIMEX
- BSC CA: `0x8a063a9ff4de28dcb87117cc759be6ce70e09f81`
- Listing time: 2025-10-08 15:00 UTC+8
- Supply: 10B

But web/X/news lookup showed the intended project was **Solstice / SLX**, a 2026-05-25 Binance Alpha project.

## Verification findings

- User-provided BSC CA: `0x02bcC4C181B83a8c0A342BC003389CbEcb4BC54D`
  - BscScan showed about 21.0M supply and very few holders.
  - Dexscreener / GeckoTerminal found no valid pool for that exact CA.
  - This did **not** match official Solstice tokenomics of 1B total supply.
  - Treat as an unconfirmed / suspicious early-monitor address unless official Binance/Project confirms it.

- More credible BSC trading CA observed from active pools:
  - `0x4516096ee830171b2aafFc62d05DF0515B090d37`
  - BscScan showed 1B supply.
  - Dexscreener / GeckoTerminal showed active PancakeSwap V2 SLX/USDT pool:
    - Pair: `0xA6c7885baeb65102b54AF375Ae9764af49F1393D`
    - Liquidity around $2M during the check
    - FDV around $70M–$75M during the check

- CoinGecko Solstice listed Solana platform CA:
  - `SLXdx4BUt2v9uJQNzWqSfzTJ9UKLUDsvxHFMEEdrfgq`
  - CoinGecko API described Solstice as a Solana DeFi / Yield Layer project.

## Official / higher-confidence project facts found

- [Official site](https://solstice.finance/)
- [Official X](https://x.com/solsticefi)
- [Docs tokenomics](https://docs.solstice.finance/solstice-for-users/slx/tokenomics)
- RootData project: Solstice, project_id 14462
- RootData description: DeFi protocol on Solana with USX, YieldVault, and Solstice Staking; product of Deus X Capital.
- Official Tokenomics:
  - Total supply: 1B SLX
  - Foundation: 24% (50% TGE; 30-month vesting)
  - Community: 37.71% (21.2% TGE; 36-month vesting)
  - Team & Advisors: 20% (0% TGE; 12-month cliff; 24-month vesting)
  - Airdrops: 10% (varied)
  - Strategic TVL Partners: 8% (25% TGE; 12-month vesting)
  - Public Sale: 0.29% (100% TGE)
  - Initial circulating supply: ~24%
  - Official docs explicitly state no early VC token allocations.

## Workflow lesson

When symbol-only lookup returns an old Binance Alpha entry, especially for a short reused ticker like `SLX`, do not rely on the local monitor result alone. Cross-check:

1. User-provided CA against BscScan supply/holders/decimals.
2. Dexscreener / GeckoTerminal for active pools by that exact CA.
3. Search web/X for `project name + symbol + Binance Alpha`.
4. Official X / docs / CoinGecko / CMC for current project identity.
5. If the Binance Alpha API returns a different project with the same symbol, explicitly label it as a stale/symbol-collision result, not the intended project.

## Reporting lesson

Lead with a CA warning before the report if the user-provided CA is not supported by official/project/pool evidence. In the contract section, list:

- Confirmed or more credible active-pool CA first.
- Official Solana CA if relevant.
- User-provided CA separately as `待确认 / 风险地址` with the reason.

## Alpha123 time lesson

For this workflow, Alpha123 is the preferred source for hour-level Alpha / listing / airdrop time when available. Treat Alpha123 displayed time as UTC+8 unless the source explicitly says otherwise. If Alpha123 shows `20:00` and official X only says `May 25`, report `20:00 UTC+8` from Alpha123 and use official X only as date-level confirmation. Third-party monitors that show a different hour should be labeled as supplemental third-party monitoring, not the primary launch time.
