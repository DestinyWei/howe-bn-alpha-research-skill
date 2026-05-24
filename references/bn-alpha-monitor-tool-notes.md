# BN Alpha Monitor 工具接入说明

本 skill 可接入本地 BN Alpha 盘前池子监控工具：

```text
/home/ubuntu/bn-alpha-monitor
```

## 常用命令

### 从 Binance Alpha listing 自动生成报告块

```bash
cd /home/ubuntu/bn-alpha-monitor
PYTHONPATH=src python -m bn_alpha_monitor.cli snapshot-from-listing \
  --source binance-alpha \
  --symbol NEX \
  --no-save \
  --report-block
```

### 手动指定合约并抓 explorer

```bash
cd /home/ubuntu/bn-alpha-monitor
PYTHONPATH=src python -m bn_alpha_monitor.cli snapshot \
  --symbol NEX \
  --name Nexus \
  --bsc-ca <BSC_CA> \
  --eth-ca <ETH_CA> \
  --total-supply <TOTAL_SUPPLY> \
  --fetch-explorer \
  --no-save \
  --report-block
```

## 输出格式要求

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

## 规则

- 默认买入深度档位：约 2x / 3x / 5x 当前 FDV。
- 每个目标 FDV 单独一行。
- 主池和深度估算池必须分开。
- 如果主池是 CLMM/V3/Infinity，不用总 TVL 直接估算深度。
- 普通 AMM 深度估算只适合 constant-product `x*y=k` 池。
- 第三方 depth 优先，但必须标注来源。

## 环境变量

工具可能读取：

```bash
ETHERSCAN_API_KEY=your_etherscan_api_key_here
BSCSCAN_API_KEY=your_bscscan_api_key_here
BN_ALPHA_MONITOR_DATA_DIR=./data/monitor_snapshots
```

API 获取与额度：

- Etherscan API：注册 / 登录后在 `https://etherscan.io/myapikey` 创建 key，文档见 `https://docs.etherscan.io/`。Etherscan API V2 支持通过 `chainid` 查询 ETH / BSC 等多链数据；本工具默认读取 `ETHERSCAN_API_KEY`，`BSCSCAN_API_KEY` 仅作为 BNB Chain 覆盖项。
- Etherscan API 有免费额度，日常 BN Alpha 新币调研中的转账观察、合约辅助验证基本够用；只有高频自动监控或批量扫描时才通常需要更高额度。

不要提交真实 `.env`。
