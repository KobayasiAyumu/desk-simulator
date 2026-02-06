# Desk Setup Simulator (Isometric) 🖥️

HTML5 CanvasとJavaScriptのみで構築された、アイソメトリック（等測投影）視点のデスク環境シミュレーターです。
3Dライブラリ（Three.jsなど）を使用せず、独自の座標変換ロジックによって2.5D空間を描画しています。

**👉 [デモサイトはこちら (Demo URL)](https://kobayasiayumu.github.io/desk-simulator/)**

## ✨ 特徴 (Features)

* **Isometric Projection**: 斜め上45度からの視点を数学的な計算で再現。
* **360° Rotation View**: 部屋全体を90度ずつ回転させ、死角にある家具も確認可能。
* **Dynamic Shading**: オブジェクトの色に基づき、上面・側面・影の3色を自動生成して立体感を表現。
* **Z-Sorting**: 「Painter's Algorithm」を実装し、家具の前後関係（重なり）を正しく描画。
* **Ghost Cursor**: 配置予定の家具を半透明でプレビュー表示。

## 🛠 使用技術 (Tech Stack)

フレームワークやゲームエンジンに頼らず、**Vanilla JS (標準のJavaScript)** のみでアルゴリズムを実装しました。

* **HTML5 Canvas API**: 描画エンジン
* **JavaScript (ES6+)**: ロジック実装
    * **Coordinate Transformation**: グリッド座標(Grid) ⇔ 画面座標(Screen) の相互変換
    * **Matrix Logic (View Rotation)**: 視点回転に伴うワールド座標からビュー座標への変換行列ロジック
    * **Procedural Coloring**: ベースカラーから明暗を自動計算するシェーディング処理

## 🕹️ 操作方法 (Controls)

| キー / 操作 | アクション |
|---|---|
| **Mouse Move** | 配置場所の選択（カーソル移動） |
| **Click** | 家具を配置 |
| **R** | 家具を90度回転させる |
| **V** | 視点（部屋全体）を90度回転させる |
| **Q** | 全ての家具を削除する |

## 🚀 技術的なこだわり (Technical Highlights)

### 1. 座標変換システム (Coordinate System)
2次元配列上のデータ（ワールド座標）を、アイソメトリックな画面上のピクセル（スクリーン座標）に変換するために、以下の計算式を実装しています。

```javascript
// グリッドから画面座標への変換
screenX = originX + (gridX - gridY) * (tileWidth / 2);
screenY = originY + (gridX + gridY) * (tileHeight / 2) - (gridZ * tileHeight);
2. 視点回転のロジック (View Rotation)
視点を回転させる際、家具のデータそのものを書き換えるのではなく、**「ワールド座標（絶対位置）」と「ビュー座標（見た目の位置）」**を分離して管理しています。これにより、何度回転させてもデータの整合性が保たれます。

3. 描画順序の制御 (Z-Sort)
手前の物体が奥の物体を隠す表現をするために、描画毎にオブジェクトをソートしています。 depth = x + y の値が小さい順（奥）から大きい順（手前）に描画することで、正しい前後関係を実現しました。

## 👨‍💻 Author

* GitHub: [@AYUMU](https://github.com/KobayasiAyumu)
* Student at Human Academy IT College

---
&copy; 2026 SkyShare Project
