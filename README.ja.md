# 観光・ホスピタリティ経営 学術論文作成スキル

[English](README.md) | [简体中文](README.zh-CN.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

OpenCode / Claude Code / Codex 向けの観光・ホスピタリティ経営学術論文作成スキル。トピック選定から理論的枠組み、研究設計、データ分析、完全な初稿までをカバーします。

観光・ホスピタリティ分野の主要6誌に対応：**Tourism Management, Annals of Tourism Research, JTR, IJHM, IJCHM, JST**。

## 機能

AIエージェントを **0→初稿 5ステージパイプライン** でガイドします：

| ステージ | 成果物 | 主な出力 |
|---------|--------|---------|
| **S1**: トピック選定 | ギャップ表、ジャーナル推薦、貢献ステートメント | どのジャーナルか + 何が新しいか |
| **S2**: 理論的枠組み | 概念モデル、仮説導出、文献統合 | §2 文献・枠組み 草案 |
| **S3**: 研究設計 | 方法論設計図（定量/定性/混合）、測定尺度、標本計画 | §3 方法論 草案 |
| **S4**: データ分析 | 定量（SEM、回帰、観光需要）または定性（グラウンデッド・セオリー、エスノグラフィー、テーマ分析）の結果 | §4-5 分析結果 草案 |
| **S5**: 執筆・組立 | Introduction、考察、理論的・実践的示唆、Abstract | 完全初稿 |

**ドメイン特化型**：観光・ホスピタリティジャーナル固有の慣習（概念モデル提示構造、尺度開発基準、定性研究の信頼性基準、混合研究法統合フレームワーク、査読者期待など）を組み込んでいます。

---

## インストール

### 1. リポジトリのクローン

```bash
git clone https://github.com/liyuanbo1024/tourism-management-writing.git
```

### 2. AIエージェントへのインストール

| エージェント | インストールコマンド |
|-------------|-------------------|
| **OpenCode** | `cp -r tourism-management-writing ~/.config/opencode/skills/` |
| **Claude Code** | `cp -r tourism-management-writing ~/.claude/skills/` |
| **Codex** | `cp -r tourism-management-writing ~/.agents/skills/` |
| **Cursor** | `cp -r tourism-management-writing ~/.cursor/skills/` |
| **Windsurf** | `cp -r tourism-management-writing ~/.windsurf/skills/` |

インストール後、自然言語でスキルを起動できます：
- `SNSが観光行動に与える影響について論文を書きたい。ポジショニングを手伝って`
- `概念的モデルと仮説ができた。測定尺度を設計して`
- `観光経営の論文執筆パイプラインを全部通して`

---

## 使い方

### パイプラインモード

```
「観光経営論文執筆パイプラインを通して実行して。私のトピックは…」
```

エージェントが現在の段階を評価し、S1→S5まで順次実行。各段階で確認を取ります。

### ステージジャンプ

| トリガーフレーズ | ジャンプ先 |
|----------------|----------|
| 「研究アイデアがある…」 | S1: トピック選定 |
| 「理論的枠組みを構築して」 | S2: 理論的枠組み |
| 「研究方法を設計して」 | S3: 研究設計 |
| 「調査/インタビューデータを分析して」 | S4: データ分析 |
| 「完全な論文を書いて」 | S5: 執筆・組立 |

### リファレンスモード

```
「Tourism Management の定性研究の厳密性基準は？」
「JTR の仮説導出はどう構成すべき？」
```

---

## 対応ジャーナル

| ジャーナル | 核となる特徴 |
|-----------|------------|
| Tourism Management (TM) | 広範な観光研究、高い厳密性、政策・実践との関連 |
| Annals of Tourism Research (ATR) | 理論的深さ、社会学・人類学的視点 |
| Journal of Travel Research (JTR) | 定量重視、消費者行動、デスティネーションマーケティング |
| Int. J. Hospitality Management (IJHM) | ホスピタリティ運営、人的資源管理、サービス経営 |
| Int. J. Contemporary Hospitality Mgmt (IJCHM) | 現代的課題、イノベーション、戦略的ホスピタリティ |
| Journal of Sustainable Tourism (JST) | 持続可能性、倫理、コミュニティ影響、環境 |

### ジャーナル別方法論の好み

| 方法 | TM | ATR | JTR | IJHM | IJCHM | JST |
|------|-----|------|------|------|-------|-----|
| 定量（SEM、回帰） | ✓✓✓ | ✓ | ✓✓✓ | ✓✓✓ | ✓✓✓ | ✓✓ |
| 定性（GT、エスノグラフィー） | ✓✓ | ✓✓✓ | ✓ | ✓✓ | ✓✓ | ✓✓✓ |
| 混合研究法 | ✓✓ | ✓✓ | ✓✓ | ✓✓ | ✓✓✓ | ✓✓✓ |
| 尺度開発 | ✓✓✓ | ✓ | ✓✓✓ | ✓✓✓ | ✓✓✓ | ✓✓ |
| 観光需要モデリング | ✓✓✓ | ✓ | ✓✓✓ | ✓ | — | — |
| 系統的レビュー/メタ分析 | ✓✓ | ✓✓✓ | ✓✓ | ✓✓ | ✓✓✓ | ✓✓ |

---

## ファイル構成

```
tourism-management-writing/
├── SKILL.md                              メインスキルファイル
├── references/                           8個の参照ファイル
├── assets/                               概念モデル例
├── examples/                             LaTeXテンプレート + R + Python
├── README.md / README.zh-CN.md / .ja.md / .ko.md
└── LICENSE
```

---

## ライセンス

MIT License — [LICENSE](LICENSE) 参照。

---

## 謝辞

[agentskills.io](https://agentskills.io) 仕様と [OpenCode](https://github.com/anomalyco/opencode) のスキル作成方法論に基づく。観光・ホスピタリティ分野の知識は Elsevier 誌（Tourism Management、ATR、IJHM、IJCHM）、Sage（JTR）、Taylor & Francis（JST）の編集声明に依拠。
