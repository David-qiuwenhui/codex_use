# Baoyu Skills 使用指南

这份文档介绍从 `JimLiu/baoyu-skills` 安装的一组宝玉 Skills，方便后续快速判断“什么时候该用哪个 Skill、怎么发起任务、需要注意什么”。

> 安装位置：`~/.codex/skills/baoyu-*`
>
> 注意：新安装的 Skills 通常需要重启 Codex 后才会进入可用 Skill 列表。

## 1. 总体定位

`baoyu-skills` 是一组面向内容生产、内容转换、视觉生成和社交发布的专用工作流 Skills。它们不是一个单一能力，而是一套按场景拆分的工具箱。

它大致覆盖这些工作：

- 把网页、X/Twitter、YouTube、微信群聊等内容提取成 Markdown 或摘要
- 翻译、格式化、转换 Markdown 到 HTML
- 生成封面图、文章插图、信息图、小红书图片、漫画、幻灯片图片
- 压缩图片、生成图片、画专业 SVG 图表
- 发布内容到微信公众号、微博、X
- 提取 Electron 应用资源和源码

最简单的使用方式是在请求里直接点名 Skill：

```text
使用 baoyu-url-to-markdown，把这个网页保存成 Markdown：<url>
```

也可以通过自然语言触发：

```text
帮我下载这个 YouTube 视频的字幕，并整理成 Markdown。
```

## 2. Skill 分类速查

### 内容获取与转写

| Skill | 适合场景 |
| --- | --- |
| `baoyu-url-to-markdown` | 把网页保存成 Markdown，支持通用网页、X/Twitter、YouTube、Hacker News 等适配 |
| `baoyu-danger-x-to-markdown` | 使用逆向 API 把 X/Twitter 推文或文章转换成 Markdown |
| `baoyu-youtube-transcript` | 下载 YouTube 字幕、转写、封面图，支持多语言、章节、翻译 |
| `baoyu-wechat-summary` | 总结微信群聊精华，维护群聊历史、用户画像和群记忆 |

### 文本处理与转换

| Skill | 适合场景 |
| --- | --- |
| `baoyu-translate` | 翻译、精翻、本地化，支持 quick / normal / refined 三种模式和术语表 |
| `baoyu-format-markdown` | 把普通文本或 Markdown 美化为结构化文章 |
| `baoyu-markdown-to-html` | 把 Markdown 转为适合阅读或公众号排版的 HTML |

### 视觉与图片生成

| Skill | 适合场景 |
| --- | --- |
| `baoyu-image-gen` | 通用 AI 图片生成后端，支持多提供商、参考图、比例、批量生成 |
| `baoyu-cover-image` | 生成文章封面图，支持不同画幅、配色、渲染风格、情绪 |
| `baoyu-article-illustrator` | 分析文章结构，为文章自动规划并生成插图 |
| `baoyu-infographic` | 生成专业信息图，适合高密度信息总结和可视化 |
| `baoyu-xhs-images` | 生成小红书/微信图文风格的系列图片卡片 |
| `baoyu-comic` | 生成知识漫画、教育漫画、人物故事漫画或教程漫画 |
| `baoyu-slide-deck` | 根据内容生成专业幻灯片图片 |
| `baoyu-diagram` | 输出专业暗色主题 SVG 图表，如架构图、流程图、时序图、关系图 |
| `baoyu-compress-image` | 压缩图片，默认转 WebP，也支持 PNG/JPEG |

### 社交发布

| Skill | 适合场景 |
| --- | --- |
| `baoyu-post-to-wechat` | 发布微信公众号文章或图片贴图 |
| `baoyu-post-to-weibo` | 发布微博、图片、视频或微博头条文章 |
| `baoyu-post-to-x` | 发布 X/Twitter 推文、图片、视频或长文 |

### 工具与逆向

| Skill | 适合场景 |
| --- | --- |
| `baoyu-electron-extract` | 提取 Electron 应用 `.asar` 资源、JS、source map，还原或格式化源码 |
| `baoyu-danger-gemini-web` | 通过逆向 Gemini Web API 做文本或图片生成 |

### 设计类

| Skill | 适合场景 |
| --- | --- |
| `baoyu-design` | 生成 HTML 设计稿、交互原型、wireframe、PPT、文档、设计系统 |

`baoyu-design` 已经有单独说明文档：`BAOYU_DESIGN_GUIDE.md`。

## 3. 常用工作流

