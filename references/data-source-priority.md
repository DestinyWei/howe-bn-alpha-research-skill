# 数据源优先级

## 1. 发现与上线信息

1. Binance Alpha public API / Binance Alpha 页面
2. Alpha123
3. 官方 X / 官网公告

## 2. 合约与供应

1. 官方文档 / 官方 X / 官网
2. CoinMarketCap
3. BscScan / Etherscan
4. Dexscreener / GeckoTerminal

规则：

- BSC CA 优先展示。
- 多链项目要检查 bridge / wrapped supply，不要直接把 BSC supply 和 total supply 的差异写成疑点。
- CA 未官方确认时必须标注风险。

## 3. 团队与融资

1. RootData API / RootData 页面
2. 官方 team 页面
3. LinkedIn
4. Crunchbase / 公开报道

规则：

- 默认只写 founders / co-founders / CEO / chief scientist。
- LinkedIn 直接挂在人名上。
- LinkedIn 无法访问时，明确写核验限制。

## 4. 池子与链上监控

1. 本地 `bn-alpha-monitor`
2. Dexscreener
3. GeckoTerminal
4. Dextools
5. Etherscan API V2 / BSC via Etherscan V2 chainid
6. 可信第三方链上监控帖

规则：

- 第三方链上监控必须标注来源。
- CEX 钱包标签只是链上观察，不等同官方上线/充值确认。
- CLMM/V3/Infinity 不应只用 TVL 估算买入深度。
