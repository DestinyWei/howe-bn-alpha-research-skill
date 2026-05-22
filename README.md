# BN Alpha 新币调研 Skill 使用说明

这个文档用于说明 `bn-alpha-research` skill 的使用方式，适合放到新的仓库作为 README / workflow 文档。

English guide: [README.en.md](README.en.md)

## 作者与来源

- 作者 / 整理：Howe
- X：https://x.com/0xcryptoHowe
- Telegram Channel：https://t.me/cryptohowe_treasure
- Telegram Group：https://t.me/cyrptohowe_discussion
- 灵感来源：https://x.com/0xcryptoHowe/status/1982980551285121407

这个 skill 是蒸馏并结合 Howe 上述推文，以及 Howe 个人 Telegram 频道中所有 Alpha 新币调研内容后，整理形成的一套 BN Alpha 新币 Pre-TGE 调研工作流。

---

## 仓库结构

```text
howe-bn-alpha-research-skill/
├── README.md                         # 中文默认文档
├── README.en.md                      # English guide
├── SKILL.md
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

- `SKILL.md`：Hermes / agent 可加载的核心 skill 定义。
- `README.md`：面向仓库读者的中文默认使用说明。
- `README.en.md`：英文使用说明。
- `references/`：数据源、报告格式、盘前监控工具接入说明。
- `templates/`：公开报告和私人备注模板。
- `examples/`：示例输出。
- `.env.example`：环境变量占位符；不要提交真实 `.env`。

---

## 1. 用途

`bn-alpha-research` 用于 Binance Alpha / BN Alpha Pre-TGE 新币调研，目标是生成可直接用于 Telegram 频道或研报草稿的中文 `#Alpha新币分析`。

主要覆盖：

- Binance Alpha / Alpha123 上线信息
- 项目概况与一句话定位
- 合约地址与链上信息
- 基本面与叙事
- Tokenomics 与流通情况
- 团队背景与 LinkedIn 核验
- 融资背景与 VC 成本推算
- 盘前 / 池子监控
- 买入深度估算
- CEX 钱包标签命中观察
- 主要风险
- 开盘前观察重点
- 私人决策备注

默认场景是 **Pre-TGE / 上线前调研**，不是 Post-TGE 盘中交易监控。

---

## 2. 默认输出风格

默认输出为中文，包含两部分：

1. **公开版频道草稿**
   - 使用 `#Alpha新币分析` 标签
   - 内容 concise，可直接复制到 Telegram
   - 不展示明确买卖区间或公开估值区间
   - 保留免责声明

2. **私人决策备注**
   - 可以更直接
   - 可以写参与倾向、价格区间、放弃条件
   - 不作为公开频道内容

---

## 3. 推荐调用方式

### 3.1 调研单个 BN Alpha 新币

示例 prompt：

```text
用 bn-alpha-research 调研一下 NEX，按我们的 #Alpha新币分析 格式输出，包含盘前池子监控和私人决策备注。
```

如果你已经有项目链接或合约，也可以直接提供：

```text
用 bn-alpha-research 调研这个 BN Alpha 新币：
项目：Nexus / NEX
BSC CA：0x...
ETH CA：0x...
CMC：https://coinmarketcap.com/...
官网：https://...
X：https://x.com/...
```

---

## 4. 公共报告格式

默认标题：

```text
#Alpha新币分析｜项目名 / SYMBOL
```

默认结构：

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

重要顺序要求：

- `合约地址与链上信息` 必须放在 `基本面与叙事` 前面。
- `项目概况` 只放短信息，不写长篇叙事。
- 公开版默认不写明确估值区间和交易区间。

---

## 5. 各部分写法规范

### 一、项目概况

只包含四类信息：

- 项目名
- Token / Symbol，symbol 前加 `$`
- Alpha / 上线时间，统一转为 UTC+8
- 一句话定位

示例：

```text
一、项目概况
- 项目：Nexus
- Token：$NEX
- Alpha 时间：2026-05-20 22:00 UTC+8
- 定位：面向 AI / zkVM / verifiable computing 的计算验证网络。
```

不要在这里放：

- 官网
- X 链接
- 长篇技术介绍
- 产品细节
- 融资信息

---

### 二、合约地址与链上信息

规则：

- BSC CA 优先展示
- 然后 ETH / SOL / 其他链
- 每条只放 CA + Explorer
- 不堆 BscScan metadata
- 如果 CA 未官方确认，要明确标注风险

示例：

```text
二、合约地址与链上信息
- BSC CA：0x365de036a1f7dccb621530d517133521debb2013
  Explorer：https://bscscan.com/token/0x365de036a1f7dccb621530d517133521debb2013
- ETH CA：0xf57D49646621F563b0B905aFc8336923AC569Ec5
  Explorer：https://etherscan.io/token/0xf57D49646621F563b0B905aFc8336923AC569Ec5
```

---

### 三、基本面与叙事

写项目真正的基本面分析：

- 所属赛道
- 项目解决什么问题
- 当前叙事热度
- 产品成熟度
- 生态 / 用户 / 合作方
- 项目是否匹配当前市场偏好