### 网页到 Markdown

适合保存文章、网页资料、线程内容。

```text
使用 baoyu-url-to-markdown，把这个网页转换成 Markdown：
<url>

要求：
- 保留标题、作者、发布时间
- 下载或保留图片请先询问
- 输出到 url-to-markdown/
```

如果是 X/Twitter 内容，并且普通读取失败，可以考虑：

```text
使用 baoyu-danger-x-to-markdown，把这个 X 链接保存为 Markdown：
<x-url>

我同意使用逆向 API。
```

### YouTube 字幕与封面

```text
使用 baoyu-youtube-transcript，下载这个 YouTube 视频的字幕：
<youtube-url>

要求：
- 优先中文，其次英文
- 保留时间戳
- 按章节整理
- 同时下载视频封面
```

常见变体：

```text
请把字幕翻译成简体中文，并输出 Markdown。
```

```text
请列出这个视频可用的字幕语言。
```

### 翻译与精翻

`baoyu-translate` 有三种模式：

| 模式 | 用法 | 适合场景 |
| --- | --- | --- |
| quick | 快速直译 | 短文本、临时理解 |
| normal | 分析后翻译 | 普通文章、博客、说明文 |
| refined | 分析、翻译、审校、润色 | 重要文章、公开发布内容 |

示例：

```text
使用 baoyu-translate，把这篇文章精翻成中文。

模式：refined
读者：中文技术读者
风格：准确、自然、有出版感
术语：AI agent 翻译为“智能体”，workflow 翻译为“工作流”
输入：<file-or-url>
```

第一次使用时，它可能要求创建 `EXTEND.md` 偏好文件，用来保存目标语言、模式、读者、术语表等默认配置。

### Markdown 美化与 HTML 转换

格式化 Markdown：

```text
使用 baoyu-format-markdown，帮我把这篇文章整理成结构清晰的 Markdown。

要求：
- 添加合适标题层级
- 提炼摘要
- 保留代码块
- 输出为 <filename>-formatted.md
```

转成 HTML：

```text
使用 baoyu-markdown-to-html，把这篇 Markdown 转成适合微信公众号排版的 HTML。

要求：
- 支持代码高亮
- Mermaid 图转图片
- 外链转底部引用
```

### 文章配图

适合长文章、教程、观点文、公众号文章。

```text
使用 baoyu-article-illustrator，给这篇文章规划并生成插图。

要求：
- 先分析文章结构
- 推荐需要插图的位置
- 每张图先写 prompt 文件
- 生成前让我确认风格和数量
输入：<article-file>
```

这个 Skill 会用“类型 × 风格 × 配色”的方式保证插图一致性。

### 封面图

```text
使用 baoyu-cover-image，为这篇文章生成封面图。

标题：
副标题：
主题：
画幅：16:9
风格：克制、科技、人文感
要求：先给 3 个方向，确认后再生成。
```

常见画幅：

- `2.35:1`：电影感横幅
- `16:9`：通用文章封面
- `1:1`：社交平台方图

### 信息图

```text
使用 baoyu-infographic，把这份内容生成一张专业信息图。

输入：<content>
目标：帮助读者快速理解核心结构
风格：深色、专业、适合技术文章
要求：先推荐 layout × style 组合，再生成。
```

适合：

- 研究报告摘要
- 流程、框架、模型说明
- 数据或观点浓缩
- 复杂概念视觉化

### 小红书/微信图片卡片

```text
使用 baoyu-xhs-images，把这篇内容做成 6 张小红书图片卡片。

要求：
- 适合社交传播
- 每张卡片一个核心观点
- 风格活泼但不幼稚
- 先确认标题、张数、风格和配色
```

适合：

- 小红书种草图
- 微信图文卡片
- 知识点拆解
- 社交平台系列图

### 知识漫画

```text
使用 baoyu-comic，做一篇知识漫画。

主题：
目标读者：
页数：
风格：
语气：
要求：
- 先输出分镜和角色设定
- 确认后再生成图片
```

适合：

- 教程漫画
- 人物传记漫画
- 概念解释漫画
- 教育内容漫画

### 画专业图表

```text
使用 baoyu-diagram，画一个系统架构图。

内容：
风格：暗色、专业、适合技术文档
输出：standalone SVG
```

适合：

- 架构图
- 流程图
- 时序图
- 状态机
- 组织结构图
- 决策树
- 数据流图
- 模块关系图

