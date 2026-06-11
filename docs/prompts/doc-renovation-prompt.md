# 仓库文档规范化提示词

> 用途：当你发现一个 GitHub 仓库的 README 和文档存在渲染问题、语言混乱、缺少导航链接时，使用本提示词让 AI 代理一次性修复。
> 适用场景：接手新仓库、文档重构、多语言整理、GitHub Pages 配置。

---

## 提示词模板

```
请对仓库 [仓库名/URL] 的文档进行规范化整改，解决以下问题：

1. 根目录 README 是英文的，但项目主要受众是中文用户；
2. docs/ 或其他自定义目录下的 Markdown 文件在 GitHub 上渲染异常、排版混乱；
3. 文档之间缺少互相跳转的导航链接，README 不引用 docs，docs 不返回 README；
4. 内容存在错别字、语句不通顺、中英混杂。

请按以下步骤执行：

## 第一步：摸底

先读取以下内容并汇报问题清单：
- 根目录 README.md
- docs/ 目录下所有 Markdown 文件（如有多语言 lang/ 子目录也一并读取）
- 检查是否存在 _config.yml
- 检查所有文档中的相对路径引用是否有效（图片、PDF、内部链接）
- 识别错别字和别扭的中英文表达

汇报格式：
```
问题清单：
1. [文件路径] — [具体问题描述]
2. ...
```

## 第二步：创建 GitHub Pages 配置

如果仓库没有 _config.yml，在根目录创建：

```yaml
# GitHub Pages 配置
title: [项目名称]
description: [项目一句话简介]
markdown: GFM
plugins:
  - jekyll-relative-links
relative_links:
  enabled: true
  collections: true
include:
  - docs/
  - docs/lang/
  - docs/assets/
```

## 第三步：重写根目录 README

如果根目录 README 是英文而项目主要面向中文用户：
- 将其重写为中文标准版
- 保留必要的英文术语（如项目名称、API 名词）
- 添加一个"深度阅读"或"相关文档"章节，列出 docs/ 下所有文档并附链接
- 保持 badges、star history 等社区元素不变
- 修正所有相对路径引用，确保从根目录出发能正确解析

如果 README 中引用 docs/assets/ 下的图片，路径示例：`docs/assets/xxx.png`

## 第四步：修复 docs/ 下的文档文件

对 docs/ 下每个 Markdown 文件：
- 确保内容在 GitHub 上能正常渲染（避免不兼容的 HTML 标签、过长行）
- 修正所有相对路径引用（图片、PDF、内部链接）
- 在文件末尾添加导航链接：

```markdown
---

[← 返回主 README](../README.md) · [📋 其他文档 →](other-doc.md)
```

英文文档使用：

```markdown
---

[← Back to main README](../README.md) · [📋 Other Doc →](other-doc.md)
```

## 第五步：处理多语言文档

如果 docs/lang/ 下有多个语言版本：
- 在根目录 README 的语言切换链接中，指向 docs/lang/ 下对应版本
- 在每个语言文档顶部添加提示：

```
> 📌 The primary README has moved to [README.md](../../README.md).
```

中文版：

```
> 📌 中文 README 主版本已移至根目录 [README.md](../../README.md)。
```

- 在末尾添加返回主 README 的导航链接

## 第六步：修正错别字和语句

逐文件扫描以下常见问题并修正：
- 中英文之间缺少空格（如"这是一个Skill" → "这是一个 Skill"）
- 全角半角标点混用
- 错别字（如"即然" → "既然"、"部暑" → "部署"）
- 不通顺的长句（拆分成短句）
- 不一致的术语（同一概念全文统一译名）

## 第七步：提交规范

使用以下格式提交：

```
docs: [一句话概括改动]

- [具体改动条目]
- [具体改动条目]
- ...
```

## 质量检查清单

提交前确认以下所有项为 ✅：

- [ ] 根目录 README 为项目主要语言版本
- [ ] _config.yml 已创建（如需要 GitHub Pages）
- [ ] 所有 docs/ 文件末尾有导航链接
- [ ] 导航链接的双向性（README → docs 和 docs → README）
- [ ] 所有相对路径引用有效（图片显示正常、PDF 可下载）
- [ ] 无错别字、语句通顺
- [ ] 多语言文档有"主版本已迁移"提示
- [ ] README 中有"深度阅读"章节引用 docs/
- [ ] 提交信息符合约定格式
```

---

## 使用方式

将上方提示词完整复制，发给你的 AI 代理（Claude Code / ChatGPT / 其他支持聊天的 AI），替换 `[仓库名/URL]` 为实际仓库地址即可。

### 示例

> 请对仓库 https://github.com/example/my-project 的文档进行规范化整改，...
