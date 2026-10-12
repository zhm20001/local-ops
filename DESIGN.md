# 总控台 — Design (Operate · Swiss / 简洁)

锁定视觉与交互方向。实现以 `static/themes/ops.css` 令牌为准；本文件是产品层约束，改 UI 前先对照。

## Mode
**Operate**：操作台，不是营销页。偏 Swiss / Minimal — 网格对齐、高对比正文、少装饰、状态优先。

## Palette (named hex)
| Token | Light | Dark | Role |
|-------|-------|------|------|
| Room | `#EEF2F6` | `#0A0E14` | 页面底 |
| Card | `#FFFFFF` | `#131A24` | 面板 / 卡片 |
| Ink | `#17202B` | `#E6EDF3` | 主文字 |
| Ink muted | `#5F6D7A` | `#7D8A99` | 次级说明 |
| Accent | `#2F6FDE` | `#5B9DFF` | 焦点 / 主操作 |
| Run | `#127A4F` | `#3ECF8E` | 运行中 |
| Stop / Danger | `#D1453D` | `#F26D6D` | 停止、错误 |
| Warn | `#A9740A` | `#F5B544` | 端口/负载告警 |

（另有 `--line` / `--card-2` 发丝边与下沉条带；勿再引入第五套强调色作装饰。）

## Type roles
- **UI / 中文**：系统栈 `-apple-system … PingFang SC`（`--font-sans`）
- **数据 / 代码**：Geist Mono vendored（`--font-mono`）
- **禁止**：Google Fonts / CDN 字体；UI 内零 emoji 图标（用 Lucide SVG / `icons.js`）

## Layout
- 左 `.rail` + 顶栏 + 主列 / 右侧信息栏（≤1280 侧栏下沉，≤900 隐藏轨）。
- 启动台：KPI 概览 → Services 区 → Tasks 区；空态必须带一句引导 + 指向已有「添加」入口。
- 密度 dial ≈ 6/10；留白克制，不为「好看」加大卡片间距而牺牲扫描效率。

## Signature (one)
发丝边 + 柔和小圆角面板，左侧窄轨与蓝色焦点环（`--focus-ring`）。不要第二套签名装饰（无大渐变 Hero、无玻璃拟态堆叠）。

## Motion
默认 subtle（≤2/10）：短过渡 150–250ms。必须尊重 `prefers-reduced-motion: reduce`（跳过 stagger / 骨架脉冲，直接终态）。Busy 用稳定骨架或静态占位，避免闪烁 spinner。

## Anti-patterns
- 空白空态、无 CTA；把错误藏进 hover。
- 装饰性图表、彩虹状态条、emoji 当图标。
- 引入框架 / CDN / 构建链；改 `/api/*` JSON 字段「顺便优化」。
- 慢仪表盘：首屏与 2s 轮询不得被重绘整表拖垮（DOM 按 key reconcile）。

## Light / Dark
两者一等公民：`data-theme="light|dark"` + 跟随系统；同一套结构令牌，仅换色值。对比度目标正文 ≥ 4.5:1；焦点环在两模式下均可见。
