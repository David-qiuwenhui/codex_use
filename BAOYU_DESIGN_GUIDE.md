# Baoyu Design 使用指南

这份文档用于快速理解和使用 `baoyu-design` Skill。它适合作为后续给 Codex、Claude Code、Cursor 等文件型 Agent 的工作说明，也可以作为你自己发起设计任务时的提示词参考。

## 1. 它是什么

`baoyu-design` 是一个面向设计产物的 Skill。它的核心产出不是普通代码功能，而是本地文件系统中的 HTML 设计稿、交互原型、PPT、文档、动效或设计系统。

它适合处理这些任务：

- UI mockup、高保真产品界面、App 页面、后台 dashboard
- 可点击交互原型、多步骤流程、多状态演示
- wireframe、低保真探索、多方案设计
- landing page、品牌页、产品展示页
- PPT / pitch deck / 演示文稿，并支持导出 PPTX
- 简历、一页纸、memo、报告等打印友好的文档
- 动效视频、产品 walkthrough、timeline animation
- 创建、导入、使用 design system / UI kit / brand tokens
- 从 Figma `.fig`、GitHub repo、HTML/CSS 页面中提取设计参考
- 导出为 PDF、独立 HTML、PPTX、视频、Canva 或 Figma

一句话概括：当任务与“设计、原型、线框图、页面、视觉探索、PPT、产品屏幕、设计系统”有关时，就应该考虑使用 `baoyu-design`。

## 2. 什么时候应该触发

可以直接在请求中点名：

```text
使用 baoyu-design 帮我做一个 AI 写作 App 的高保真原型。
```

也可以用自然语言触发：

```text
帮我做一个后台 dashboard 的交互原型。
```

```text
根据这个 PRD 做一套 8 页 pitch deck。
```

```text
把这个产品 onboarding 流程画成 wireframe，给我 3 个方向。
```

```text
基于这个 GitHub repo 的设计风格，重做设置页。
```

```text
把这个 Figma .fig 文件导入成一个可复用设计系统。
```

## 3. 推荐使用流程

### Step 1: 说明产物类型

先告诉 Agent 你要什么类型的产物：

- 高保真 UI
- 低保真 wireframe
- 可点击交互原型
- PPT / deck
- 打印文档
- 移动端原型
- 动效视频
- 设计系统

示例：

```text
使用 baoyu-design，帮我做一个移动端记账 App 的高保真交互原型。
```

### Step 2: 提供设计上下文

尽量提供以下信息：

- 产品/业务背景
- 目标用户
- 主要使用场景
- 关键页面或流程
- 参考品牌、竞品、截图、Figma、HTML、GitHub repo
- 是否已有 design system / UI kit / 品牌色 / 字体
- 需要几个方案或变体

示例：

```text
产品是给自由职业者用的轻量 CRM。目标用户是设计师、顾问、独立开发者。
请做 dashboard、客户详情页、跟进流程三个页面。
风格希望专业、清爽、有一点编辑器/工作台感，不要营销页风格。
请给 2 个视觉方向，并做成可点击原型。
```

### Step 3: 确认保存位置

`baoyu-design` 推荐把所有设计产物放在：

```text
designs/<project-name>/
```

例如：

```text
designs/freelancer-crm/
```

不要把设计 HTML、JSX、图片、字体散落在项目根目录。每个设计项目应该有自己的文件夹。

### Step 4: 选择是否使用设计系统

如果已有设计系统，可以要求 Agent 发现并使用：

```text
请先检查当前仓库里是否有可用的 design system，如果有，优先使用它。
```

如果没有，也可以明确说：

```text
这次不使用现有设计系统，请自行建立一套适合这个产品的视觉方向。
```

如果要创建新的设计系统：

```text
使用 baoyu-design 创建一个可复用的设计系统，包含 tokens、组件、示例页面和 preview.html。
```

### Step 5: 预览和验证

`baoyu-design` 的 HTML 原型应通过 HTTP 服务预览，而不是直接用 `file://` 打开。

常见预览方式：

```bash
python3 -m http.server 4311 --directory designs
```

然后访问：

```text
http://localhost:4311/<project-name>/<file-name>.html
```

如果是多文件 React/Babel 原型，这一步尤其重要，因为直接打开本地 HTML 可能导致 JSX 文件加载失败。

## 4. 常见任务模板

### 高保真交互原型

```text
使用 baoyu-design，帮我做一个高保真交互原型。

产品：
目标用户：
核心流程：
需要的页面：
视觉方向：
参考资料：
输出位置：designs/<project-name>/
要求：包含真实交互、hover/click 状态、多状态切换，并通过本地 HTTP 服务预览。
```

### Wireframe 探索

```text
使用 baoyu-design 做 wireframe 探索。

主题：
目标用户：
要探索的问题：
请给 3-5 个明显不同的结构方向。
优先关注信息架构、流程和布局，不需要高保真视觉。
输出到 designs/<project-name>/。
```

### PPT / Pitch Deck

```text
使用 baoyu-design 做一套 pitch deck。

主题：
听众：
演讲时长：
页数：
核心叙事：
已有资料：
视觉风格：
输出为 HTML deck，并在确认后导出为可编辑 PPTX。
```

