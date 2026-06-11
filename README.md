# analyze-arxiv-paper

[中文](#中文) | [English](#english)

## 中文

一个用于深度、基于证据分析 arXiv 与 AI 研究论文的多语言 Codex Skill。

它重点解析方法动机、详细流程、模型模块、数学公式、实验依据、局限性、开源链接和复现建议。对于论文未提供的信息，会明确说明缺失，而不会自行编造。

### 功能特点

- 深入解析方法设计与完整 Pipeline
- 使用 LaTeX 保留关键公式，并逐一解释符号
- 基于论文证据比较实验结果与基线方法
- 检索 GitHub、代码仓库和项目主页链接
- 缺失数据与信息的防幻觉规则
- 默认使用英文输出
- 支持中文、日语、韩语、德语、意大利语、法语及其他指定语言

### 安装

#### 使用 Codex Skill Installer

在 Codex 中输入：

```text
使用 $skill-installer 从 https://github.com/Luolan-AI/analyze-arxiv-paper 安装 Skill
```

#### 手动安装

```bash
git clone https://github.com/Luolan-AI/analyze-arxiv-paper.git
mkdir -p ~/.agents/skills
cp -R analyze-arxiv-paper/analyze-arxiv-paper ~/.agents/skills/
```

如果 Skill 没有立即出现，请重启 Codex。

### 使用

通常不需要每次完整输入 Skill 名称。上传论文 PDF 后，直接输入：

```text
用中文分析这篇论文
```

也可以更简短：

```text
分析这篇论文
```

Codex 会根据论文分析请求自动匹配此 Skill。未指定语言时默认使用英文。

只有自动匹配失败时，才需要显式调用：

```text
使用 $analyze-arxiv-paper，用中文深入分析这篇论文。
```

也可以指定重点：

```text
使用 $analyze-arxiv-paper，重点解释论文的方法、公式和复现步骤。
```

### 输入处理规则

- 完整 PDF 或足够的论文正文：执行完整分析。
- 摘要加部分正文：只分析现有内容能够支持的结论。
- 仅有摘要：翻译摘要并提供摘要层面的分析，不虚构方法或实验细节。
- 未提供论文内容：要求用户上传 PDF 或提供论文文本。

### 许可证

MIT License。

---

## English

A multilingual Codex skill for deep, evidence-grounded analysis of arXiv and AI research papers.

It focuses on methodology, motivation, pipeline details, model modules, equations, experimental evidence, limitations, open-source links, and reproduction guidance. Missing facts are explicitly reported instead of invented.

### Features

- Detailed methodology and pipeline analysis
- LaTeX-preserved equations with symbol explanations
- Evidence-backed experiment and baseline comparisons
- GitHub, code repository, and project-page detection
- Anti-hallucination rules for missing information
- English output by default
- Chinese, Japanese, Korean, German, Italian, French, and other requested languages

### Install

#### With Codex Skill Installer

Ask Codex:

```text
Use $skill-installer to install the skill from https://github.com/Luolan-AI/analyze-arxiv-paper
```

#### Manual installation

```bash
git clone https://github.com/Luolan-AI/analyze-arxiv-paper.git
mkdir -p ~/.agents/skills
cp -R analyze-arxiv-paper/analyze-arxiv-paper ~/.agents/skills/
```

Restart Codex if the skill does not appear immediately.

### Use

You normally do not need to type the full skill name every time. After uploading a paper PDF, simply ask:

```text
Analyze this paper in Chinese.
```

Or even:

```text
Analyze this paper.
```

Codex can automatically match paper-analysis requests to this skill. English is used by default when no language is specified.

Use the explicit invocation only if automatic matching fails:

```text
Use $analyze-arxiv-paper to analyze this paper.
```

You can also specify a focus or output language:

```text
Use $analyze-arxiv-paper to explain the methodology, equations, and reproduction steps in German.
```

### Input behavior

- Full PDF or sufficient paper text: performs the complete analysis.
- Abstract plus partial text: analyzes only supported claims.
- Abstract only: translates and provides abstract-level analysis without inventing method or experiment details.
- No paper content: asks the user to upload a PDF or provide text.

### License

MIT License.