注意：`baoyu-diagram` 输出的是 SVG，不是位图。

### 生成幻灯片图片

```text
使用 baoyu-slide-deck，根据这份内容生成一套幻灯片图片。

主题：
听众：
页数：
风格：
要求：
- 先生成大纲和每页设计说明
- 确认后逐页生成图片
```

如果你需要可编辑 HTML/PPTX deck，更适合用 `baoyu-design`。

### 压缩图片

```text
使用 baoyu-compress-image，压缩这个目录里的图片：
./images

要求：
- 递归处理
- 输出 WebP
- 质量 80
- 保留原图
```

常见 CLI 形态：

```bash
bun ~/.codex/skills/baoyu-compress-image/scripts/main.ts ./images -r -q 80 --keep
```

如果没有 `bun`，部分 Skills 会尝试使用 `npx -y bun`。

### 发布到平台

微信公众号：

```text
使用 baoyu-post-to-wechat，把这篇 Markdown 发布到微信公众号草稿。

要求：
- 外链转底部引用
- 保留图片
- 发布前让我确认标题、摘要和封面
```

微博：

```text
使用 baoyu-post-to-weibo，发布这条微博。

内容：
图片：
要求：发布前先预览。
```

X/Twitter：

```text
使用 baoyu-post-to-x，发布这条推文。

内容：
图片：
要求：使用 Chrome 登录态，发布前确认。
```

这类发布 Skill 通常依赖平台登录态、API token、Chrome CDP 或浏览器自动化。发布前建议显式要求“先预览，不要直接发布”。

## 4. 配置与偏好文件

很多 Baoyu Skills 支持 `EXTEND.md` 偏好文件。查找优先级通常是：

1. 当前项目：`.baoyu-skills/<skill-name>/EXTEND.md`
2. XDG 配置：`${XDG_CONFIG_HOME:-$HOME/.config}/baoyu-skills/<skill-name>/EXTEND.md`
3. 用户目录：`$HOME/.baoyu-skills/<skill-name>/EXTEND.md`

常见可配置项包括：

- 默认输出目录
- 默认语言
- 翻译模式和术语表
- 图片生成后端
- 图片风格、批量大小
- 是否下载媒体资源
- 发布平台参数

第一次使用某些 Skill 时，如果没有 `EXTEND.md`，它会要求先完成偏好设置。不要让 Agent 静默创建默认配置；应让它询问后再写入。

## 5. 图片生成后端

多个视觉类 Skills 会调用图片生成后端，例如：

- `baoyu-image-gen`
- Codex 原生 `imagegen`
- Gemini / OpenRouter / DashScope / Replicate 等

通用规则：

- 生成前通常要先写 prompt 文件，便于复现。
- 默认应先确认风格、数量、画幅、配色，再开始生成。
- 不要用 SVG、HTML、Canvas 冒充位图生成结果。
- 如果图片里的文字错误，应重新生成或减少图中文字，不要用脚本覆盖修补。
- 批量生成时，先准备所有 prompt，再分批生成。

常用提示：

```text
请先把每张图的 prompt 保存到 prompts/，我确认后再生成。
```

```text
使用 Codex 原生 imagegen 作为图片后端。
```

```text
直接生成，不用确认。采用 16:9、深色科技风、批量 4 张。
```

## 6. 需要额外依赖的场景

部分 Skills 依赖本机工具：

| 依赖 | 相关 Skill | 说明 |
| --- | --- | --- |
| `bun` 或 `npx -y bun` | 多数 CLI 型 Skills | 用于运行 TypeScript 脚本 |
| Chrome / Chrome CDP | 网页抓取、发布、部分转换 | 可能需要登录态或人工处理验证码 |
| `wx` | `baoyu-wechat-summary` | 需要本机安装并初始化 `wx-cli` |
| 图片处理工具 | `baoyu-compress-image` | 会自动选择 `sips`、`cwebp`、ImageMagick、Sharp 等 |

如果缺少依赖，应该让 Agent 先检查环境并给出安装建议，而不是盲目继续。

## 7. 安全与权限注意

名称中带 `danger` 的 Skills 需要格外注意：

- `baoyu-danger-gemini-web`
- `baoyu-danger-x-to-markdown`

它们通常使用逆向接口或非官方 Web API。使用前应明确：

- 用户是否同意使用该方式
- 是否涉及账号登录态、Cookie、token
- 是否可能违反目标平台规则
- 是否有官方 API 或普通网页读取方式可替代