默认情况下，PPTX 导出应优先使用“可编辑 PPTX”，而不是截图式 PPTX。只有在明确要求像素级还原、不可编辑也可以时，才使用截图式导出。

### 打印文档

```text
使用 baoyu-design 做一份打印友好的文档。

类型：一页纸 / 简历 / memo / 报告
内容：
目标读者：
语气：
纸张规格：默认 US Letter 或 A4
要求：屏幕可读，打印为 PDF 时版式稳定。
```

### 移动端原型

```text
使用 baoyu-design 做一个移动端原型。

设备：iPhone
场景：
页面：
交互：
要求：适合手机访问，可以添加到主屏幕。
输出为单个自包含 HTML。
```

### 从 GitHub / HTML / Figma 导入参考

```text
使用 baoyu-design，基于这个 GitHub repo 的真实 UI 代码做设计参考：
<repo-url>

请先读取真实源码和样式，不要凭记忆仿造。
然后基于它重做 <页面/流程>。
```

```text
使用 baoyu-design，读取这个本地 HTML/CSS 页面作为设计参考：
<path>

请从代码中提取颜色、字体、组件状态和布局规则，再做新的页面。
```

```text
使用 baoyu-design，导入这个 .fig 文件：
<path>

请先 outline，再选择关键 frame/component 做参考，必要时生成设计系统。
```

## 5. 产物组织建议

推荐目录结构：

```text
designs/
  project-name/
    Prototype.html
    app.jsx
    components.jsx
    data.jsx
    styles.css
    assets/
      logo.png
      hero-image.png
    _d_meta.json
```

如果绑定了设计系统，通常会出现：

```text
designs/
  project-name/
    _ds/
      <design-system-slug>/
        _ds_prompt.md
        ...
```

注意：

- 用户可见的 HTML 应放在项目目录内。
- 引用的图片、字体、音频等资产应复制到项目目录内。
- 不要从设计文件中引用项目目录外部的零散资源。
- 多文件原型要通过 HTTP 服务预览。

## 6. 设计质量要求

使用 `baoyu-design` 时，可以要求 Agent 遵守以下标准：

- 不做泛泛的模板风格。
- 不堆无意义的 placeholder、假数据、装饰图标或 filler 内容。
- 优先用真实业务内容和真实状态。
- 中文/中英混排要使用合适字体栈和行高。
- 移动端点击目标不小于 44px。
- PPT 中正文不要过小，优先保证远距离可读。
- 使用 flex/grid 和 gap 管理布局间距。
- 如果已有品牌或设计系统，优先使用其中的颜色、字体、组件和交互状态。
- 最终交付前要打开预览并检查 console/runtime 错误。

## 7. 和普通前端开发的区别

`baoyu-design` 更偏向“设计产物”，不是直接改生产代码。

它通常会：

- 在 `designs/` 下创建 HTML 原型
- 用 React + Babel 快速构建交互
- 用本地 HTTP 服务预览
- 用截图和浏览器检查视觉
- 为设计系统记录 `_d_meta.json`
- 在需要时导出 PPTX、PDF、视频或独立 HTML

如果最终要落到真实产品代码中，可以继续要求：

```text
请基于这个 baoyu-design 原型，整理一份开发交接文档。
```

或者：

```text
请把这个设计转化为当前项目中的真实组件实现。
```

## 8. 快速提示词

最短可用版本：

```text
使用 baoyu-design，帮我做一个 <产品/页面/流程> 的 <高保真原型/wireframe/PPT/文档>。
输出到 designs/<project-name>/，通过本地 HTTP 预览并检查无报错。
```

更完整版本：

```text
使用 baoyu-design 做一个 <产物类型>。

背景：
目标用户：
核心目标：
页面/内容范围：
视觉方向：
参考资料：
是否使用设计系统：
需要几个方案：
输出位置：designs/<project-name>/

请先确认关键问题，然后创建 HTML 设计产物，通过 HTTP 服务预览，检查加载和交互无错误后交付。
```

## 9. 给 Agent 的执行约束

当 Agent 执行 `baoyu-design` 任务时，应遵守：

1. 先读取 `baoyu-design/SKILL.md`。
2. 再读取 `system-prompt.md`。
3. 在 Codex 环境中读取 `references/codex.md`。
4. 根据任务类型读取对应的 `built-in-skills/*.md`。
5. 新项目应询问关键设计问题，而不是直接假设方向。
6. 输出放到 `designs/<project-name>/`。
7. 如果使用设计系统，要导入到 `_ds/<slug>/`，读取 `_ds_prompt.md` 并遵守其视觉约束。
8. 所有用户可见产物都要记录为项目资产。
9. 通过 HTTP 服务预览，不用 `file://` 直接打开。
10. 完成前检查页面加载、交互和控制台错误。

## 10. 一句话记忆

`baoyu-design` 是把 Agent 变成“本地设计工作室”的 Skill：先理解上下文，再选择设计流程，最后产出可预览、可迭代、可导出的 HTML 设计资产。
