---
name: analyze-arxiv-paper
description: "深入阅读和总结用户提供的 arXiv 或其他 AI/机器学习论文 PDF、正文、摘要及补充材料，重点拆解方法动机、设计逻辑、逐步 pipeline、模型模块、数学公式、实验对比、局限性、开源链接和复现建议。用于论文精读、多语言方法解析、公式讲解、实验梳理、代码复现或迁移分析；默认英文，可按用户选择输出其他语言；仅依据用户提供的论文内容作答。 Deeply analyze user-provided arXiv and other AI/ML paper PDFs, text, abstracts, and supplementary materials, focusing on motivation, design logic, step-by-step pipelines, model modules, equations, experiments, limitations, code links, and reproduction guidance. Use for paper reading, multilingual methodology analysis, equation explanation, experiment review, reproduction, or transfer analysis; default to English, support user-selected languages, and rely only on supplied paper content."
---

# 深度分析 AI 论文 / Deep AI Paper Analysis

以 AI 领域博士研究者的标准分析论文，优先帮助用户理解和复现方法部分。保持专业、严谨、可追溯，不把常识、外部资料或猜测伪装成论文结论。

Analyze papers to a doctoral research standard, prioritizing understanding and reproduction of the methodology. Remain professional, rigorous, and traceable. Never present general knowledge, external information, or speculation as a paper conclusion.

## 1. 确认输入与语言 / Confirm Input and Language

1. 接受用户提供的完整 PDF、正文、摘要、附录或补充材料。
   Accept a complete PDF, paper text, abstract, appendix, or supplementary material supplied by the user.
2. 若用户没有提供论文内容，要求其上传 PDF 或粘贴论文文本/摘要，然后停止分析。仅有标题、arXiv ID 或 URL 不等于已提供论文内容；除非用户明确要求并授权检索，否则不要自行联网补充。
   If no paper content is supplied, ask the user to upload a PDF or paste paper text/an abstract, then stop. A title, arXiv ID, or URL alone does not count as supplied content. Do not retrieve external material unless the user explicitly requests and authorizes it.
3. 默认使用英文输出。支持中文、日语、韩语、德语、意大利语、法语或其他明确指定的语言。标题、表格、正文和提示语使用同一种目标语言；保留公式、变量名、模型名、数据集名和指标名。
   Default to English. Support Chinese, Japanese, Korean, German, Italian, French, or another explicitly requested language. Use one target language for headings, tables, prose, and notices while preserving equations, variable names, model names, dataset names, and metric names.
4. 用户未选择语言时直接使用英文，不额外追问；用户明确指定语言时，以其选择为准。
   When no language is selected, use English without asking. When the user specifies a language, follow that choice.
5. 判断证据完整度 / Determine evidence completeness:
   - **完整论文或足够的方法与实验正文 / Full paper or sufficient methodology and experiment text**：执行全部流程。 / Run the complete workflow.
   - **摘要加局部正文 / Abstract plus partial text**：只分析现有内容支持的项目，缺失处写目标语言版本的“论文提供的内容未明确说明”。 / Analyze only supported items and state, in the target language, that the supplied paper content does not explicitly explain missing items.
   - **仅摘要 / Abstract only**：只翻译摘要并进行摘要层面的有限分析；不得扩写方法步骤、公式、实验设置、数值或复现细节。提示用户上传完整 PDF 才能完成深度精读。 / Translate the abstract and provide only abstract-level analysis. Do not invent method steps, equations, experimental settings, numbers, or reproduction details. Ask for the full PDF to complete a deep analysis.

## 2. 建立证据索引 / Build an Evidence Index

通读输入后，在内部定位以下证据，不必展示索引过程：

After reading the supplied content, internally locate the following evidence without showing the indexing process:

- 摘要、问题定义、作者明确提出的动机与贡献。 / Abstract, problem definition, explicitly stated motivation, and contributions.
- Method、Approach、Model、Algorithm、Training、Inference 等章节。 / Method, Approach, Model, Algorithm, Training, and Inference sections.
- 关键公式、算法框、模型图、流程图及符号定义。 / Key equations, algorithm blocks, architecture diagrams, flowcharts, and symbol definitions.
- Experiments、Implementation Details、Ablation、Limitations、Appendix。 / Experiments, Implementation Details, Ablation, Limitations, and Appendix sections.
- 数据集、指标、基线、关键数值和计算成本。 / Datasets, metrics, baselines, key values, and computational costs.
- `github.com`、`GitHub`、`code`、`implementation`、`project page`、`supplementary` 等代码或项目链接线索。 / Code and project-link clues such as `github.com`, `GitHub`, `code`, `implementation`, `project page`, and `supplementary`.

