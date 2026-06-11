# analyze-arxiv-paper

A multilingual Codex skill for deep, evidence-grounded analysis of arXiv and AI research papers.

It focuses on methodology, motivation, pipeline details, model modules, equations, experimental evidence, limitations, open-source links, and reproduction guidance. Missing facts are explicitly reported instead of invented.

## Features

- Detailed methodology and pipeline analysis
- LaTeX-preserved equations with symbol explanations
- Evidence-backed experiment and baseline comparisons
- GitHub/project-link detection and reproduction guidance
- Anti-hallucination rules for missing data
- English output by default
- Chinese, Japanese, Korean, German, Italian, French, and other requested languages

## Install

### With Codex Skill Installer

Ask Codex:

```text
Use $skill-installer to install the skill from https://github.com/Luolan-AI/analyze-arxiv-paper
```

### Manual installation

```bash
git clone https://github.com/Luolan-AI/analyze-arxiv-paper.git
mkdir -p ~/.agents/skills
cp -R analyze-arxiv-paper/analyze-arxiv-paper ~/.agents/skills/
```

Restart Codex if the skill does not appear immediately.

## Use

Upload a paper PDF and ask:

```text
Use $analyze-arxiv-paper to analyze this paper.
```

For Chinese output:

```text
使用 $analyze-arxiv-paper，用中文深入分析这篇论文。
```

You can also specify a focus:

```text
Use $analyze-arxiv-paper to explain the methodology, equations, and reproduction steps in German.
```

## Input behavior

- Full PDF or sufficient paper text: performs the complete analysis.
- Abstract plus partial text: analyzes only supported claims.
- Abstract only: translates and provides abstract-level analysis without inventing method or experiment details.
- No paper content: asks the user to upload a PDF or provide text.

## License

MIT License.
# analyze-arxiv-paper
A multilingual Codex skill for deep, evidence-grounded analysis of arXiv and AI research papers.