要求：简洁，不写百科式长介绍。

---

### 四、Tokenomics 与流通情况

使用紧凑 block，不写散文。

示例：

```text
Tokenomics：
- 总量：100T NEX
- 初始流通：官方暂未披露
- Team：暂未披露
- Investors：暂未披露
- Treasury / Ecosystem：暂未披露

观察：官方暂未披露完整 Tokenomics，开盘前需要重点关注初始流通、空投领取时间和投资人解锁安排。
```

规则：

- 缺失就明确写 `暂未披露`
- 不猜测比例
- 最多放 3 个关键来源链接
- 如果 CMC 与官方数据不一致，以官方资料优先，并说明差异

---

### 五、团队背景

默认只写 founder / co-founder / CEO / chief scientist 等核心创始层。

LinkedIn 链接必须直接挂在人名上，不单独占一行。

推荐格式：

```text
五、团队背景
- [Daniel Marin](https://www.linkedin.com/in/danielmarin)：Co-founder / CEO，负责项目整体战略与产品方向。
- [Jens Groth](https://www.linkedin.com/in/jens-groth)：Co-founder / Chief Scientist，密码学 / zk 方向背景，负责核心技术研究。
```

不要写成：

```text
- Daniel Marin：Co-founder / CEO
  LinkedIn：https://www.linkedin.com/in/danielmarin
```

如果 LinkedIn 无法核验：

```text
- Daniel Marin：Co-founder / CEO，LinkedIn 暂无法完整核验，仅基于 RootData / 官方资料判断。
```

---

### 六、融资背景与 VC 成本推算

使用紧凑 block。

示例：

```text
融资情况：
- Seed：$xM｜Lead：...｜投资人：...
- Series A：$xM｜Lead：...｜投资人：...
- 总融资：$xM

VC 成本：
- 可计算性：无法计算
- 原因：公开资料未披露 token round valuation / FDV / 投资人 token allocation
- 对应 FDV：暂无可靠公开数据
```

VC 成本计算优先级：

1. 有 round FDV / token valuation：
   - `VC 成本价 ≈ 对应轮次 FDV / 总供应量`
2. 有融资金额 + token allocation：
   - `VC 成本价 ≈ 融资金额 / 对应分配代币数量`
3. 只有融资金额，无 valuation / allocation：
   - 不强行计算
   - 只做定性分析

要求：

- 如果能算，必须同时写 unit cost 和对应 FDV。
- 如果不能算，明确写 `无法计算`。
- 公开版不展示主观买卖区间。

---

### 七、盘前价 / 池子价

优先接入本地 `bn-alpha-monitor` 工具输出。

工具路径：

```text
/home/ubuntu/bn-alpha-monitor
```

常用命令：

```bash
PYTHONPATH=src python -m bn_alpha_monitor.cli snapshot-from-listing \
  --source binance-alpha \
  --symbol NEX \
  --no-save \
  --report-block
```

报告中的展示格式：

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

规则：

- 主池和深度估算池必须分开。
- 如果主池是 CLMM / V3 / Infinity，不要直接用主池总 TVL 推买入深度。
- 买入深度默认展示约 2x / 3x / 5x 当前 FDV。
- 每个目标 FDV 单独显示一行。
- 第三方 depth 优先于自动 AMM 估算。

第三方 depth 示例：

```text
盘前 / 池子：Nexus / $NEX
- 主池：BSC pancakeswap-infinity-clmm；当前 FDV $20.19M；流动性 $1.5M
- 买入深度：第三方链上监控显示（aLiiDeez）
  - 约 $600k 可推至 $400M FDV
  - 约 $1.08M 可推至 $1B FDV
- CEX 钱包标签命中：Coinbase / Kraken / KuCoin（链上转账观察）
- 说明：以上仅表示命中已知交易所钱包标签，不等同官方上线/充值确认
- 风险标记：单边池，价格容易被买盘快速推高；买入深度来自第三方链上监控，需二次验证
```

---

### 八、估值与开盘观察

公开版不写明确 fair value 区间。

可以写：

- 当前盘前 FDV 是否偏高 / 偏低
- 流动性是否足够
- 买入深度是否敏感
- VC 成本是否可验证
- Tokenomics 是否缺失
- 是否需要等官方补充信息

示例：

```text
当前池子 FDV 约 $19.9M，流动性约 $1.5M。由于买入深度显示几万美元级别买盘即可推至 2x / 3x / 5x FDV，开盘阶段价格发现可能较敏感，FDV 更适合作为流动性压力参考，不宜直接视为稳定估值。
```

---

### 九、主要风险

常见风险：

- Tokenomics 未披露
- 初始流通不明确
- 空投卖压
- 池子流动性薄
- CLMM 总流动性无法直接代表买入深度
- CEX 钱包标签不等同官方上线 / 充值确认
- 合约地址未官方确认
- Alpha 新币开盘波动大

---

### 十、开盘前观察重点

示例：

```text
十、开盘前观察重点
- 官方是否补充完整 Tokenomics
- BSC / ETH 合约是否与官方渠道一致
- 主池流动性是否继续增加
- 买入深度是否继续变厚
- 是否出现大额撤池或异常转账
- CEX 是否发布正式充值 / 交易公告
```

