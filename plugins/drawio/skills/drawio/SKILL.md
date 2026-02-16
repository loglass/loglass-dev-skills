---
name: drawio
description: draw.io (.drawio) ファイルの作成・読み込み・編集・開く。アーキテクチャ図、ER図、フローチャート、ドメインモデル図など各種ダイアグラムに対応。「図を作って」「ダイアグラムを作成」「アーキテクチャ図」「ER図」「オブジェクト図」「.drawioを開いて」「ドメインモデルを確認」「図に何が書いてある？」などのリクエスト時に使用。Mermaid記法やPlantUMLの生成には使用しない。
---

# draw.io ダイアグラム スキル

draw.io 形式 (.drawio) のダイアグラムを作成・読み込み・編集する。

## 対応する図の種類（例）

- アーキテクチャ図
- ドメインモデル図
- オブジェクト図
- ER図
- フローチャート
- ワイヤーフレーム
- シーケンス図
- クラス図

上記以外のダイアグラムも draw.io で表現できるものであれば対応可能。

## ワークフロー

### 1. 読み込み（開発時の参照）

ドメインモデルやアーキテクチャ図を読み込んで、開発のコンテキストとして活用する。

**トリガー例:** 「ドメインモデルを確認して」「設計図を読んで」「アーキテクチャを参照して」「図に何が書いてある？」

**手順:**

1. **参照ファイル読み込み**: 以下を読み込む
   - [references/xml-reference.md](references/xml-reference.md) — mxCell パターン、解析例
2. `Glob` で `.drawio` ファイルを検索
3. `Read` で XML を読み込み
4. `mxCell` の属性から情報を抽出:
   - `value` 属性: ラベル（エンティティ名、メソッド名など）
   - `parent` 属性: 親子関係（グループ所属）
   - `source`/`target` 属性: エッジの接続関係
   - `style` 属性の `fillColor`: 要素の分類（色による区別）
5. 構造化された情報として要約を出力

### 2. 作成・編集

新規ダイアグラムの作成、または既存 .drawio ファイルの更新を行う。

**トリガー例:** 「図を作って」「ダイアグラムを作成」「アーキテクチャ図を書いて」「ER図を作って」「図を更新して」「エンティティを追加して」「関連を変更して」

**手順:**

1. **要件確認**: ユーザーから図の種類・含める要素を確認する
2. **参照ファイル読み込み**: 以下を **必ず** 読み込んでから作業を開始する
   - [references/xml-reference.md](references/xml-reference.md) — mxCell パターン、スタイル、カラーパレット
   - [references/layout-guide.md](references/layout-guide.md) — レイアウト原則、座標計算
3. **既存ファイル確認**: `Glob` で対象の `.drawio` を検索
   - **既存ファイルあり** → `Read` で XML を取得し、既存の ID を確認する
   - **既存ファイルなし** → 新規作成として進める
4. **要素の洗い出し**: ボックス、関係性、グループを列挙する
5. **XML 生成・編集**:
   - **新規作成**: 基本構造テンプレート + mxCell を組み合わせ、`Write` で `.drawio` として保存
   - **既存編集**: 既存 ID と重複しない新しい ID を付与し、`Edit` で XML を更新
6. **パス表示**: ファイルパスをユーザーに伝える（自動で開かない）

### 3. デスクトップアプリで開く

**トリガー例:** 「このファイルを開いて」「.drawioを開く」「図を開いて」

**手順:**

1. ファイルパスを特定（指定がなければ `Glob` で `.drawio` を検索）
2. `Bash` で `open -a "draw.io" <ファイルパス>` を実行

前提: `brew install --cask drawio` でインストール済みであること

## XML 基本構造

**重要:** `darkMode="0"` を必ず指定すること。Adaptive Colors を無効化し、ダークモードのエディタで開いても色が反転せず、SVG/PNG エクスポート時もライトモードの色を維持できる。

```xml
<mxfile host="app.diagrams.net" agent="Claude" version="21.0.0">
  <diagram name="ダイアグラム名" id="unique-id">
    <mxGraphModel dx="1200" dy="800" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827" math="0" shadow="0" darkMode="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <!-- 要素をここに追加 -->
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

複数ページが必要な場合は `<diagram>` を複数並べる。各 `<mxGraphModel>` に `darkMode="0"` を指定する。

## 重要な制約

- **`darkMode="0"` を必ず指定** — 省略するとダークモードで色が反転する
- **ID は一意にする** — `box1`, `edge1` など接頭辞をつけて管理する
- **改行は `&#xa;` を使用** — XML 内のテキスト改行
- **親子関係は `parent` 属性で指定** — グループ内の子要素の座標は親からの相対位置
- **`vertex="1"` は図形、`edge="1"` はエッジ**
- **編集後は自動で開かない** — ファイルパスを表示するだけ。ユーザーが「開いて」と言った時のみ開く
- **XMLコメントに `--` を含めない** — `<!-- Order ---> Customer -->` はXMLエラーになる。`<!-- Order to Customer -->` のように書く

## トラブルシューティング

### XMLパースエラー

**原因:** コメント内に `--` が含まれている
**解決:** `<!-- Order to Customer -->` のように `--` を避ける。詳細は [references/xml-reference.md](references/xml-reference.md) の冒頭を参照

### ダークモードで色が反転する

**原因:** `darkMode="0"` の指定漏れ
**解決:** `<mxGraphModel>` に `darkMode="0"` を追加する。複数ページの場合は全ページに指定する

### 図形が重なる / エッジが交差する

**原因:** レイアウト計算の問題
**解決:** [references/layout-guide.md](references/layout-guide.md) のレイアウト原則を確認。エッジの接続位置を `exitX`/`exitY`/`entryX`/`entryY` で分散させる

### ID 重複でレンダリングが崩れる

**原因:** 同じ ID の mxCell が複数存在する
**解決:** 編集前に既存の ID を確認し、一意な ID を付与する

### draw.io アプリが開かない

**原因:** draw.io デスクトップアプリが未インストール
**解決:** `brew install --cask drawio` でインストールする

## 参照ファイル

- **XML パターン & スタイル** → [references/xml-reference.md](references/xml-reference.md)
  内容: mxCell パターン（矩形・テキスト・エッジ・グループ・DB・スタックレイアウト）、スタイル属性、カラーパレット、エッジスタイル、カスタムプロパティ、接続ポイント、読み込み時の解析例
  **読み込み・作成・編集で読み込むこと**

- **レイアウトガイド** → [references/layout-guide.md](references/layout-guide.md)
  内容: レイアウト原則、座標計算、配置パターン、境界線の座標計算
  **作成・編集で読み込むこと**