重要事实尽量附简短位置标记，例如 `[来源：§3.2, Eq. (4)]`、`[Source: Table 2]` 或 `[来源：用户提供的摘要 / Source: supplied abstract]`。输入没有页码或章节信息时，不虚构位置。

Attach short location markers to important facts when possible, such as `[Source: §3.2, Eq. (4)]`, `[Source: Table 2]`, or `[Source: supplied abstract]`. Never invent page or section locations.

## 3. 执行分析 / Perform the Analysis

### 摘要翻译 / Abstract Translation

- 忠实翻译完整摘要，不添加摘要外的信息。 / Faithfully translate the complete abstract without adding information.
- 保留技术名词、缩写、数学符号和数值；必要时首次出现时补充原文术语。 / Preserve technical terms, abbreviations, mathematical symbols, and numbers; include the original term at first mention when useful.
- 若摘要已使用目标语言，提供忠实、通顺的整理版，并说明无需跨语言翻译。 / If the abstract is already in the target language, provide a faithful polished version and state that cross-language translation is unnecessary.

### 方法动机 / Method Motivation

- 说明作者为什么提出该方法及其驱动力。 / Explain why the authors proposed the method and what motivated it.
- 具体列出现有方法的痛点、假设限制或失败场景。 / Identify concrete weaknesses, assumption limits, or failure cases of existing methods.
- 简洁概括研究假设或核心直觉。 / Concisely summarize the research hypothesis or core intuition.
- 区分作者明确陈述与分析性推断。推断必须标记为目标语言版本的“基于论文内容的推断”，且不得引入外部事实。 / Distinguish explicit author statements from analytical inference. Label inference as based on the supplied paper and do not introduce external facts.

### 方法设计 / Method Design

这是全文重点，应投入最多篇幅。按照输入到输出的真实依赖关系逐步解释，而不是只罗列模块名称。

This is the primary focus and should receive the most detail. Explain the true input-to-output dependencies step by step instead of merely listing module names.

1. 定义任务、输入、输出、训练目标和推理目标。 / Define the task, inputs, outputs, training objective, and inference objective.
2. 给出完整 pipeline，每一步说明 / Provide the complete pipeline and explain for every step:
   - 接收什么数据或中间表示。 / What data or intermediate representation it receives.
   - 执行什么具体操作，包括采样、编码、变换、融合、匹配、优化或解码。 / What exact operation it performs, including sampling, encoding, transformation, fusion, matching, optimization, or decoding.
   - 产生什么输出，以及输出的形状、语义或后续用途；论文未给形状时不要猜测。 / What it outputs and the output's shape, meaning, or later use; do not guess shapes absent from the paper.
   - 该步骤为什么存在，以及如何解决前述痛点。 / Why the step exists and how it addresses the stated problem.
3. 描述每个模型模块的职责、信息流、参数共享关系和模块间协作。 / Describe each module's responsibility, information flow, parameter sharing, and coordination with other modules.
4. 区分训练与推理阶段，指出输入、计算路径和输出差异。 / Separate training from inference and explain differences in inputs, computation paths, and outputs.
5. 对每个核心公式 / For every core equation:
   - 使用 LaTeX 原样保留或忠实重写，例如 `$L = L_{task} + \lambda L_{reg}$`。 / Preserve or faithfully rewrite it in LaTeX, for example `$L = L_{task} + \lambda L_{reg}$`.
   - 定义重要符号、张量或概率项。 / Define important symbols, tensors, and probability terms.
   - 解释公式计算什么、优化什么、影响哪个模块。 / Explain what it computes, what it optimizes, and which module it affects.
   - 说明公式在整体 pipeline 中的位置和设计作用。 / State where it appears in the pipeline and its design role.
   - 不得用纯文字跳过核心数学关系；输入缺失公式时，明确说明论文提供的内容未包含该公式。 / Do not replace core mathematical relationships with vague prose. If the formula is absent, explicitly say the supplied content does not include it.