---

## 6. CEX 钱包标签写法

CEX 相关信息必须避免被误读为官方确认。

推荐写法：

```text
- CEX 钱包标签命中：Coinbase / Kraken / KuCoin（链上转账观察）
- 说明：以上仅表示命中已知交易所钱包标签，不等同官方上线/充值确认
```

不要写成：

```text
- CEX 痕迹：Coinbase 有转账痕迹，链上观察，不等同官方确认
```

---

## 7. 私人决策备注格式

私人备注可以更直接，不用于公开发布。

示例：

```text
【私人决策备注】
参与倾向：中
适合策略：小仓观察，不追高
关键观察：
- 如果开盘 FDV 快速冲到高位，但流动性没有同步增加，性价比下降
- 如果官方补充 Tokenomics 且初始流通较低，短线情绪可能更强
- 如果出现撤池 / 大额转出，需要降低参与优先级
放弃条件：
- 合约与官方信息不一致
- 池子流动性明显下降
- CEX 充值确认迟迟不出现
```

---

## 8. 数据源优先级

### 发现与上线信息

1. Binance Alpha public API / Binance Alpha 页面
2. Alpha123
3. 官方 X / 官网公告

### 合约与供应

1. 官方文档 / 官方 X / 官网
2. CoinMarketCap
3. BscScan / Etherscan
4. Dexscreener / GeckoTerminal

### 团队与融资

1. RootData API / RootData 页面
2. 官方 team 页面
3. LinkedIn
4. Crunchbase / 公开报道

### 池子与链上监控

1. 本地 `bn-alpha-monitor`
2. Dexscreener
3. GeckoTerminal
4. Dextools
5. Etherscan API V2 / BscScan via Etherscan V2
6. 可信第三方链上监控帖，但必须标注为第三方观察

---

## 9. 环境变量与密钥安全

本地工具可能使用以下环境变量：

```bash
ETHERSCAN_API_KEY=your_etherscan_api_key_here
BSCSCAN_API_KEY=your_bscscan_api_key_here
ROOTDATA_API_KEY=your_rootdata_api_key_here
BN_ALPHA_MONITOR_DATA_DIR=./data/monitor_snapshots
```

规则：

- 真实 API key 只放本地 `.env` 或安全环境变量。
- 不要提交 `.env`。
- 不要把真实 key 写进 README、测试、fixture、skill 或报告。
- 开源仓库只保留 `.env.example` 占位符。

---

## 10. 最终检查清单

生成报告前检查：

- [ ] 标题包含 `#Alpha新币分析`
- [ ] 项目概况足够短
- [ ] `$SYMBOL` 格式正确
- [ ] 时间已转为 UTC+8
- [ ] 合约信息在基本面前面
- [ ] BSC CA 优先
- [ ] 合约只放 CA + explorer
- [ ] Team 只写 founders / co-founders
- [ ] LinkedIn 直接挂在人名上
- [ ] Tokenomics 缺失时明确写未披露
- [ ] VC 成本包含 unit cost + FDV；无法计算时明确说明
- [ ] 盘前 / 池子 block 接入 monitor 工具
- [ ] 主池和深度估算池分开
- [ ] 买入深度每个 FDV 单独一行
- [ ] CEX 钱包标签不写成官方确认
- [ ] 公开版不写明确买卖区间
- [ ] 私人决策备注与公开报告分开
- [ ] 有免责声明
- [ ] 不自动发布到 Telegram
- [ ] 不写入 Obsidian / LLM Wiki，除非用户另外要求

---

## 11. 完整输出骨架

```text
#Alpha新币分析｜项目名 / SYMBOL

一、项目概况
- 项目：...
- Token：$...
- Alpha 时间：... UTC+8
- 定位：...

二、合约地址与链上信息
- BSC CA：...
  Explorer：...
- ETH CA：...
  Explorer：...

三、基本面与叙事
...

四、Tokenomics 与流通情况
Tokenomics：
- 总量：...
- 初始流通：...
- Team：...
- Investors：...
- Treasury / Ecosystem：...

五、团队背景
- [Founder Name](LinkedIn URL)：Role，背景与相关经验。
- [Co-founder Name](LinkedIn URL)：Role，背景与相关经验。

六、融资背景与 VC 成本推算
融资情况：
- ...

VC 成本：
- 可计算性：...
- 成本价：...
- 对应 FDV：...
- 限制：...

七、盘前价 / 池子价
盘前 / 池子：项目名 / $SYMBOL
- 主池：...
- 深度估算池：...
- 买入深度：...
  - 约 $x 可推至 $y FDV
  - 约 $x 可推至 $y FDV
  - 约 $x 可推至 $y FDV
- 风险标记：...

八、估值与开盘观察
...

九、主要风险
- ...

十、开盘前观察重点
- ...

免责声明：以上内容仅为个人研究记录，不构成任何投资建议。新币开盘波动较大，请自行判断风险。

【私人决策备注】
参与倾向：...
适合策略：...
关键观察：
- ...
放弃条件：
- ...
```
