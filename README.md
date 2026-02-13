# loglass-dev-skills

Loglass の開発用 Claude Code プラグイン集。

Claude Code plugin collection for Loglass development.

## 言語ポリシー / Language Policy

このリポジトリは日本語話者と英語話者が混在する環境を想定していますが、メンテナンスは日本語で行います。

This repository assumes a mixed Japanese and English speaking environment, but maintenance is done in Japanese.

- **フロントマター**: 英語 / Frontmatter: English
- **README**: 日本語を記載し、その下に英語も併記 / README: Japanese with English translation below
- **SKILL.md と参照ドキュメント**: 日本語 / SKILL.md and reference docs: Japanese

## プラグイン一覧 / Plugin List

| プラグイン / Plugin | 説明 / Description | バージョン / Version |
|------------|------|------------|
| [drawio](./plugins/drawio/) | draw.io (.drawio) でアーキテクチャ図、ER図、フローチャート等を作成・編集<br>Create and edit architecture diagrams, ER diagrams, flowcharts, etc. with draw.io | 1.0.0 |

## インストール / Installation

### 1. マーケットプレイスを追加 / Add Marketplace

```
/plugin marketplace add loglass/loglass-dev-skills
```

### 2. プラグインをインストール / Install Plugin

必要なプラグインだけ選んでインストールできます。全プラグインが一括でインストールされることはありません。

You can selectively install only the plugins you need. All plugins will not be installed at once.

```
/plugin install drawio@loglass-dev-skills
```

## 使い方 / Usage

### drawio プラグイン / drawio Plugin

draw.io 形式 (.drawio) のダイアグラムを作成・読み込み・編集できます。

Create, read, and edit diagrams in draw.io format (.drawio).

**対応する図の種類 / Supported Diagram Types:**
- アーキテクチャ図（オニオンアーキテクチャ、レイヤー構造）/ Architecture diagrams (Onion architecture, layered structure)
- ER図 / ER diagrams
- フローチャート / Flowcharts
- ワイヤーフレーム / Wireframes
- シーケンス図 / Sequence diagrams
- クラス図 / Class diagrams
- ドメインモデル図 / Domain model diagrams

**使用例 / Usage Examples:**

```text
「アーキテクチャ図を作って」 / "Create an architecture diagram"
「ER図を作成して。User(id, name, email) → Order(id, user_id, total)」 / "Create an ER diagram: User(id, name, email) → Order(id, user_id, total)"
「この .drawio ファイルを開いて」 / "Open this .drawio file"
「図に何が書いてあるか説明して」 / "Explain what's in the diagram"
「フローチャートに処理Dを追加して」 / "Add process D to the flowchart"
```

## 前提条件 / Prerequisites

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) がインストール済みであること / Claude Code must be installed
- draw.io デスクトップアプリがインストール済みであること（`brew install --cask drawio`） / draw.io desktop app must be installed (`brew install --cask drawio`)

## コントリビューション / Contributing

プラグインの追加・改善の提案は Issue または Pull Request でお願いします。

Suggestions for adding or improving plugins are welcome via Issues or Pull Requests.

### プラグインの追加方法 / How to Add Plugins

1. `plugins/<プラグイン名>/` ディレクトリを作成 / Create `plugins/<plugin-name>/` directory
2. `plugins/<プラグイン名>/.claude-plugin/plugin.json` にマニフェストを配置 / Place manifest in `plugins/<plugin-name>/.claude-plugin/plugin.json`
3. `plugins/<プラグイン名>/skills/<スキル名>/SKILL.md` にスキル定義を配置 / Place skill definition in `plugins/<plugin-name>/skills/<skill-name>/SKILL.md`
4. ルートの `.claude-plugin/marketplace.json` にプラグイン情報を追加 / Add plugin info to root `.claude-plugin/marketplace.json`

## ライセンス / License

MIT License