6. 若有算法框，按真实顺序解释初始化、循环、条件、更新规则和停止条件。 / If an algorithm block is present, explain initialization, loops, conditions, update rules, and stopping criteria in the original order.

### 与其他方法对比 / Comparison with Other Methods

- 只比较论文正文中出现或可由其描述直接支持的方法。 / Compare only methods mentioned in or directly supported by the supplied paper.
- 从建模对象、信息来源、训练目标、推理方式或计算流程说明本质差异。 / Explain fundamental differences in modeling target, information source, training objective, inference method, or computation flow.
- 将创新区分为核心机制、已有组件的新组合、训练/工程改进或应用扩展。不得夸大“首次”或“SOTA”；此类说法必须归因于作者。 / Classify innovation as a core mechanism, a new combination of existing components, a training/engineering improvement, or an application extension. Do not exaggerate “first” or “SOTA” claims; attribute them to the authors.
- 分析适用范围和更合适的场景，并说明证据。 / Analyze scope and suitable scenarios with supporting evidence.
- 使用 Markdown 表格，至少包含：`方法/类别 / Method/Category`、`核心做法 / Core Approach`、`优点 / Advantages`、`缺点 / Disadvantages`、`本文改进 / Improvement`、`证据位置 / Evidence Location`。缺失项填写目标语言版本的“论文未明确说明”。 / Use a Markdown table with at least these fields. Fill unsupported cells with the target-language equivalent of “The paper does not explicitly state this.”

### 实验表现与优势 / Experimental Performance and Advantages

- 说明任务、数据集、数据划分、基线、指标、训练设置、消融实验和效率实验。 / Explain tasks, datasets, splits, baselines, metrics, training settings, ablations, and efficiency experiments.
- 只列出可从表格或正文核对的代表性数值，并写清方法、数据集、指标、方向和对比对象。 / Report only verifiable representative values and include the method, dataset, metric, direction, and comparison target.
- 指出优势最明显的场景及具体证据，不用“显著提升”替代数字。 / Identify scenarios with the strongest advantages and provide concrete evidence instead of replacing numbers with vague claims.
- 分开整理作者承认的局限与由论文证据支持的隐含局限；后者标记为“基于论文内容的推断”。 / Separate author-acknowledged limitations from evidence-supported implicit limitations; label the latter as inference based on the paper.
- 检查泛化能力、计算/显存开销、训练稳定性、数据依赖、标注成本、假设条件和失败案例；无证据时明确说明。 / Check generalization, compute/memory cost, training stability, data dependence, annotation cost, assumptions, and failure cases; explicitly state when evidence is absent.
- 不自行计算统计显著性，不混淆绝对提升、相对提升和百分比。 / Do not calculate statistical significance independently or confuse absolute, relative, and percentage improvements.

### 学习与应用 / Learning and Application

- 主动检索论文内容中的 GitHub、代码仓库和项目主页链接。找到时原样提供并注明位置；未找到时写目标语言版本的“论文文本中未发现 GitHub 链接”。 / Search the supplied content for GitHub, repository, and project-page links. Provide exact links and locations when found; otherwise state that no GitHub link was found in the supplied paper text.
- 总结复现步骤：数据准备、预处理、模型初始化、损失函数、训练策略、推理流程和评估协议。 / Summarize reproduction steps: data preparation, preprocessing, initialization, losses, training strategy, inference, and evaluation protocol.
- 提取论文明确给出的超参数、优化器、学习率、批量大小、训练轮数、数据增强、硬件和随机种子。缺失项明确说明。 / Extract explicitly stated hyperparameters, optimizer, learning rate, batch size, epochs, augmentation, hardware, and random seeds. Mark missing items clearly.
- 未发现代码链接但方法足够完整时，提供基于 PyTorch 的高层级伪代码。只表达论文支持的模块和数据流，并注释未说明的细节；不要伪造可直接运行的完整实现。 / When no code link is found but the method is sufficiently specified, provide high-level PyTorch pseudocode containing only supported modules and data flow. Comment on unspecified details and do not fabricate a runnable implementation.
- 只有摘要或方法信息不足时，不生成猜测性伪代码，改为列出复现前仍需获取的信息。 / With only an abstract or insufficient method details, do not generate speculative pseudocode; list the information still required for reproduction.
- 分析跨任务迁移。论文验证过的写为事实；其他情况标记为“迁移设想”，并说明需替换的数据接口、输出头、损失或训练协议。 / Analyze transfer to other tasks. Treat paper-validated transfer as fact; label other cases as transfer proposals and explain required changes to data interfaces, output heads, losses, or training protocols.

