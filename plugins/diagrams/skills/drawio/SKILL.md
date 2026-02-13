---
name: drawio
description: draw.io (.drawio) ファイルの作成・読み込み・編集・開く。アーキテクチャ図、ER図、フローチャート、ワイヤーフレーム、シーケンス図、クラス図、ドメインモデル図に対応。「図を作って」「ダイアグラムを作成」「アーキテクチャ図」「ER図」「.drawioを開いて」「ドメインモデルを確認」「図に何が書いてある？」などのリクエスト時に使用。
---

# draw.io ダイアグラム スキル

draw.io 形式 (.drawio) のダイアグラムを作成・読み込み・編集する。

## 主な用途

### 1. 読み込み（開発時の参照）

ドメインモデルやアーキテクチャ図を読み込んで、開発のコンテキストとして活用する。

```text
ユーザー: 「ドメインモデルを確認して」「設計図を読んで」「アーキテクチャを参照して」
```

**読み込み手順:**
1. `Glob` で `.drawio` ファイルを検索
2. `Read` で XML を読み込み
3. `mxCell` の `value` 属性からエンティティ名・関係性を抽出
4. 構造化された情報として要約

**XML からの情報抽出:**
- `value` 属性: ラベル（エンティティ名、メソッド名など）
- `parent` 属性: 親子関係（グループ所属）
- `source`/`target` 属性: エッジの接続関係
- `style` 属性の `fillColor`: 要素の分類（色による区別）

### 2. 作成（新規ダイアグラム）

Markdown や要件から draw.io 形式のダイアグラムを作成する。

### 3. 編集（既存ファイルの更新）

既存の .drawio ファイルに要素を追加・変更する。

### 4. デスクトップアプリで開く

```text
ユーザー: 「このファイルを開いて」「.drawioを開く」「図を開いて」
```

**手順:**
1. ファイルパスを特定（指定がなければ `Glob` で `.drawio` を検索）
2. `Bash` で `open -a "draw.io" <ファイルパス>` を実行（※ `brew install --cask drawio` でインストール済みの前提）

## 対応する図の種類

| 種類             | 用途                       |
|------------------|----------------------------|
| アーキテクチャ図 | システム構成、レイヤー構造 |
| ER図             | エンティティ関係           |
| フローチャート   | 処理フロー、状態遷移       |
| ワイヤーフレーム | 画面レイアウト             |
| シーケンス図     | 処理の流れ                 |
| クラス図         | オブジェクト構造           |
| ドメインモデル図 | 集約、エンティティ、関連   |

## XML 基本構造

🚨 **重要**: `darkMode="0"` を必ず指定すること（Adaptive Colors 無効化）

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

**`darkMode="0"` の効果:**
- Adaptive Colors が無効化され、常にライトモードの色で表示
- ダークモードのエディタで開いても色が反転しない
- SVG/PNG エクスポート時もライトモードの色を維持

### 複数ページ

1つのファイルに複数ページを含める場合：

```xml
<mxfile host="app.diagrams.net" agent="Claude" version="21.0.0">
  <diagram name="概要" id="page1">
    <mxGraphModel ... darkMode="0">
      <root>...</root>
    </mxGraphModel>
  </diagram>
  <diagram name="詳細" id="page2">
    <mxGraphModel ... darkMode="0">
      <root>...</root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

## mxCell 基本パターン

### 矩形（ボックス）

```xml
<mxCell id="box1" value="ラベル" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### テキスト

```xml
<mxCell id="text1" value="テキスト内容" style="text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=0;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="100" height="30" as="geometry" />
</mxCell>
```

### 矢印（エッジ）

```xml
<mxCell id="edge1" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;" edge="1" parent="1" source="box1" target="box2">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

## 作成手順

1. **要件を確認**: 何を図にするか（アーキテクチャ、フロー、ER等）
2. **要素を洗い出す**: ボックス、関係性、グループ
3. **レイアウトを決める**: 座標計算（grid=10を意識）
4. **XMLを生成**: 基本構造 + mxCell を組み合わせ
5. **ファイル出力**: プロジェクトの適切なディレクトリに `.drawio` として保存

## 注意事項

- 🚨 **`darkMode="0"` を必ず指定** - Adaptive Colors を無効化してライトモード固定
- ID は一意にする（`box1`, `edge1` など接頭辞をつける）
- 改行は `&#xa;` を使用
- 親子関係は `parent` 属性で指定
- グループ内の子要素の座標は親からの相対位置
- `vertex="1"` は図形、`edge="1"` はエッジ
- **編集後は自動で開かない** - ファイルパスを表示するだけでOK。ユーザーが「開いて」と言った時のみ開く

## 読み込み時の解析例

### アーキテクチャ図から構造を抽出

```xml
<mxCell id="domain-group" value="domain/" style="swimlane;..." />
<mxCell id="usecase-group" value="usecase/" style="swimlane;..." />
<mxCell id="arrow1" source="usecase-group" target="domain-group" edge="1" />
```

↓ 解析結果

```text
レイヤー構造:
- domain/ (青: #dae8fc) - 中心層
- usecase/ (黄: #fff2cc) - ユースケース層

依存関係:
- usecase → domain (依存)
```

### ドメインモデルから用語を抽出

```xml
<mxCell id="entity1" value="注文&#xa;Order" style="rounded=1;fillColor=#dae8fc;..." />
<mxCell id="entity2" value="顧客&#xa;Customer" style="rounded=1;fillColor=#dae8fc;..." />
<mxCell id="edge1" source="entity1" target="entity2" style="..." edge="1" />
```

↓ 解析結果

```text
エンティティ:
- 注文 (Order)
- 顧客 (Customer)

関連:
- 注文 → 顧客
```

## 開発時の活用パターン

| パターン   | 説明                                                     | 例                                                         |
|------------|----------------------------------------------------------|------------------------------------------------------------|
| 実装前確認 | ドメインモデル図を読み込んでユビキタス言語を確認         | 「ドメインモデルを読んで、Order 集約の構成を教えて」       |
| 設計参照   | アーキテクチャ図を参照してレイヤー間の依存方向を確認     | 「アーキテクチャ図を確認して、依存関係を教えて」           |
| 図の作成   | 設計議論の結果をダイアグラムとして可視化                 | 「この設計をドメインモデル図にして」                       |
| 図の更新   | 実装変更に合わせて既存の図も更新                         | 「Order に status フィールドを追加して」                    |
| レビュー   | 図と実装の整合性をチェック                               | 「この図と実装が合っているか確認して」                     |

## 参照ファイル

- **XML パターン & スタイル** → [references/xml-reference.md](references/xml-reference.md)
  内容: 拡張 mxCell パターン（グループ、DB、スタックレイアウト）、スタイル属性、カラーパレット、エッジスタイル、カスタムプロパティ、接続ポイント
  読み込みタイミング: 高度な図形を使った作成・編集時

- **レイアウトガイド** → [references/layout-guide.md](references/layout-guide.md)
  内容: レイアウト原則、座標計算、配置パターン、境界線の座標計算
  読み込みタイミング: 新規図の作成時やエッジの重なり修正時
