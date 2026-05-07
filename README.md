# jiang-ai-skill

`jiang-ai-skill` 是一个面向中文论文和学术文本的 Codex skill，目标是降低模板化、机械化的 AI 表达痕迹，让文本更接近真实作者反复推敲后的写作状态，同时尽量保留专业术语、事实、数据、引文和原有文档结构。

这个项目包含两部分：

- `降ai/`：skill 本体，定义任务边界、改写原则、红黄绿分级和 DOCX 工作流。
- `scripts/docx_io.py`：配套的轻量 DOCX 辅助脚本，用于读取段落、替换段落、分析格式和输出基础格式化文档。

这个仓库用于公开展示我在中文学术写作辅助方向上的实践，也可以作为后续申请项目计划时的开源项目材料。

## 适用场景

- 课程论文、毕业论文、研究报告的学术表达自然化
- 对中文文本做“降 AI 味”处理
- 保留原始排版结构的 Word 文档改写工作流
- 先检查高风险段落，再进行重点改写

## 项目结构

```text
jiang-ai-skill/
├─ README.md
├─ LICENSE
├─ requirements.txt
├─ scripts/
│  └─ docx_io.py
└─ 降ai/
   ├─ SKILL.md
   └─ agents/
      └─ openai.yaml
```

## 已知能力

### 1. Skill 侧

- 对整篇论文做红黄绿分级，而不是只做逐句替换
- 优先处理摘要、引言、研究意义、文献综述、结论等高风险章节
- 保留专业术语、作者名、年份、数据、图表编号和参考文献编号
- 更关注重组表达和论证顺序，而不是简单换同义词

### 2. 脚本侧

`scripts/docx_io.py` 当前提供这些命令：

- `read`：读取 `.docx` 非空段落并编号输出
- `replace`：替换指定段落，默认输出为新文件，不覆盖原文
- `write`：把纯文本写入新的 `.docx`
- `analyze`：分析模板的页面和字体格式信息
- `formatted_write`：把基础 Markdown 文本输出为 `.docx`，可选复用模板格式

## 当前状态与已知限制

这个仓库中的脚本是为个人工作流整理出来的轻量辅助工具，公开版本以“基础可用”为目标，不是完整的论文改写平台。

已知限制如下：

- 依赖 `python-docx`，需要先安装依赖后再运行
- 更适合基础的 DOCX 读取、段落替换、格式分析和轻量格式化输出
- 对非常复杂的论文模板、特殊域对象、脚注、批注、修订痕迹等场景，兼容性有限
- 不承诺任何 AIGC 检测平台结果
- 不保证适配所有学校模板或所有第三方查重/检测流程

## 安装

### Python 依赖

```bash
pip install -r requirements.txt
```

### 作为 Codex skill 使用

把 `降ai/` 目录放到本地 Codex skills 目录后，即可按 skill 方式调用。

如果你的环境支持按名称引用 skill，可以直接使用：

```text
使用 $jiang-ai 检查并改写这篇 Word 论文，按红黄绿分级处理高风险段落，并保留原有排版。
```

## 脚本用法

### 1. 读取段落

```bash
python scripts/docx_io.py read input.docx
```

### 2. 替换指定段落并输出为新文件

```bash
echo 这是新的段落内容 | python scripts/docx_io.py replace input.docx 12 --output output.docx
```

### 3. 写入纯文本到新文档

```bash
type content.txt | python scripts/docx_io.py write output.docx
```

### 4. 分析模板格式

```bash
python scripts/docx_io.py analyze template.docx
```

### 5. 生成基础格式化文档

```bash
type content.md | python scripts/docx_io.py formatted_write output.docx --template template.docx
```

## 开源说明

这个项目的目标是帮助中文论文和学术文本做表达自然化与结构整理，不提供“绕过检测”的承诺，也不建议将其理解为任何检测平台的对抗工具。

如果你要基于这个项目继续开发，建议把它视为：

- 一个可直接复用的 Codex skill 样例
- 一个面向 DOCX 工作流的轻量脚本起点
- 一个适合继续工程化的个人开源项目雏形

## 许可证

本项目采用 [MIT License](./LICENSE)。
