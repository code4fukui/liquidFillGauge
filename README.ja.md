# liquidFillGauge

D3.js用のカスタマイズ可能な液体充填ゲージ可視化ライブラリです。このプロジェクトは、Curtis Bratton氏が作成したオリジナルの[D3 Liquid Fill Gauge](http://bl.ocks.org/brattonc/5e5ce9beee483220e2f6)をD3 v4以降に対応させたアップデート版です。

## デモ

[**ライブデモ**](https://code4fukui.github.io/liquidFillGauge/)

デモページでは、さまざまな設定・スタイル・動的更新を適用した複数のゲージを確認できます。

![異なるスタイルと色を持つ複数の液体充填ゲージのデモ](https://user-images.githubusercontent.com/593536/154857031-6a4352ea-315a-437c-a548-a23053a55b37.gif)

## 機能

- **高カスタマイズ性:** 色、太さ、テキストサイズ、配置を制御可能。
- **波のアニメーション:** 波の高さ、数、アニメーション速度を設定可能。
- **動的更新:** ゲージ描画後に値の変化をスムーズにアニメーション表示。
- **柔軟な値表示:** パーセンテージまたは生の数値を表示可能。ロード時に「カウントアップ」アニメーションもオプションで利用可能。
- **高度な波の制御:** 波の上昇アニメーションや低/高パーセンテージ時の高さスケーリングを有効/無効にできる。
- **ESモジュール対応:** 現代的なJavaScriptプロジェクトで簡単にインポート・利用可能。

## 使い方

### 1. SVG要素の追加

HTMLに一意のIDを持つ`<svg>`要素を作成し、そこにゲージをレンダリングします。

```html
<svg id="my-gauge" width="150" height="150"></svg>
```

### 2. インポートと初期化

モジュールをインポートし、`liquidFillGauge.load()`を使用してゲージを作成します。`liquidFillGauge.default()`からデフォルト設定オブジェクトを取得し、カスタマイズできます。

```javascript
import liquidFillGauge from "https://code4fukui.github.io/liquidFillGauge/liquidFillGauge.js";

// デフォルト設定を取得
const config = liquidFillGauge.default();

// 設定をカスタマイズ
config.circleColor = "#FF7777";
config.textColor = "#FF4444";
config.waveTextColor = "#FFAAAA";
config.waveColor = "#FFDDDD";
config.waveAnimateTime = 1000; // 1秒

// ゲージをロード
const myGauge = liquidFillGauge.load("my-gauge", 55, config);

// 後で値を更新する場合:
// myGauge.update(80);
```

## API

### `liquidFillGauge.load(elementId, value, [config])`

指定されたSVG要素内にゲージをレンダリングします。

- `elementId` (String): ターゲット`<svg>`要素の`id`。
- `value` (Number): 表示する初期値。
- `config` (Object, optional): デフォルト設定を上書きする設定オブジェクト。
- **戻り値:** `update`メソッドを持つゲージインスタンス。

### `gauge.update(newValue)`

スムーズなアニメーションでゲージの値を新しい値に更新します。

- `newValue` (Number): 表示する新しい値。

```javascript
// 'myGauge'がload()関数から返されたものと仮定
setInterval(() => {
    const newValue = Math.random() * 100;
    myGauge.update(newValue);
}, 2000);
```

## 設定オプション

すべての設定オプションはオプションです。

| オプション | 型 | デフォルト | 説明 |
| :--- | :--- | :--- | :--- |
| `minValue` | `Number` | `0` | ゲージの最小値。 |
| `maxValue` | `Number` | `100` | ゲージの最大値。 |
| `circleThickness` | `Number` | `0.05` | 外側の円の太さ（その半径に対するパーセンテージ）。 |
| `circleFillGap` | `Number` | `0.05` | 外側の円と波の円の間の隙間（外側の円の半径に対するパーセンテージ）。 |
| `circleColor` | `String` | `'#178BCA'` | 外側の円の色。 |
| `waveHeight` | `Number` | `0.05` | 波の高さ（波の円の半径に対するパーセンテージ）。 |
| `waveCount` | `Number` | `1` | 波の円の幅に対する完全な波の数。 |
| `waveRiseTime` | `Number` | `1000` | 波が0から最終的な高さまで上昇する時間（ミリ秒単位）。 |
| `waveAnimateTime` | `Number` | `18000` | 1つの波がゲージを横切ってスクロールするのにかかる時間（ミリ秒単位）。 |
| `waveRise` | `Boolean` | `true` | `true`の場合、ロード時に波が0から最大の高さまで上昇します。 |
| `waveHeightScaling` | `Boolean` | `true` | `true`の場合、波の高さは充填率50%で最大になり、0%および100%で最小になります。 |
| `waveAnimate` | `Boolean` | `true` | `true`の場合、波が水平にスクロールします。 |
| `waveColor` | `String` | `'#178BCA'` | 充填される波の色。 |
| `waveOffset` | `Number` | `0` |
