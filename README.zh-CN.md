# Listening Atlas Agent Kit（聆听图谱 Agent Kit）

这是一套文档优先的工具包，用来让具备浏览器或 computer-use 能力的 AI agent 在任意音乐平台上生成古典音乐歌单、听音指南和静态 HTML 电子书。

English README: [README.md](README.md).

## 这个仓库是什么

这个仓库不是自动化代码项目，而是一套 agent kit：它包含 prompts、specs、检查清单、模板和样本输出。用户可以把这些文件交给 Codex、Claude Code 或其他 browser/computer-use agent，让 agent 按文档执行。

核心目标是平台无关。用户应该能够用同一套编辑方法，在 Apple Music、Spotify、YouTube Music、YouTube、TIDAL、网易云音乐或其他平台上生成自己的歌单和指南。

## 包含内容

- `docs/`：工作流和 QA 检查清单。
- `specs/`：数据 schema 和发布规范。
- `prompts/`：可直接复制给 agent 的 prompts。
- `templates/`：project brief、playlist row 和 asset manifest 模板。
- `products/zh-CN/`：中文成品指南和歌单。
- `products/en/`：英文成品指南和歌单。
- `site/`：带语言切换的 GitHub Pages 静态电子书原型。
- `samples/`：原始 Apple Music 案例材料。
- GitHub Releases：中英文成品 ZIP 下载包。

## 快速开始

如果你想用这个仓库制作自己的歌单：

1. 下载或 clone 这个仓库。
2. 把这些文件交给你的 agent：
   - `docs/USAGE.md`
   - `docs/PLAYBOOK.md`
   - `templates/project_brief.template.md`
   - `specs/PLAYLIST_SCHEMA.md`
   - `specs/PLATFORM_ADAPTERS.md`
   - `prompts/` 中与你当前阶段匹配的 prompt
3. 让 agent 根据你的目标读者、语言、平台和曲目数量填写 project brief。
4. 让 agent 生成平台无关的 playlist TSV。
5. 让 browser/computer-use agent 在你选择的音乐平台上逐条执行 TSV。
6. 让 agent 写指南并生成静态 HTML 电子书。
7. 发布前执行 QA 检查清单。

详细步骤见 [docs/USAGE.md](docs/USAGE.md)。

## 成品

仓库里有两套独立成品：

- 中文：`products/zh-CN/classical_atlas_guide.zh-CN.md` 和 `products/zh-CN/classical_atlas_playlist.zh-CN.tsv`
- 英文：`products/en/classical_atlas_guide.en.md` 和 `products/en/classical_atlas_playlist.en.tsv`

发布 ZIP 包会上传到 GitHub Release 页面，作为用户可下载的成品文件。本地可以用 `release-assets/` 暂存这些 ZIP，但该目录不提交进仓库。

## GitHub Pages

`site/` 目录包含静态 HTML 电子书原型：

- `site/index.html`：中文版
- `site/en/index.html`：英文版

每个页面右上角都有语言切换链接。正式发布时，可以用 GitHub Pages workflow 部署 `site/`，也可以把 `site/` 的内容复制到仓库实际用于 Pages 的分支或目录。

## 素材政策

本项目采用保守的开源发布政策：

- 打包图片必须是公有领域、CC0，或明确可在兼容开放授权下复用。
- Wikimedia Commons 文件必须逐图确认授权、作者、来源和署名。
- The Met Open Access / CC0 优先用于公版艺术作品插图。
- Spotify、TIDAL、Apple Music、YouTube、网易云音乐等平台提供的专辑封面、音乐家照片、缩略图和 metadata 只做链接或用户本地生成说明，不打包进仓库。
- 所有打包视觉素材必须先进入 asset manifest。

## 授权

除另有说明外，本仓库原创文档、prompts、specs、模板、样本数据和生成的指南文字采用 [CC BY 4.0](LICENSE.md) 授权。

第三方来源保留各自授权和条款。本仓库不提供法律建议。
