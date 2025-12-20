# ASCII to Image Converter

将 Markdown 文件中的 ASCII 字符画转换为精美的 PNG 图片。

## 功能

- 识别 Markdown 中的 ASCII 图（流程图、架构图、状态机等）
- 语义理解后生成专业 SVG（渐变、阴影、圆角）
- 使用 resvg 转换为高清 PNG（200 DPI）
- 自动替换原 ASCII 块为图片引用

## 使用方式

对 Claude 说：
- "把 xxx.md 的字符画变成图片"
- "Convert ASCII diagrams to images"

## ASCII 块标记

```markdown
<!-- CONVERT_TO_IMAGE: diagram-name -->
+-------+     +-------+
| Start | --> |  End  |
+-------+     +-------+
<!-- END_CONVERT_TO_IMAGE -->
```

## 安装

将整个 `ascii-to-image` 文件夹复制到项目的 `.claude/skills/` 目录下：

```
your-project/
└── .claude/
    └── skills/
        └── ascii-to-image/    ← 放这里
            ├── README.md
            ├── SKILL.md
            └── scripts/
                └── resvg.exe
```

## 依赖

- `scripts/resvg.exe` - SVG 转 PNG 工具（已内置，无需额外安装）
