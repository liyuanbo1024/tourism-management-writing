# Tourism & Hospitality Management Academic Writing Skill

[English](README.md) | [简体中文](README.zh-CN.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

A comprehensive OpenCode/Claude Code/Codex skill for writing tourism and hospitality management papers — from topic selection through theoretical framing, research design, data analysis, to a complete first draft.

Covers 6 flagship tourism & hospitality journals: **Tourism Management, Annals of Tourism Research, JTR, IJHM, IJCHM, JST**.

## What This Skill Does

This skill guides AI coding agents through the full **0-to-Draft Pipeline** for tourism & hospitality papers:

| Stage | What It Produces | Key Output |
|-------|-----------------|------------|
| **Stage 1**: Topic Positioning | Gap table, journal recommendation, contribution statement | Which journal + what's new |
| **Stage 2**: Theoretical Framework | Conceptual model, hypothesis development, literature synthesis | §2 Literature & framework draft |
| **Stage 3**: Research Design | Methodology blueprint (quant/qual/mixed), measurement scales, sampling plan | §3 Methodology section draft |
| **Stage 4**: Data Analysis | Quantitative (SEM, regression, tourism demand) or Qualitative (grounded theory, ethnography, thematic analysis) results | §4-5 Results draft |
| **Stage 5**: Writing & Assembly | Introduction, Discussion, Implications, Abstract, formatting | Complete first draft |

The skill is **domain-specific**: it encodes the conventions, expectations, and stylistic norms of tourism & hospitality journals — such as conceptual model presentation, measurement scale development standards, qualitative trustworthiness criteria, mixed-methods integration frameworks, and journal-specific reviewer expectations — that generic writing skills do not cover.

---

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/liyuanbo1024/tourism-management-writing.git
```

### 2. Install for Your AI Agent

Choose your platform below.

#### OpenCode

Copy the skill directory to your OpenCode skills folder:

```bash
# Linux/macOS
cp -r tourism-management-writing ~/.config/opencode/skills/

# Windows (PowerShell)
Copy-Item -Recurse tourism-management-writing "$env:USERPROFILE\.config\opencode\skills\"
```

Or register a custom skills path in `~/.config/opencode/opencode.json`:

```json
{
  "skills": {
    "paths": [
      "~/.config/opencode/skills",
      "/path/to/your/cloned/tourism-management-writing"
    ]
  }
}
```

Then trigger with: `/tourism-management-writing` or just describe your task naturally ("I need to write a Tourism Management paper on...").

#### Claude Code (Anthropic)

```bash
# Linux/macOS
cp -r tourism-management-writing ~/.claude/skills/

# Windows (PowerShell)
Copy-Item -Recurse tourism-management-writing "$env:USERPROFILE\.claude\skills\"
```

Claude Code auto-discovers skills in `~/.claude/skills/`. The skill activates when you mention:
- Writing for Tourism Management, Annals of Tourism Research, JTR, IJHM, IJCHM, JST
- Tourism/hospitality research design, SEM, grounded theory, ethnography
- Any phrase matching the skill description triggers

#### Codex (OpenAI)

```bash
# Linux/macOS
cp -r tourism-management-writing ~/.agents/skills/

# Windows (PowerShell)
Copy-Item -Recurse tourism-management-writing "$env:USERPROFILE\.agents\skills\"
```

#### Cursor / Windsurf

These editors use the same skill format. Copy to your configured skills directory, typically:

```bash
# Cursor
cp -r tourism-management-writing ~/.cursor/skills/

# Windsurf
cp -r tourism-management-writing ~/.windsurf/skills/
```

#### Manual (Any Agent)

If your agent supports custom markdown-based skills, you can:

1. Point the agent's skills path to the cloned directory
2. Or directly reference `SKILL.md` in your agent's configuration
3. Or concatenate `SKILL.md` + relevant reference files into a single prompt

The skill format follows the [agentskills.io specification](https://agentskills.io/specification) with YAML frontmatter (`name` + `description` fields).

---

## How to Use

### Quick Start

Once installed, trigger the skill by describing your task naturally. The agent will detect the skill automatically. Examples:

```
"I'm writing a paper on tourist behavior and social media influence.
Help me position the contribution and choose a journal."

"My conceptual model and hypotheses are ready. Help me design
the measurement scales and survey instrument."

"I've collected survey data from 500 hotel guests. Run the SEM
analysis and generate the results tables."

"Write the full paper draft for Annals of Tourism Research."
```

### Pipeline Mode

For a complete 0-to-draft workflow, say:

```
"Take me through the full tourism management writing pipeline.
My topic is [describe your topic]."
```

The agent will:
1. Load the skill and assess your current stage
2. Execute Stage 1 (positioning) → get confirmation
3. Proceed to Stage 2 (theoretical framework) → get confirmation
4. Continue through Stage 5 (full draft)
5. Output a complete manuscript with proper formatting

### Stage-Specific Mode

Jump to any stage:

| Trigger Phrase | Stage |
|---------------|-------|
| "I have a research idea about..." | Stage 1: Positioning |
| "Help me build the theoretical framework" | Stage 2: Theory & Literature |
| "Help me design the research methodology" | Stage 3: Research Design |
| "Help me analyze my survey/interview data" | Stage 4: Data Analysis |
| "Write the full paper" | Stage 5: Assembly |

### Reference-Only Mode

The skill also works as a passive reference. Just ask:

```
"What are Tourism Management's expectations for qualitative rigor?"
"How should I structure the hypothesis development for JTR?"
"What's the standard scale validation procedure for IJCHM?"
```

---

## File Structure

```
tourism-management-writing/
├── SKILL.md                              # Main skill file
│   ├── Journal Selection Quick Reference
│   ├── 0-to-Draft Pipeline (5 stages)
│   ├── Methodology Decision Framework
│   └── Cross-References to all reference files
│
├── references/
│   ├── journal-characteristics.md        # 6 journals: detailed profiles
│   ├── theoretical-framework.md          # Conceptual models, hypothesis writing
│   ├── quantitative-methods.md           # SEM, CFA, regression, tourism demand
│   ├── qualitative-methods.md            # Grounded theory, ethnography, thematic
│   ├── measurement-scales.md             # Scale development, validation, adaptation
│   ├── mixed-methods.md                  # Integration designs, joint displays
│   ├── reviewer-expectations.md          # What reviewers look for, rebuttal tips
│   └── writing-patterns.md               # Reusable writing patterns
│
├── assets/
│   └── conceptual-model-examples.md      # Annotated conceptual model examples
│
├── examples/
│   ├── manuscript_template.tex           # LaTeX template
│   ├── sem_analysis.R                    # SEM analysis template (lavaan)
│   └── qualitative_coding.py             # Thematic analysis template
│
├── README.md                             # This file
├── README.zh-CN.md                       # Chinese
├── README.ja.md                          # Japanese
├── README.ko.md                          # Korean
└── LICENSE                               # MIT License
```

---

## Covered Journals

| Journal | Abbreviation | Core Identity |
|---------|-------------|---------------|
| Tourism Management | TM | Broad tourism, high rigor, policy & practice relevance |
| Annals of Tourism Research | ATR | Theoretical depth, sociological/anthropological lens |
| Journal of Travel Research | JTR | Quantitative focus, consumer behavior, destination marketing |
| Int. J. Hospitality Management | IJHM | Hospitality operations, HR, service management |
| Int. J. Contemporary Hospitality Mgmt | IJCHM | Contemporary issues, innovation, strategic hospitality |
| Journal of Sustainable Tourism | JST | Sustainability, ethics, community impact, environment |

### Methodology by Journal Preference

| Method | TM | ATR | JTR | IJHM | IJCHM | JST |
|--------|-----|------|------|------|-------|-----|
| Quantitative (SEM, regression) | ✓✓✓ | ✓ | ✓✓✓ | ✓✓✓ | ✓✓✓ | ✓✓ |
| Qualitative (grounded theory, ethnography) | ✓✓ | ✓✓✓ | ✓ | ✓✓ | ✓✓ | ✓✓✓ |
| Mixed methods | ✓✓ | ✓✓ | ✓✓ | ✓✓ | ✓✓✓ | ✓✓✓ |
| Scale development | ✓✓✓ | ✓ | ✓✓✓ | ✓✓✓ | ✓✓✓ | ✓✓ |
| Tourism demand modeling | ✓✓✓ | ✓ | ✓✓✓ | ✓ | — | — |
| Systematic review / meta-analysis | ✓✓ | ✓✓✓ | ✓✓ | ✓✓ | ✓✓✓ | ✓✓ |

---

## Customization

### Adding a Journal

Edit `references/journal-characteristics.md` and add a new section following the template:

```markdown
### Your Journal Name

**Publisher**: ...
**Focus**: ...
**Key characteristics**:
- ...
**Methodology preferences**: ...
**What it values most**:
1. ...
```

### Adapting the SEM Template

The SEM analysis uses `lavaan` syntax. Modify in `examples/sem_analysis.R`:

```r
model <- '
  # Measurement model
  Satisfaction =~ sat1 + sat2 + sat3 + sat4
  Loyalty =~ loy1 + loy2 + loy3
  # Structural model
  Loyalty ~ Satisfaction + ServiceQuality
'
```

### Creating a New Paper Template

1. Copy `examples/manuscript_template.tex` as your starting point
2. Replace the title, author, and abstract
3. Fill in your conceptual model, methodology, and results
4. Compile with: `xelatex manuscript.tex` (two passes)

---

## Example Output

The `examples/` directory contains reference files:

1. **`manuscript_template.tex`**: A clean LaTeX template with placeholder sections following the tourism paper structure (Introduction → Literature & Framework → Methodology → Results → Discussion & Implications).

2. **`sem_analysis.R`**: A runnable R template for structural equation modeling with lavaan — measurement model CFA, structural model testing, fit indices, and mediation analysis.

3. **`qualitative_coding.py`**: A Python template for thematic analysis workflow — coding, theme development, and trustworthiness documentation.

---

## Requirements

- **AI Agent**: OpenCode, Claude Code, Codex, Cursor, Windsurf, or any agent supporting the agentskills.io format
- **For LaTeX compilation** (examples): XeLaTeX or pdfLaTeX with `amsmath`, `booktabs`, `natbib`, `geometry`, `setspace`, `enumitem`, `hyperref`, `caption`, `tikz` (for conceptual models)
- **For quantitative analysis** (examples): R 4.0+ with `lavaan`, `semTools`, `psych`
- **For qualitative analysis** (examples): Python 3.10+ with `numpy`, `pandas`

---

## Contributing

Contributions are welcome. Areas where help is especially valuable:

- **Journal profiles**: Detailed editorial statements and reviewer expectations for additional tourism journals
- **Writing patterns**: Additional reusable patterns distilled from published tourism papers
- **Methodology templates**: Analysis templates for SmartPLS, Mplus, NVivo workflows
- **Measurement scales**: Validated scales catalog across tourism/hospitality constructs
- **Multi-language support**: Chinese/Korean/Japanese tourism writing conventions

Please open an issue or pull request on GitHub.

---

## License

MIT License — see [LICENSE](LICENSE) file.

---

## Acknowledgments

Built using the [agentskills.io](https://agentskills.io) specification and the skill authoring methodology from [OpenCode](https://github.com/anomalyco/opencode). The tourism & hospitality domain knowledge draws on editorial statements from Elsevier journals (Tourism Management, ATR, IJHM, IJCHM), Sage (JTR), and Taylor & Francis (JST).