### 总结 / Summary

- 用一句短句概括核心思想。中文、日语和韩语不超过 20 个字符；英文、德语、意大利语、法语等以空格分词的语言不超过 20 个词。优先保证准确。 / Summarize the core idea in one short sentence: at most 20 characters for Chinese, Japanese, or Korean, and at most 20 words for space-delimited languages. Prioritize accuracy.
- 给出 3 至 5 步“速记版 pipeline”。不用论文自造术语或比喻，使用自明、直接的动作描述。 / Provide a 3-5 step memorization pipeline using direct, self-explanatory actions without paper-specific coined terms or metaphors.

## 4. 固定输出结构 / Fixed Output Structure

严格保持以下编号和层级。将标题翻译成目标语言，不要同时输出中英文标题，除非用户明确要求双语分析。

Keep the following numbering and hierarchy. Translate headings into the target language; do not output bilingual headings unless the user explicitly requests bilingual analysis.

```markdown
## 0. 摘要翻译 / Abstract Translation

## 1. 方法动机 / Method Motivation
### 1.1 提出原因 / Why the Method Was Proposed
### 1.2 现有方法痛点 / Limitations of Existing Methods
### 1.3 研究假设或直觉 / Research Hypothesis or Intuition

## 2. 方法设计 / Method Design
### 2.1 任务定义与输入输出 / Task Definition, Input, and Output
### 2.2 详细 Pipeline / Detailed Pipeline
### 2.3 模块结构与协作 / Modules and Coordination
### 2.4 公式与算法解释 / Equations and Algorithms
### 2.5 训练与推理差异 / Training vs. Inference

## 3. 与其他方法对比 / Comparison with Other Methods
### 3.1 本质差异与创新点 / Fundamental Differences and Innovations
### 3.2 适用场景 / Applicable Scenarios
### 3.3 方法对比表 / Comparison Table

## 4. 实验表现与优势 / Experimental Performance and Advantages
### 4.1 实验设计 / Experimental Design
### 4.2 关键结果 / Key Results
### 4.3 优势最明显的场景 / Scenarios with the Strongest Advantages
### 4.4 局限性 / Limitations

## 5. 学习与应用 / Learning and Application
### 5.1 开源情况 / Open-Source Status
### 5.2 复现步骤 / Reproduction Steps
### 5.3 超参数与实现注意事项 / Hyperparameters and Implementation Notes
### 5.4 PyTorch 高层级伪代码（需要时）/ High-Level PyTorch Pseudocode (When Applicable)
### 5.5 迁移到其他任务 / Transfer to Other Tasks

## 6. 总结 / Summary
### 6.1 一句话核心思想 / One-Sentence Core Idea
### 6.2 速记版 Pipeline / Memorization Pipeline
```

某节证据不足时，保留标题并直接说明信息缺失，不要删除该节或用常识填充。

When evidence is insufficient, retain the heading and explicitly state that information is missing. Do not delete the section or fill it with general knowledge.

## 5. 最终质量检查 / Final Quality Check

输出前逐项确认 / Confirm before responding:

- 所有实验数字均可在用户提供的内容中定位。 / Every experimental number is traceable to supplied content.
- 所有核心公式均保留数学符号并使用 LaTeX。 / Every core equation preserves mathematical symbols and uses LaTeX.
- 每个模块都解释了输入、操作、输出、作用和协作关系。 / Every module includes its input, operation, output, purpose, and coordination.
- 已区分论文事实、作者主张和基于论文内容的推断。 / Paper facts, author claims, and evidence-based inference are distinguished.
- 没有把摘要层面的描述扩写成不存在的方法细节。 / Abstract-level statements are not expanded into nonexistent method details.
- 没有找到的信息明确标记为论文未说明。 / Missing information is explicitly marked as not stated by the paper.
- 标题、表格和正文符合用户选择；未指定语言时使用英文。 / Headings, tables, and prose follow the user's language choice; English is used by default.
