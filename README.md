# loglass-dev-skills

Loglass の開発用 Claude Code プラグイン集。

## プラグイン一覧

| プラグイン | 説明 | バージョン |
|------------|------|------------|
| [diagrams](./plugins/diagrams/) | draw.io (.drawio) でアーキテクチャ図、ER図、フローチャート等を作成・編集 | 1.0.0 |

## インストール

### 1. マーケットプレイスを追加

```
/plugin marketplace add loglass/loglass-dev-skills
```

### 2. プラグインをインストール

```
/plugin install diagrams@loglass-dev-skills
```

### プラグイン個別インストール

必要なプラグインだけ選んでインストールできます。全プラグインが一括でインストールされることはありません。

## 使い方

### diagrams プラグイン

draw.io 形式 (.drawio) のダイアグラムを作成・読み込み・編集できます。

**対応する図の種類:**
- アーキテクチャ図（オニオンアーキテクチャ、レイヤー構造）
- ER図
- フローチャート
- ワイヤーフレーム
- シーケンス図
- クラス図
- ドメインモデル図

**使用例:**

```text
「アーキテクチャ図を作って」
「ER図を作成して。User(id, name, email) → Order(id, user_id, total)」
「この .drawio ファイルを開いて」
「図に何が書いてあるか説明して」
「フローチャートに処理Dを追加して」
```

## 前提条件

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) がインストール済みであること
- draw.io デスクトップアプリがインストール済みであること（`brew install --cask drawio`）

## コントリビューション

プラグインの追加・改善の提案は Issue または Pull Request でお願いします。

### プラグインの追加方法

1. `plugins/<プラグイン名>/` ディレクトリを作成
2. `.claude-plugin/plugin.json` にマニフェストを配置
3. `skills/<スキル名>/SKILL.md` にスキル定義を配置
4. ルートの `.claude-plugin/marketplace.json` にプラグイン情報を追加

## ライセンス

MIT License
