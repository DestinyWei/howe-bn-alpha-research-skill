# Changelog

## [Unreleased]

### Changed

- 强化公共生图规则：`summary_dashboard`、`data_table`、`tokenomics_chart` 均默认使用 HTML/CSS → headless browser → 16:9 PNG，不再把 PIL / 手动画图作为默认路径。
- 明确公共图头部不要添加右上角装饰性 badge / pill 框；保留标题 + 简短副标题即可。
- 明确 `tokenomics_chart` 在分配数据不完整时必须生成披露状态图，不能伪造 Team / Investors / Ecosystem 占比。

# 修改记录 / Changelog

## 2026-06-21

### Added

- 新增报告前置结构：`【01｜一分钟速览】`、`【02｜关键数据卡】`、`【03｜完整调研内容】`。
- 新增可选公共总结图 / 数据表格规则：默认关闭，用户明确要求时才生成。
- 推荐公共图使用确定性 HTML/CSS 生成 16:9 横版 PNG，并在返回前做中文清晰度、裁切、页脚 QA。

### Changed

- README、SKILL、report-format、templates 同步更新到新版输出结构。
- 明确 Telegram 渲染注意事项：作者归属 quote 与 `【01｜一分钟速览】` 之间需要保留一个实际可见空行。
- 公共总结图默认不展示 CA / 合约地址，且不要写 `不展示合约地址`、`图中不展示 CA`、`合约地址已隐藏` 这类说明文字；直接省略合约地址字段。

### Notes

- 文字报告仍保留完整合约核验与正文分析；图片只做公开摘要，不替代正文。
- 私人决策备注、买卖区间、仓位建议和强交易指令不进入公共图片。
