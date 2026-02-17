# drawio

draw.io (.drawio) 形式のダイアグラムを作成・読み込み・編集するプラグイン。

> このドキュメントの言語方針については[言語ポリシー](../../README.md#言語ポリシー)を参照してください。  
> For language policy, see [Language Policy](../../README.md#language-policy).  
> 
> English version is available [below](#features).

## 機能

draw.io 形式 (.drawio) のダイアグラムを作成・読み込み・編集できます。

**対応する図の種類:**
- アーキテクチャ図
- ER図
- フローチャート
- ワイヤーフレーム
- シーケンス図
- クラス図
- ドメインモデル図
- オブジェクト図

## 前提条件

### draw.io デスクトップアプリ

draw.io デスクトップアプリがインストール済みであること。

**macOS:**

```bash
brew install --cask drawio
```

**Windows:**

```powershell
winget install -e --id JGraph.Draw
```

### AI コーディングツール

以下のいずれかが利用可能であること。

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) CLI
- [Cursor](https://www.cursor.com/) (Agent Skills 対応)

## インストール

### Claude Code CLI（ターミナル）

ターミナルで `claude` を起動し、以下のコマンドを実行してください。

```
/plugin marketplace add loglass/loglass-dev-skills
/plugin install drawio@loglass-dev-skills
```

#### 自動更新の設定（推奨）

プラグインを常に最新の状態に保つため、マーケットプレイスの自動更新を有効にしてください。

1. `/plugin` を実行
2. **Marketplaces** タブを選択
3. **loglass-dev-skills** を選択
4. **Enable auto-update** を選択

> 一度設定すれば、以降はプラグインの更新が自動的に適用されます。

### Cursor の場合

SKILL.md は[オープン標準](https://www.mintlify.com/blog/skill-md)として複数の AI コーディングツールで対応しています。このリポジトリをクローンし、Cursor のグローバルスキルディレクトリ (`~/.cursor/skills/`) へシンボリックリンクを作成してください。

1. リポジトリをクローン（任意の場所）:

   ```bash
   git clone https://github.com/loglass/loglass-dev-skills.git
   ```

2. グローバルスキルディレクトリにシンボリックリンクを作成:

   ```bash
   mkdir -p ~/.cursor/skills
   ln -s {loglass-dev-skills}/plugins/drawio/skills/drawio ~/.cursor/skills/drawio
   ```

   `{loglass-dev-skills}` はクローン先の絶対パスに置き換えてください。

   これにより、全プロジェクトで drawio スキルが利用可能になります。AI が `SKILL.md` の `description` フロントマターを読み取り、関連タスク（「図を作って」等）を検知すると自動的にスキルを読み込みます。

> **Windows の場合:** [Windows Cursor セットアップガイドの Wiki](https://github.com/loglass/loglass-dev-skills/wiki/draw.io%E3%82%B9%E3%82%AD%E3%83%AB-Cursor-Windows%E3%81%AE%E5%A0%B4%E5%90%88%E3%81%AE%E3%82%BB%E3%83%83%E3%83%88%E3%82%A2%E3%83%83%E3%83%97%E3%82%AC%E3%82%A4%E3%83%89)を参照してください。

## 使用例

```text
「アーキテクチャ図を作って」
「ER図を作成して。User(id, name, email) → Order(id, user_id, total)」
「この .drawio ファイルを開いて」
「図に何が書いてあるか説明して」
「フローチャートに処理Dを追加して」
```

## Tips

### 推奨設定

**ライトモード:**

「拡張 → 外観 → ライト」(Extras → Appearance → Light) を選択してください。ダークモードだと draw.io の色が反転して表示される問題があります。

**自動保存:**

「拡張 → 自動保存」(Extras → Autosave) を ON にしてください。Claude Code が .drawio ファイルを編集した際、draw.io アプリ側に自動的に反映されます。

### Google ドライブ連携

.drawio ファイルを Google ドライブに保存し、[Google Drive for Desktop](https://www.google.com/drive/download/) でローカル同期すると、チームでの図の共有・バージョン管理に便利です。

## スキル

- `drawio`: draw.io ファイルの作成・編集・読み込み

詳細は [SKILL.md](./skills/drawio/SKILL.md) を参照してください。

---

## Features

Create, read, and edit diagrams in draw.io format (.drawio).

> For language policy, see [Language Policy](../../README.md#language-policy).

**Supported Diagram Types:**
- Architecture diagrams
- ER diagrams
- Flowcharts
- Wireframes
- Sequence diagrams
- Class diagrams
- Domain model diagrams
- Object diagrams

## Prerequisites

### draw.io Desktop App

draw.io desktop app must be installed.

**macOS:**

```bash
brew install --cask drawio
```

**Windows:**

```powershell
winget install -e --id JGraph.Draw
```

### AI Coding Tool

One of the following must be available:

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) CLI
- [Cursor](https://www.cursor.com/) (Agent Skills supported)

## Installation

### Claude Code CLI (Terminal)

Launch `claude` in your terminal and run the following commands.

```
/plugin marketplace add loglass/loglass-dev-skills
/plugin install drawio@loglass-dev-skills
```

#### Auto-Update Setup (Recommended)

To keep plugins up to date automatically, enable auto-update for the marketplace.

1. Run `/plugin`
2. Select the **Marketplaces** tab
3. Select **loglass-dev-skills**
4. Select **Enable auto-update**

> Once configured, plugin updates will be applied automatically.

### For Cursor Users

SKILL.md is an [open standard](https://www.mintlify.com/blog/skill-md) supported by multiple AI coding tools. Clone this repository and create a symbolic link in Cursor's global skills directory (`~/.cursor/skills/`).

1. Clone the repository (to any location):

   ```bash
   git clone https://github.com/loglass/loglass-dev-skills.git
   ```

2. Create a symbolic link in the global skills directory:

   ```bash
   mkdir -p ~/.cursor/skills
   ln -s {loglass-dev-skills}/plugins/drawio/skills/drawio ~/.cursor/skills/drawio
   ```

   Replace `{loglass-dev-skills}` with the absolute path to the cloned repository.

   This makes the drawio skill available across all projects. The AI reads the `description` frontmatter in `SKILL.md` and automatically loads the skill when it detects a relevant task (e.g., "create a diagram").

> **On Windows:** See the [Windows Cursor Setup Guide on wiki](https://github.com/loglass/loglass-dev-skills/wiki/draw.io%E3%82%B9%E3%82%AD%E3%83%AB-Cursor-Windows%E3%81%AE%E5%A0%B4%E5%90%88%E3%81%AE%E3%82%BB%E3%83%83%E3%83%88%E3%82%A2%E3%83%83%E3%83%97%E3%82%AC%E3%82%A4%E3%83%89).

## Usage Examples

```text
"Create an architecture diagram"
"Create an ER diagram: User(id, name, email) → Order(id, user_id, total)"
"Open this .drawio file"
"Explain what's in the diagram"
"Add process D to the flowchart"
```

## Tips

### Recommended Settings

**Light Mode:**

Select "Extras → Appearance → Light". Dark mode causes color inversion issues in draw.io.

**Autosave:**

Enable "Extras → Autosave". When Claude Code edits a .drawio file, changes will be automatically reflected in the draw.io app.

### Google Drive Integration

Save .drawio files to Google Drive and sync locally with [Google Drive for Desktop](https://www.google.com/drive/download/) for convenient team sharing and version management.

## Skills

- `drawio`: Create, edit, and read draw.io files

See [SKILL.md](./skills/drawio/SKILL.md) for details.
