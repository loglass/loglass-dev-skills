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

## プラグイン詳細 / Plugin Details

各プラグインの詳細は、それぞれのディレクトリの README を参照してください。

For details on each plugin, please refer to the README in each directory.

- [drawio](./plugins/drawio/README.md): draw.io ダイアグラムツール / draw.io diagram tool

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
