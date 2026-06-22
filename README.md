# BN Alpha 新币调研 Skill 使用说明

这个文档用于说明 `bn-alpha-research` skill 的使用方式，适合放到新的仓库作为 README / workflow 文档。

English guide: [README.en.md](README.en.md)

## 作者与来源

- 作者 / 整理：Howe
- X/Twitter：[@0xcryptoHowe](https://x.com/0xcryptoHowe)
- Telegram 频道：[cryptohowe_treasure](https://t.me/cryptohowe_treasure)
- Telegram 群组：[cyrptohowe_discussion](https://t.me/cyrptohowe_discussion)
- 微信：`Howe_Wei`（添加请备注：调研Skill）
- 灵感来源：[Alpha 调研流程 List](https://x.com/0xcryptoHowe/status/1982980551285121407)

这个 skill 是蒸馏并结合 Howe 上述推文，以及 Howe 个人 Telegram 频道中所有 Alpha 新币调研内容后，整理形成的一套 BN Alpha 新币 Pre-TGE 调研工作流。

---

## 仓库结构

```text
howe-bn-alpha-research-skill/
├── README.md                         # 中文默认文档
├── README.en.md                      # English guide
├── CHANGELOG.md                      # 修改记录
├── SKILL.md
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
- `CHANGELOG.md`：结构、视觉输出和文档规则的修改记录。
- `references/`：数据源、报告格式、HTML/CSS 公共生图规则、盘前监控工具接入说明。
- `templates/`：公开报告、前置摘要/数据卡和决策辅助重点提醒模板。
- `examples/`：完整示例输出，覆盖 `【01｜一分钟速览】`、`【02｜关键数据卡】`、`【03｜完整调研内容】` 与公开报告 1-10 节。
- `.env.example`：环境变量占位符；不要提交真实 `.env`。

---

## 首次使用：可选 API Key 引导

这个 skill **不强制要求配置 API key**。不配置也可以正常使用：agent 会继续通过公开网页、官方 X / 官网、CMC、DEX 数据源和人工交叉验证来完成调研。

但如果你希望团队 / 融资 / 链上转账等数据更稳定、更准确，建议首次安装后先配置下面三个 key：

1. `ROOTDATA_API_KEY`
   - 用途：查询项目档案、团队成员、融资轮次、投资人等信息。
   - 获取：在 RootData 官网申请 / 开通 OpenAPI，可从 [RootData API docs](https://www.rootdata.com/ApiDoc) 或 [RootData CN API docs](https://cn.rootdata.com/ApiDoc) 进入。
   - 好处：减少网页访问受限或页面结构变化导致的团队 / 融资信息缺失。

2. `ETHERSCAN_API_KEY`
   - 用途：通过 Etherscan API V2 查询 ETH 及其它支持链的合约与转账数据。
   - 获取：登录 Etherscan 后在 [API Keys 页面](https://etherscan.io/myapikey)创建 key；参考 [Etherscan API docs](https://docs.etherscan.io/)。
   - 好处：比 HTML 页面解析更稳定，适合观察 ETH 侧合约、跨链转账、CEX 钱包标签命中等链上证据。

3. `BSCSCAN_API_KEY`
   - 用途：查询 BNB Chain / BSC 上的合约与转账数据。
   - 获取：登录 BscScan 后在 API Keys 页面创建 key；也可参考 Etherscan API V2 文档中的多链说明。
   - 好处：当 BSC 数据是主链证据时，可以作为独立 key 使用，减少对 HTML fallback 的依赖。

本地配置方式：

```bash
cp .env.example .env
# 编辑 .env，填入你自己的 key
```

示例：

```bash
ROOTDATA_API_KEY=your_rootdata_api_key_here
ETHERSCAN_API_KEY=your_etherscan_api_key_here
# Optional BNB Chain override; usually not needed
BSCSCAN_API_KEY=your_bscscan_api_key_here
BN_ALPHA_MONITOR_DATA_DIR=./data/monitor_snapshots
```

安全提醒：`.env` 只保存在本地，**不要提交到 GitHub**。开源仓库只保留 `.env.example` 占位符。

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
- 决策辅助与开盘前重点提醒

默认场景是 **Pre-TGE / 上线前调研**，不是 Post-TGE 盘中交易监控。

---

## 2. 默认输出风格

默认输出为中文公开版频道草稿：使用 `#Alpha新币分析`，内容简洁，可直接复制到 Telegram，并保留免责声明。标题下方会空一行，并用引用格式展示作者归属：`> 本 BN 新币调研 Skill 由 [@0xcryptoHowe](https://x.com/0xcryptoHowe) 制作，欢迎关注反馈！`。

作者归属 quote 后面需要和 `【01｜一分钟速览】` 之间保留一个**实际可见空行**；如果 Telegram 渲染吃掉单个空行，可以在原文中多留一个 raw newline。

---

## 3. 推荐调用方式

### 3.1 调研单个 BN Alpha 新币

示例 prompt：

```text
用 bn-alpha-research 调研一下 NEX，按我们的 #Alpha新币分析 格式输出，包含盘前池子监控和决策辅助重点提醒。
```

如果你已经有项目链接或合约，也可以直接提供：

```text
用 bn-alpha-research 调研这个 BN Alpha 新币：
项目：Nexus / NEX
BSC CA：0x...
ETH CA：0x...
CMC：[CoinMarketCap 链接]
官网：[官方网站链接]
X：[官方 X 链接]
```

---

## 4. 公共报告格式

默认结构：

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

重要顺序要求：`合约地址与链上信息` 必须放在 `基本面与叙事` 前面；`项目概况` 只放短信息，不写长篇叙事。项目行末尾可追加该项目官方 X/Twitter handle 的可点击链接，不单独写 `X：` 标签。
### 前置摘要与数据卡

- `【01｜一分钟速览】`：放在作者归属 quote 后面，第一行必须说明这是 AI 基于公开资料生成的研究摘要，不代表作者本人建议，也不构成投资建议；后续使用紧凑标签行，不要写成全 bullet 列表。
- `【02｜关键数据卡】`：只抽取正文和同一证据集中已经支持的数据；缺失值写 `未披露`、`暂未发现`、`无法计算` 或 `暂无法判断`，不要为了卡片完整而编数。
- `【03｜完整调研内容】`：作为前置摘要/数据卡与原始完整正文之间的分隔符；不要在 `【01】/【02】/【03】` 标题下添加辅助副标题。

### 可选公共总结图 / 数据表格 / Tokenomics 图

默认不生成图片。只有用户明确要求“总结图 / 配图 / 数据表格 / Tokenomics 图 / 图表 / public visual”时才生成。

**统一生成方式：必须优先使用确定性的 HTML/CSS 生成 16:9 横版图，再用 headless browser 渲染为 PNG。** 不要把 PIL 手动画图、模型原生生图或 prompt-only 当成默认实现；只有在本地没有浏览器渲染能力时，才把 HTML 文件或 prompt-only 作为降级方案返回。

支持三种公共图模式：

1. `summary_dashboard`
   - 默认推荐；适合频道配图 / 横版总结图。
   - 展示项目定位、开盘时间、核心数据、风险标签和观察重点。

2. `data_table`
   - 结构化关键数据表格图。
   - 字段来自 `【02｜关键数据卡】` 与同一证据集，例如供应、流通、融资、VC 成本、盘前价、池子价、风险标签。

3. `tokenomics_chart`
   - Tokenomics 分配图。
   - 只有公开分配数据足够完整时才画 donut / bar / stacked allocation；如果分配不完整，必须生成“披露状态图”，明确标记 `待披露` / `待核验` / `无法计算`，不要编造 Team / Investors / Ecosystem 占比。

公共图片规则：

- 三种模式都要保持和 `summary_dashboard` 一致的深色 dashboard / card grid 风格。
- 图片头部保持干净：只放标题和简短副标题；不要在右上角添加装饰性 badge / pill 框，例如 `HTML/CSS 16:9`、`Public Visual`、`Data Table`、`Tokenomics`、`No Fake Ratio`。
- 不展示 CA / 合约地址，除非用户明确要求。
- 不要在图片里写 `不展示合约地址`、`图中不展示 CA`、`合约地址已隐藏` 之类说明；直接省略合约地址字段即可。
- 不展示买卖区间、仓位建议、私人参与策略或强交易指令。
- 底部保留类似 `非投资建议｜AI 基于公开资料生成｜数据以文字报告为准｜@0xcryptoHowe` 的简短 disclaimer。
- 返回图片前检查中文清晰度、无明显重叠/裁切、页脚完整；尤其注意 `overflow:hidden` 可能导致底部文字被静默裁切。


---

## 5. 各部分写法规范

### 一、项目概况

只包含四类信息：

- 项目名；如有官方 X/Twitter handle，在项目行末尾直接追加可点击链接，例如 `项目：Nexus｜[@NexusLabs](https://x.com/NexusLabs)`，不要写 `X：` 标签
- Token / Symbol，symbol 前加 `$`
- Alpha / 上线 / 空投时间，优先 Alpha123 小时级时间，统一写为 UTC+8
- 一句话定位

示例：

```text
一、项目概况
- 项目：Nexus｜[@NexusLabs](https://x.com/NexusLabs)
- Token：$NEX
- Alpha 时间：2026-05-20 22:00 UTC+8
- 定位：面向 AI / zkVM / verifiable computing 的计算验证网络。
```

不要在这里放：

- 官网
- 单独的 X 链接行（官方 handle 应放在项目行末尾）
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
  Explorer：[BscScan](https://bscscan.com/token/0x365de036a1f7dccb621530d517133521debb2013)
- ETH CA：0xf57D49646621F563b0B905aFc8336923AC569Ec5
  Explorer：[Etherscan](https://etherscan.io/token/0xf57D49646621F563b0B905aFc8336923AC569Ec5)
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
  LinkedIn：单独一行链接（不要这样写）
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

- 融资 / 孵化 / public sale / no VC allocation / 估值 FDV 等说法必须附具体来源链接，不只写“RootData 显示”这类模糊标签。
- 链接要覆盖在文字上，例如 `[RootData 项目页](url)`、`[官方 Tokenomics](url)`，不要直接贴一连串裸链接。
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
- CEX 钱包标签：如出现交易所钱包标签，按第 6 节的固定口径说明，避免写成官方确认
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

## 7. 决策辅助与重点提醒格式

公开版可以保留 `决策辅助与重点提醒`，但只做关键风险和待复核信息提醒，不输出具体交易策略、买卖价格、仓位建议或强交易指令。

示例：

```text
十、决策辅助与开盘前重点提醒
- Tokenomics：重点复核初始流通、解锁节奏、空投领取时间，判断开盘抛压是否可能集中。
- 合约与链上：复核最终 CA 是否与 Binance Alpha / 官方渠道一致，避免同名项目或临时池子误判。
- 盘前 / 池子：关注 MEXC 盘前成交量是否有效、DEX 池子流动性是否足够、主池和深度估算池是否一致。
- 融资与成本：确认融资来源、轮次估值 / FDV 口径是否可靠，避免把 equity valuation 误当 token FDV。
- CEX 与链上标签：CEX 钱包标签只作为链上观察，不等同官方充值或上线确认。
- 临开盘复核：最终 Tokenomics、CA、池子流动性、盘前价、官方公告是否有新增变化。
```

---

## 8. 数据源优先级

### 发现与上线信息

1. **Alpha123**：优先用于小时级 Alpha / 上线 / 空投时间；其界面/API 时间按 UTC+8 处理，除非来源明确标注其它时区。
2. Binance Alpha public API / Binance Alpha 页面：用于项目、日期、活动入口与最终展示交叉验证。
3. 官方 X / 官网公告：优先确认项目身份与上线日期；如果只给日期、不含小时，不覆盖 Alpha123 小时级时间。
4. 可信第三方链上监控：只能作为补充，必须标注“第三方监控”。

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

API 获取入口：

- RootData API：在 RootData 官网申请 / 开通 OpenAPI，入口可从 RootData API 文档进入：[RootData API docs](https://www.rootdata.com/ApiDoc) 或 [RootData CN API docs](https://cn.rootdata.com/ApiDoc)。用于查询项目、团队、融资、投资人等信息。
- Etherscan API：注册 / 登录 Etherscan 后，在 [API Keys 页面](https://etherscan.io/myapikey)创建 key；参考 [Etherscan API 文档](https://docs.etherscan.io/)。当前 Etherscan API V2 可通过不同 `chainid` 查询 ETH / BSC 等多链数据，本工具默认用 `ETHERSCAN_API_KEY`，如需单独覆盖 BNB Chain 可再配置 `BSCSCAN_API_KEY`。

额度说明：

- RootData API 和 Etherscan API 都有免费额度 / 免费层级可用。
- 对日常 BN Alpha 新币调研、团队融资查询、合约转账观察、池子辅助验证来说，免费额度通常已经基本够用。
- 如果后续做高频自动监控、批量扫大量项目、或多人共享服务，再考虑升级付费额度。

规则：

- 真实 API key 只放本地 `.env` 或安全环境变量。
- 不要提交 `.env`。
- 不要把真实 key 写进 README、测试、fixture、skill 或报告。
- 开源仓库只保留 `.env.example` 占位符。

---

## 10. 最终检查清单

生成报告前检查：

- [ ] 标题包含 `#Alpha新币分析`
- [ ] 标题下方空一行后，有作者归属引用行
- [ ] 项目概况足够短；项目行末尾直接追加官方 X/Twitter handle 链接，不写 `X：` 标签
- [ ] `$SYMBOL` 格式正确
- [ ] 上线 / 空投时间优先 Alpha123；Alpha123 时间按 UTC+8 写入，未重复按 UTC 转换
- [ ] 合约信息在基本面前面
- [ ] BSC CA 优先
- [ ] 合约只放 CA + explorer
- [ ] Team 只写 founders / co-founders
- [ ] LinkedIn 直接挂在人名上
- [ ] Tokenomics 缺失时明确写未披露
- [ ] 融资 / 孵化 / public sale / no VC allocation 说法有具体来源链接，并覆盖在来源文字上
- [ ] VC 成本包含 unit cost + FDV；无法计算时明确说明
- [ ] 盘前 / 池子 block 接入 monitor 工具
- [ ] 主池和深度估算池分开
- [ ] 买入深度每个 FDV 单独一行
- [ ] CEX 钱包标签不写成官方确认
- [ ] 决策辅助只做重点提醒，不写具体操作建议
- [ ] 有免责声明
- [ ] 不自动发布到 Telegram
- [ ] 不写入 Obsidian / LLM Wiki，除非用户另外要求

---

## 11. 模板文件

完整输出骨架不在 README 里重复展开，直接看模板：

- 中文公开报告：[`templates/alpha-report-template.md`](templates/alpha-report-template.md)
- 决策辅助重点提醒：[`templates/decision-reminder-template.md`](templates/decision-reminder-template.md)
- 英文版本：[`README.en.md`](README.en.md)
