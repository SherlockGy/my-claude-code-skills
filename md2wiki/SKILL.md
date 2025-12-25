---
name: md2wiki
description: |
  使用 pandoc 将 Markdown 文件转换为 Jira/Confluence wiki 格式。
  适用场景：(1) 将 .md 文件转换为 wiki 格式 (2) markdown 转 jira 格式 (3) 生成 confluence 兼容的 wiki 文件。
  用户需在提示词中指定要转换的 markdown 文件路径。
---

# Markdown 转 Jira/Confluence Wiki 转换器

使用内置的 pandoc 将 markdown 文件转换为 Jira/Confluence wiki 格式。

## 工作流程

1. 从用户提示词中获取 markdown 文件路径
2. 验证文件是否存在
3. 使用 skill 内置的 pandoc 执行转换：
   ```bash
   "<skill_dir>/scripts/pandoc.exe" "<输入文件.md>" -t jira -o "<输出文件.wiki.txt>"
   ```
   其中 `<skill_dir>` 是此 skill 所在目录的绝对路径。
4. 输出文件命名规则：将 `.md` 扩展名替换为 `.wiki.txt`，保存在同一目录
   - 示例：`readme.md` -> `readme.wiki.txt`

## 内置工具

- `scripts/pandoc.exe` - pandoc 可执行文件，无需系统安装

## 错误处理

- 文件不存在：告知用户指定的文件不存在
- 转换失败：显示 pandoc 的错误信息
