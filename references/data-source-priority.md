# 数据源优先级

## 1. 发现与上线信息

1. **Alpha123**
   - 优先用于小时级 Alpha / 上线 / 空投时间。
   - Alpha123 界面/API 时间按 UTC+8 处理，除非来源明确标注其它时区。
   - 示例：Alpha123 显示 `20:00`，报告写 `20:00 UTC+8`，不要再按 UTC 转换一次。
2. Binance Alpha public API / Binance Alpha 页面
   - 用于项目、日期、活动入口、最终页面展示交叉验证。
3. 官方 X / 官网公告
   - 优先确认项目身份与上线日期。
   - 如果只给日期、不含小时，不覆盖 Alpha123 小时级时间。
4. 可信第三方链上监控
   - 仅作补充，必须标注为“第三方监控”。

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

- 第三方链上监控必须标注来源，且不能覆盖 Alpha123 的小时级时间。
- CEX 钱包标签只是链上观察，不等同官方上线/充值确认。
- CLMM/V3/Infinity 不应只用 TVL 估算买入深度。
