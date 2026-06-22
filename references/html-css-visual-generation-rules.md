# HTML/CSS public visual generation rules

Use these rules whenever generating public images for `bn-alpha-research`.

## Required path

- Default output path: self-contained HTML/CSS → headless browser → 16:9 PNG.
- Do not use PIL/manual drawing, model-native image generation, or prompt-only output as the default when a browser renderer is available.
- Browser fallback: if no renderer is available, return the HTML file or a prompt-only brief and clearly label it as a fallback.

## Supported modes

- `summary_dashboard`: default channel-ready public summary image.
- `data_table`: structured key-data table image sourced from `【02｜关键数据卡】` and the same evidence set.
- `tokenomics_chart`: tokenomics allocation chart when allocation data is complete. If allocation data is incomplete, render a disclosure-status chart and label missing fields as `待披露` / `待核验` / `无法计算`; never invent allocation percentages.

## Shared visual standard

- 16:9 landscape.
- Dark dashboard background, card grid, strong section numbers, colored accents, readable Chinese typography.
- Footer disclaimer such as `非投资建议｜AI 基于公开资料生成｜数据以文字报告为准｜@0xcryptoHowe`.
- Header should be clean: title + concise subtitle only.
- Do not add decorative top-right badge / pill boxes such as `HTML/CSS 16:9`, `Public Visual`, `Data Table`, `Tokenomics`, or `No Fake Ratio`.

## Public-safety rules

- Use only public-facing report content from `【01｜一分钟速览】` and `【02｜关键数据卡】`.
- Exclude private decision notes, buy/sell bands, position sizing, and strong trading instructions.
- Do not show CA / contract addresses by default. Chain names are enough for public images.
- Do not write meta-placeholder text like `不展示合约地址`; simply omit the field.

## QA checklist

Before returning or committing generated examples:

- Confirm the image is rendered from HTML/CSS at 16:9.
- Visually inspect for Chinese legibility, mojibake, overlap, cropped bottom lines, and complete footer.
- Check that no full or shortened contract address appears. The footer handle `@0xcryptoHowe` is allowed.
- For tokenomics visuals, verify missing allocation data is labeled as missing and not replaced with made-up percentages.
- If `overflow:hidden` is used, inspect the rendered PNG carefully; shorten content or increase card height if any lower line is clipped.
