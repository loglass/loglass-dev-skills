# drawio

draw.io (.drawio) 形式のダイアグラムを作成・読み込み・編集するプラグイン。

draw.io (.drawio) diagram plugin for creating, reading, and editing diagrams.

## 機能 / Features

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

## インストール / Installation

```
/plugin marketplace add loglass/loglass-dev-skills
/plugin install drawio@loglass-dev-skills
```

## 使用例 / Usage Examples

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

## スキル / Skills

- `drawio`: draw.io ファイルの作成・編集・読み込み / Create, edit, and read draw.io files

詳細は [SKILL.md](./skills/drawio/SKILL.md) を参照してください。

See [SKILL.md](./skills/drawio/SKILL.md) for details.

## ライセンス / License

MIT License
