# Listening Atlas Agent Kit（聆听图谱 Agent Kit）

Listening Atlas 是一套文档优先的 agent kit，用来让具备浏览器或 computer-use 能力的 AI agent 生成音乐聆听指南、有顺序的歌单和静态 HTML 电子书。它适合交给 Codex、Claude Code，以及其他能读文件、浏览网页、操作流媒体界面的 agent。

English README: [README.md](README.md).

<p align="center">
  <img src="docs/assets/classical-atlas-playlist-sketch.png" alt="古典音乐图谱歌单界面的手绘风预览" width="720">
</p>

## 这个仓库是什么

这个仓库给 agent 提供编辑流程、数据 contract、prompts 和 QA 检查方式。真正可复用的 kit 在 [docs/](docs)、[specs/](specs)、[prompts/](prompts) 和 [templates/](templates) 里。仓库不发布平台自动化脚本。

仓库里的参考成品是 **Classical Atlas / 古典音乐图谱**。它包含中英文指南、歌单 TSV、Apple Music 执行日志、release ZIP 和 GitHub Pages 电子书。它的作用是展示这套 kit 可以生成什么结果，不是限制你只能做古典音乐或 Apple Music。Kit 本身是平台无关的；Classical Atlas demo 是 Apple Music case-study edition。

## 快速开始

下载或 clone 这个仓库。然后给你的 agent 一个入口文件：

```text
先读 docs/AGENT_HANDOFF.md，并把它作为这个仓库的入口。
请帮我为 [音乐类型或领域] 生成一份聆听指南、playlist TSV，并在指定平台创建真实歌单。
目标平台：[Apple Music / Spotify / YouTube Music / YouTube / TIDAL / 网易云音乐 / 其他]。
目标规模：约 [50 / 100 / 180] 首。
语言：[中文 / 英文 / 其他]。
如果 project brief 还缺信息，先问我；然后按这个 kit 执行。
```

`AGENT_HANDOFF.md` 会告诉 agent 接下来该读哪些 docs、specs、templates 和 prompts。你不需要在第一条消息里塞一长串文件名。面向人类用户的完整说明见 [docs/USAGE.md](docs/USAGE.md)。

## 可以怎么定制

一次生成会先从 project brief 开始。Agent 应该询问音乐领域、目标读者、语言、平台、曲目数量、难度比例、地区覆盖，以及是否包含当代音乐、电影、游戏或其他屏幕音乐。这些选择会进入歌单 schema、指南大纲、平台搜索策略和 QA 检查。

如果你做古典音乐，可以参考仓库里的 Classical Atlas 成品。如果你要做 jazz、rock、歌剧传统、电影音乐、游戏音乐、地区民间音乐或其他领域，核心交付物保持不变；当这个领域需要不同 metadata 时，再使用 extension 层。Extension 的规则在 [specs/EXTENSION_CONTRACT.md](specs/EXTENSION_CONTRACT.md)，示例在 [specs/extensions/](specs/extensions)。

## 交付物

一次完整 agent run 应该产出 project brief、平台无关的 playlist TSV、真实平台执行后的 execution log、Markdown 指南、静态 HTML 电子书，以及在打包图片时必须提供的 asset manifest。具体文件名和验收规则见 [specs/DELIVERABLES.md](specs/DELIVERABLES.md)。

Classical Atlas demo 已经发布在 GitHub Pages，并提供 release ZIP。ZIP 是成品 demo 包。你要用这套 kit 做自己的项目时，应该从仓库里的 docs、specs、prompts 和 templates 开始，而不是从 demo ZIP 开始。

## 素材和发布

这个 kit 采用保守的开源发布策略。打包图片应当是 public domain、CC0，或明确可以在兼容开放授权下复用。每张图片都要在 asset manifest 里记录 source、creator、license、attribution 和 reuse notes。平台专辑封面、音乐人照片、缩略图和平台截图不应直接复制进仓库；可以链接，或重新绘制成不依赖平台素材的泛化插图。

## 授权

`docs/`、`specs/`、`prompts/` 和 `templates/` 中的可复用 agent kit 材料采用 [CC0 1.0](LICENSE.md)。成品 demo、样本指南文字、样本歌单数据和站点指南内容采用 [CC BY 4.0](LICENSE.md)，除非具体文件另有说明。

第三方来源保留各自授权和条款。本仓库不提供法律建议。
