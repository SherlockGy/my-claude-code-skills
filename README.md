# Claude Code Skills 合集

这是我的个人 Claude Code Skills 集合，包含一些实用的文档处理工具。

## Skills 列表

### 1. ascii-to-image

将 Markdown 文件中的 ASCII 字符画转换为精美的 PNG 图片。

**功能特性：**
- 识别 Markdown 中的 ASCII 图（流程图、架构图、状态机等）
- 语义理解后生成专业 SVG（支持渐变、阴影、圆角）
- 使用 resvg 转换为高清 PNG（200 DPI）
- 自动替换原 ASCII 块为图片引用

**使用方式：**
- 对 Claude 说："把 xxx.md 的字符画变成图片"

---

### 2. md2wiki

将 Markdown 文件转换为 Jira/Confluence Wiki 格式。

**功能特性：**
- 使用内置 pandoc 进行格式转换
- 支持转换为 Jira/Confluence 兼容的 wiki 格式
- 自动生成 `.wiki.txt` 输出文件
- 无需系统安装 pandoc，开箱即用

**使用方式：**
- 将某个 .md 文件转换为 wiki 格式
- 把全部 markdown 转 jira 格式
- 为某个 md 文件生成 confluence 兼容的 wiki 文件

---

## 安装方法

将需要的 skill 文件夹复制到你的项目的 `.claude/skills/` 目录下：

```
your-project/
└── .claude/
    └── skills/
        ├── ascii-to-image/
        └── md2wiki/
```
