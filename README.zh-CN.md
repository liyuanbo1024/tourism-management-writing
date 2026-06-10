# 旅游与酒店管理学术写作技能

[English](README.md) | [简体中文](README.zh-CN.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

面向 OpenCode / Claude Code / Codex 等AI编程智能体的旅游与酒店管理学术写作技能——覆盖从选题定位、理论框架、研究设计、数据分析到完整初稿的全流程。

覆盖6本旅游酒店领域旗舰期刊：**Tourism Management, Annals of Tourism Research, JTR, IJHM, IJCHM, JST**。

## 技能功能

引导AI智能体完成旅游与酒店管理论文的**0到初稿五阶段流程**：

| 阶段 | 产出 | 关键交付物 |
|------|------|-----------|
| **阶段1**：选题定位 | Gap table、期刊推荐、贡献陈述 | 投哪本期刊 + 创新点是什么 |
| **阶段2**：理论框架 | 概念模型、假设推导、文献综合 | §2 文献与框架初稿 |
| **阶段3**：研究设计 | 方法论蓝图（定量/定性/混合）、测量量表、抽样方案 | §3 方法论章节初稿 |
| **阶段4**：数据分析 | 定量（SEM、回归、旅游需求）或定性（扎根理论、民族志、主题分析）结果 | §4-5 分析结果初稿 |
| **阶段5**：写作组装 | 引言、讨论、理论与实践启示、摘要 | 完整初稿 |

该技能是**领域特化**的：内置了旅游与酒店期刊特有的规范——如概念模型呈现结构、量表开发标准、定性研究可信度准则、混合方法整合框架、各刊审稿人期望等，这些是通用写作技能不覆盖的。

---

## 安装

### 1. 克隆仓库

```bash
git clone https://github.com/liyuanbo1024/tourism-management-writing.git
```

### 2. 安装到AI智能体

| 智能体 | 安装命令 |
|--------|---------|
| **OpenCode** | `cp -r tourism-management-writing ~/.config/opencode/skills/` |
| **Claude Code** | `cp -r tourism-management-writing ~/.claude/skills/` |
| **Codex** | `cp -r tourism-management-writing ~/.agents/skills/` |
| **Cursor** | `cp -r tourism-management-writing ~/.cursor/skills/` |
| **Windsurf** | `cp -r tourism-management-writing ~/.windsurf/skills/` |

Windows PowerShell 用户将 `cp -r` 替换为 `Copy-Item -Recurse`，将 `~/` 替换为 `$env:USERPROFILE\`。

安装后通过自然语言触发，例如：
- "我要写一篇社交媒体影响游客行为的论文，帮我定位选题"
- "概念模型和假设已经搭好，帮我设计测量量表和调查问卷"
- "带我走一遍完整的旅游管理论文写作流程"

---

## 使用方式

### 管道模式

```
"带我走一遍完整的旅游管理写作流程。我的选题是……"
```

智能体会加载技能，评估当前阶段，从阶段1推进到阶段5，每个阶段完成后请求确认。

### 阶段跳转

| 触发语 | 跳转阶段 |
|--------|---------|
| "我有一个研究想法……" | 阶段1：选题定位 |
| "帮我构建理论框架" | 阶段2：理论框架 |
| "帮我设计研究方法" | 阶段3：研究设计 |
| "帮我分析调查/访谈数据" | 阶段4：数据分析 |
| "帮我写完整论文" | 阶段5：写作组装 |

### 参考模式

```
"Tourism Management 对定性研究严谨度的要求是什么？"
"JTR 的假设推导应该怎么组织？"
```

---

## 文件结构

```
tourism-management-writing/
├── SKILL.md                              主技能文件
├── references/
│   ├── journal-characteristics.md        6本期刊详细特征
│   ├── theoretical-framework.md          概念模型·假设写作
│   ├── quantitative-methods.md           SEM·CFA·回归·旅游需求建模
│   ├── qualitative-methods.md            扎根理论·民族志·主题分析
│   ├── measurement-scales.md             量表开发·验证·跨文化调适
│   ├── mixed-methods.md                  混合方法整合设计
│   ├── reviewer-expectations.md          审稿心理·Rebuttal策略
│   └── writing-patterns.md               可复用写作模式
├── assets/
│   └── conceptual-model-examples.md      概念模型示例
├── examples/
│   ├── manuscript_template.tex           LaTeX模板
│   ├── sem_analysis.R                    SEM分析模板（lavaan）
│   └── qualitative_coding.py             主题分析Python模板
├── README.md                             英文说明
├── README.zh-CN.md                       中文说明（本文件）
├── README.ja.md                          日文说明
├── README.ko.md                          韩文说明
└── LICENSE                               MIT许可证
```

---

## 覆盖期刊

| 期刊 | 缩写 | 核心定位 |
|------|------|---------|
| Tourism Management | TM | 广泛旅游研究、高严谨度、政策与实践影响 |
| Annals of Tourism Research | ATR | 理论深度、社会学/人类学视角 |
| Journal of Travel Research | JTR | 定量聚焦、消费者行为、目的地营销 |
| Int. J. Hospitality Management | IJHM | 酒店运营、人力资源管理、服务管理 |
| Int. J. Contemporary Hospitality Mgmt | IJCHM | 当代前沿、创新、战略酒店管理 |
| Journal of Sustainable Tourism | JST | 可持续性、伦理、社区影响、环境 |

### 各期刊方法论偏好

| 方法 | TM | ATR | JTR | IJHM | IJCHM | JST |
|------|-----|------|------|------|-------|-----|
| 定量（SEM、回归） | ✓✓✓ | ✓ | ✓✓✓ | ✓✓✓ | ✓✓✓ | ✓✓ |
| 定性（扎根理论、民族志） | ✓✓ | ✓✓✓ | ✓ | ✓✓ | ✓✓ | ✓✓✓ |
| 混合方法 | ✓✓ | ✓✓ | ✓✓ | ✓✓ | ✓✓✓ | ✓✓✓ |
| 量表开发 | ✓✓✓ | ✓ | ✓✓✓ | ✓✓✓ | ✓✓✓ | ✓✓ |
| 旅游需求建模 | ✓✓✓ | ✓ | ✓✓✓ | ✓ | — | — |
| 系统综述/元分析 | ✓✓ | ✓✓✓ | ✓✓ | ✓✓ | ✓✓✓ | ✓✓ |

---

## 示例

`examples/` 目录包含参考文件：

1. **`manuscript_template.tex`**：LaTeX模板，含旅游论文的标准章节占位（引言→文献与框架→方法→结果→讨论与启示）。

2. **`sem_analysis.R`**：可运行的R语言SEM分析模板（lavaan），含测量模型CFA、结构模型、拟合指数和中介分析。

3. **`qualitative_coding.py`**：Python主题分析工作流模板——编码、主题提炼与可信度文档。

---

## 定制化

### 添加新期刊

编辑 `references/journal-characteristics.md`，按模板格式新增期刊条目。

### 调整SEM模型

修改 `examples/sem_analysis.R` 中的 lavaan 模型语法。

---

## 参与贡献

欢迎贡献。亟需帮助的方向：
- 更多旅游期刊的详细特征和审稿期望
- 从已发表论文中提炼的额外写作模式
- SmartPLS / Mplus / NVivo 的分析模板
- 旅游/酒店构念的验证量表目录

---

## 许可证

MIT License — 详见 [LICENSE](LICENSE)。

---

## 致谢

基于 [agentskills.io](https://agentskills.io) 规范和 [OpenCode](https://github.com/anomalyco/opencode) 的技能创作方法论构建。旅游与酒店领域知识来源于 Elsevier 期刊（Tourism Management、ATR、IJHM、IJCHM）、Sage（JTR）和 Taylor & Francis（JST）的编辑声明。
