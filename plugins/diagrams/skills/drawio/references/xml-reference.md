# XML パターン & スタイル リファレンス

draw.io の拡張 mxCell パターン、スタイル属性、カラーパレットのリファレンス。

## 拡張 mxCell パターン

### 点線矢印

```xml
<mxCell id="edge2" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;dashed=1;" edge="1" parent="1" source="box1" target="box2">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### エッジラベル

```xml
<mxCell id="edge-label" value="ラベル" style="edgeLabel;html=1;align=center;verticalAlign=middle;resizable=0;points=[];" vertex="1" connectable="0" parent="edge1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### グループ（swimlane）

```xml
<mxCell id="group1" value="グループ名" style="swimlane;fontStyle=1;startSize=26;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="1">
  <mxGeometry x="40" y="80" width="200" height="150" as="geometry" />
</mxCell>
<!-- 子要素は parent="group1" を指定 -->
<mxCell id="child1" value="子要素" style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="group1">
  <mxGeometry x="20" y="40" width="80" height="40" as="geometry" />
</mxCell>
```

### データベース（シリンダー）

```xml
<mxCell id="db1" value="DB名" style="shape=cylinder3;whiteSpace=wrap;html=1;boundedLbl=1;backgroundOutline=1;size=15;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="60" height="80" as="geometry" />
</mxCell>
```

### スタックレイアウト（UMLクラス風）

ER図やクラス図で使用する、フィールド一覧を持つ矩形。

```xml
<mxCell id="class1" value="クラス名" style="swimlane;fontStyle=1;childLayout=stackLayout;horizontal=1;startSize=30;horizontalStack=0;resizeParent=1;resizeParentMax=0;resizeLast=0;collapsible=1;marginBottom=0;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="160" height="90" as="geometry" />
</mxCell>
<mxCell id="class1-row1" value="+ field1: String" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;points=[[0,0.5],[1,0.5]];portConstraint=eastwest;rotatable=0;" vertex="1" parent="class1">
  <mxGeometry y="30" width="160" height="30" as="geometry" />
</mxCell>
<mxCell id="class1-row2" value="+ method(): void" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;points=[[0,0.5],[1,0.5]];portConstraint=eastwest;rotatable=0;" vertex="1" parent="class1">
  <mxGeometry y="60" width="160" height="30" as="geometry" />
</mxCell>
```

**高さの計算:**
- ヘッダー: `startSize`（30px）
- 各行: 30px
- 全体の高さ = startSize + (行数 × 30)

## カスタムプロパティ（メタデータ）

図形に独自の属性（メタデータ）を追加する場合、`<object>` タグで mxCell をラップする：

```xml
<object label="DBサーバー" zone="3" type="database" id="db1">
  <mxCell style="shape=cylinder3;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
    <mxGeometry x="100" y="100" width="60" height="80" as="geometry" />
  </mxCell>
</object>
```

**用途:**
- ドメインモデルに追加情報（英語名、説明など）を付与
- 外部ツールとの連携用メタデータ
- 検索・フィルタリング用のタグ付け

**読み込み時の抽出:**
- `<object>` タグの属性からカスタムプロパティを取得
- `label` 属性は表示ラベル、その他は任意のメタデータ

## 接続ポイントのカスタマイズ

図形の接続ポイント（エッジの接続先）をカスタマイズ：

```xml
style="...;points=[[0,0.5],[1,0.5],[0.5,0],[0.5,1]];"
```

**座標の意味:**
- `[0,0]` = 左上、`[1,0]` = 右上
- `[0,1]` = 左下、`[1,1]` = 右下
- `[0.5,0.5]` = 中央

**例:**
- `points=[[0,0.5],[1,0.5]]` - 左右中央のみ
- `points=[[0.5,0],[0.5,1]]` - 上下中央のみ

## カラーパレット

| 用途                     | fillColor | strokeColor | 例                       |
|--------------------------|-----------|-------------|--------------------------|
| 青（デフォルト）         | #dae8fc   | #6c8ebf     | ドメイン層、主要要素     |
| 緑（成功/インフラ）     | #d5e8d4   | #82b366     | インフラ層、完了状態     |
| 黄（警告/ユースケース） | #fff2cc   | #d6b656     | ユースケース層、注意     |
| オレンジ（強調）         | #ffe6cc   | #d79b00     | ハイライト               |
| 紫（プレゼンテーション） | #e1d5e7   | #9673a6     | プレゼンテーション層     |
| 赤（エラー）             | #f8cecc   | #b85450     | エラー、危険             |
| グレー（中立）           | #f5f5f5   | #666666     | 背景、コンテナ           |

## スタイル属性リファレンス

| 属性            | 値                  | 説明                             |
|-----------------|---------------------|----------------------------------|
| `rounded`       | 0/1                 | 角丸                             |
| `whiteSpace`    | wrap                | テキスト折り返し                 |
| `html`          | 1                   | HTML有効化                       |
| `fillColor`     | #RRGGBB             | 塗りつぶし色                     |
| `strokeColor`   | #RRGGBB             | 線の色                           |
| `fontStyle`     | 0/1/2/3             | 0=標準, 1=太字, 2=斜体, 3=両方  |
| `fontSize`      | 数値                | フォントサイズ                   |
| `fontColor`     | #RRGGBB             | フォント色                       |
| `align`         | left/center/right   | 横揃え                           |
| `verticalAlign` | top/middle/bottom   | 縦揃え                           |
| `dashed`        | 1                   | 点線                             |
| `opacity`       | 0-100               | 透明度                           |

## エッジスタイル

| 属性         | 値                         | 説明         |
|--------------|----------------------------|--------------|
| `edgeStyle`  | orthogonalEdgeStyle        | 直角エッジ   |
| `edgeStyle`  | entityRelationEdgeStyle    | ER図用       |
| `curved`     | 1                          | 曲線         |
| `startArrow` | none/classic/block/oval/diamond | 始点矢印 |
| `endArrow`   | none/classic/block/oval/diamond | 終点矢印 |

### コンポジション（◆）の向き

**◆は親側（全体・包含する側）に置く**

```text
親（全体）◆────── 子（部品）

例: Order ◆────── OrderItem
    （OrderがOrderItemを包含）
```

**スタイル指定:**
```xml
<!-- source側が親の場合: startArrow に◆を指定 -->
startArrow=diamondThin;startFill=1;endArrow=none;

<!-- target側が親の場合: endArrow に◆を指定 -->
endArrow=diamondThin;endFill=1;startArrow=none;
```

- `diamondThin` = 白抜きひし形（集約）
- `startFill=1` / `endFill=1` = 塗りつぶし（コンポジション）