建议提示词：

```text
如果需要使用 danger 类 Skill，请先说明风险并征求我同意。
```

发布类 Skills 也建议默认走“草稿/预览”：

```text
不要直接发布，先生成草稿或预览，等我确认后再发布。
```

## 8. 快速触发词

| 你想做什么 | 推荐说法 |
| --- | --- |
| 保存网页 | `使用 baoyu-url-to-markdown，把这个网页保存成 Markdown` |
| 下载 YouTube 字幕 | `使用 baoyu-youtube-transcript，下载这个视频字幕` |
| 翻译文章 | `使用 baoyu-translate，精翻这篇文章` |
| 美化 Markdown | `使用 baoyu-format-markdown，整理这篇 Markdown` |
| Markdown 转公众号 HTML | `使用 baoyu-markdown-to-html，转成微信排版 HTML` |
| 生成文章封面 | `使用 baoyu-cover-image，为这篇文章生成封面图` |
| 文章自动配图 | `使用 baoyu-article-illustrator，为文章规划并生成插图` |
| 做信息图 | `使用 baoyu-infographic，生成一张信息图` |
| 做小红书卡片 | `使用 baoyu-xhs-images，生成 6 张图片卡片` |
| 做知识漫画 | `使用 baoyu-comic，做一篇知识漫画` |
| 画架构图 | `使用 baoyu-diagram，画一个架构图，输出 SVG` |
| 压缩图片 | `使用 baoyu-compress-image，压缩这个图片目录` |
| 发公众号 | `使用 baoyu-post-to-wechat，生成公众号草稿` |
| 发微博 | `使用 baoyu-post-to-weibo，发布前先预览` |
| 发 X | `使用 baoyu-post-to-x，用 Chrome 登录态发推，先确认` |
| 总结微信群聊 | `使用 baoyu-wechat-summary，总结这个群最近 7 天精华` |
| 提取 Electron 应用 | `使用 baoyu-electron-extract，提取这个 Electron 应用源码` |

## 9. 推荐组合工作流

### 网页文章转公众号

```text
1. 使用 baoyu-url-to-markdown 保存网页。
2. 使用 baoyu-format-markdown 整理文章结构。
3. 使用 baoyu-cover-image 生成封面。
4. 使用 baoyu-article-illustrator 规划插图。
5. 使用 baoyu-markdown-to-html 转为公众号 HTML。
6. 使用 baoyu-post-to-wechat 生成公众号草稿，发布前确认。
```

### YouTube 视频变文章

```text
1. 使用 baoyu-youtube-transcript 下载字幕和封面。
2. 用普通 Agent 能力整理为文章大纲。
3. 使用 baoyu-translate 翻译或本地化。
4. 使用 baoyu-format-markdown 美化。
5. 使用 baoyu-cover-image / baoyu-infographic 生成配图。
```

### 长文变社交传播素材

```text
1. 使用 baoyu-format-markdown 整理长文。
2. 使用 baoyu-infographic 生成总览信息图。
3. 使用 baoyu-xhs-images 生成 5-8 张卡片。
4. 使用 baoyu-post-to-weibo 或 baoyu-post-to-x 发布前预览。
```

### 技术文章配图

```text
1. 使用 baoyu-diagram 画架构图或流程图。
2. 使用 baoyu-article-illustrator 规划文章插图。
3. 使用 baoyu-cover-image 生成封面。
4. 使用 baoyu-compress-image 压缩所有输出图片。
```

## 10. 给 Agent 的执行约束

当你要求 Agent 使用这些 Skills 时，可以附加以下约束：

```text
执行要求：
- 先读取对应 Skill 的 SKILL.md。
- 如果 Skill 有 references/ 或 EXTEND.md 规则，按需读取。
- 如果需要首次配置，先问我，不要静默写默认值。
- 如果涉及发布、登录态、逆向接口、danger 类 Skill，先说明风险并征求确认。
- 如果涉及图片生成，先保存 prompt 文件，再调用图片后端。
- 如果涉及平台发布，默认只生成草稿或预览，不要直接发布。
- 完成后告诉我输出文件路径和关键结果。
```

## 11. 一句话记忆

`baoyu-skills` 是一套“内容生产流水线”Skills：先把外部内容抓取成结构化文本，再翻译、整理、视觉化，最后生成可发布的文章、图片、幻灯片或社交平台草稿。
