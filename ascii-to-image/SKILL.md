---
name: ascii-to-image
description: Convert ASCII art diagrams in markdown files to beautiful SVG graphics and PNG images. Claude interprets the ASCII diagram semantically and generates professional SVG code. Use when user asks to convert text diagrams, ASCII art, or character drawings to images.
allowed-tools: Read, Write, Edit, Glob, Bash
---

# ASCII to Image Converter

## 触发条件

当用户说以下类似的话时使用此 Skill：
- "把这个 md 文件里的字符画变成图片"
- "把 xxx.md 的 ASCII 图转成图片"
- "Convert ASCII diagrams to images"

## 工作流程

### Step 1: 读取 Markdown 文件
使用 Read 工具读取用户指定的 markdown 文件。

### Step 2: 识别 ASCII 块
查找被以下标记包裹的 ASCII 内容：
```
<!-- CONVERT_TO_IMAGE: <name> -->
...ASCII 字符画...
<!-- END_CONVERT_TO_IMAGE -->
```
如果没有标记，询问用户要转换哪个部分。

### Step 3: 分析图形类型
判断 ASCII 块类型：流程图、架构图、表格、状态机、树形图等。

### Step 4: 生成美化 SVG
根据语义理解生成专业的 SVG 代码，保存到 `images/<name>.svg`。

### Step 5: 转换为 PNG
调用 resvg 工具（使用 --dpi 200 提高清晰度）：
```bash
.claude/skills/ascii-to-image/scripts/resvg.exe --dpi 200 images/<name>.svg images/<name>.png
```
批量转换时，对每个 SVG 文件分别调用上述命令。

### Step 6: 更新 Markdown
用 Edit 工具将 ASCII 块替换为：`![name](images/name.png)`

## SVG 设计原则

### 图形样式
1. **圆角矩形**: `rx="8"` 或 `rx="12"`
2. **渐变填充**: 使用 `<linearGradient>`
3. **阴影效果**: 使用 `<feDropShadow>`
4. **箭头标记**: 使用 `<marker>` 元素
5. **背景**: `#FAFAFA` 或 `white`

### 文字清晰度（重要）
1. **字体粗细**: `font-weight="bold"` 或 `font-weight="700"`，必须加粗
2. **字号**: 最小 14px，标题 16-20px
3. **字体**: `font-family="Arial, Microsoft YaHei, sans-serif"`
4. **居中**: `text-anchor="middle"`
5. **颜色**: 统一使用 `white`，保持视觉一致性

## 配色参考

| 背景色 | 用途 |
|--------|------|
| #3B82F6 (蓝) | 处理/信息 |
| #10B981 (绿) | 开始/成功 |
| #6366F1 (紫) | 层级/组件 |
| #EF4444 (红) | 结束/错误 |
| #F59E0B (黄/橙) | 数据/存储 |
| #FBBF24 (浅黄) | 警告/注意 |

所有文字统一使用白色 (`fill="white"`)。

## 注意事项

1. SVG 的 width/height 根据内容调整
2. 如果 resvg 转换失败，提示用户在浏览器中打开 SVG 另存为 PNG
3. 中文文字可正常显示
4. **禁止添加装饰性图标**（如用户头像、图标符号等），只绘制 ASCII 图中明确存在的元素
