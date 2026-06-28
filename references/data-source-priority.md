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

## 4. 盘前价 / 池子与链上监控

1. **MEXC pre-market**
   - 检查通用盘前页或 direct symbol URL。
   - 记录价格、成交量和是否为有效市场；如果页面显示 `Closed` / `--` / `TBD`，写成无有效盘前参考。
2. **Aspecta pre-market / BuildKey trading**：`https://trade.aspecta.ai/`
   - 查找匹配项目 / token 的盘前或 BuildKey-style 市场。
   - 记录价格、成交量、流动性、深度、更新时间等 UI 可见字段。
   - Aspecta 是 MEXC 之外的额外盘前参考，不替代 MEXC。两者价格不一致时分别列出，按成交量、深度和新鲜度判断参考价值，不做简单平均。
   - 如果没有匹配市场或页面不可访问，明确写 `Aspecta 暂未发现有效盘前价格`。
3. 本地 `bn-alpha-monitor`
4. Dexscreener
5. GeckoTerminal
6. Dextools
7. Etherscan API V2 / BSC via Etherscan V2 chainid
8. 可信第三方链上监控帖

规则：

- 第三方链上监控必须标注来源，且不能覆盖 Alpha123 的小时级时间。
- CEX 钱包标签只是链上观察，不等同官方上线/充值确认。
- CLMM/V3/Infinity 不应只用 TVL 估算买入深度。
- 盘前价至少查 MEXC + Aspecta；任一来源缺失时要显式说明，而不是省略。
