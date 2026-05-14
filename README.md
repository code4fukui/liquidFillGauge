# liquidFillGauge

> 日本語のREADMEはこちらです: [README.ja.md](README.ja.md)

A customizable liquid fill gauge visualization for D3.js. This project is an update of the original [D3 Liquid Fill Gauge by Curtis Bratton](http://bl.ocks.org/brattonc/5e5ce9beee483220e2f6) to support D3 v4 and later.

## Demo

[**Live Demo**](https://code4fukui.github.io/liquidFillGauge/)

The demo page showcases multiple gauges with different configurations, styles, and dynamic updates.


![Demo of multiple liquid fill gauges with different styles and colors](https://user-images.githubusercontent.com/593536/154857031-6a4352ea-315a-437c-a548-a23053a55b37.gif)


## Features

-   **Highly Customizable:** Control colors, thickness, text size, and positioning.
-   **Animated Waves:** Configure wave height, count, and animation speed.
-   **Dynamic Updates:** Smoothly animate value changes after the gauge is rendered.
-   **Flexible Value Display:** Show values as percentages or raw numbers, with optional "count up" animation on load.
-   **Advanced Wave Control:** Enable or disable wave rise animation and height scaling at low/high percentages.
-   **ES Module Support:** Easily import and use in modern JavaScript projects.

## Usage

### 1. Add the SVG Element

Create an `<svg>` element in your HTML with a unique ID where the gauge will be rendered.

```html
<svg id="my-gauge" width="150" height="150"></svg>
```

### 2. Import and Initialize

Import the module and use `liquidFillGauge.load()` to create the gauge. You can get a default configuration object from `liquidFillGauge.default()` and customize it.

```javascript
import liquidFillGauge from "https://code4fukui.github.io/liquidFillGauge/liquidFillGauge.js";

// Get the default configuration
const config = liquidFillGauge.default();

// Customize the settings
config.circleColor = "#FF7777";
config.textColor = "#FF4444";
config.waveTextColor = "#FFAAAA";
config.waveColor = "#FFDDDD";
config.waveAnimateTime = 1000; // 1 second

// Load the gauge
const myGauge = liquidFillGauge.load("my-gauge", 55, config);

// To update the value later:
// myGauge.update(80);
```

## API

### `liquidFillGauge.load(elementId, value, [config])`

Renders the gauge inside the specified SVG element.

-   `elementId` (String): The `id` of the target `<svg>` element.
-   `value` (Number): The initial value to display.
-   `config` (Object, optional): A configuration object to override default settings.
-   **Returns:** A gauge instance with an `update` method.

### `gauge.update(newValue)`

Updates the gauge to a new value with a smooth animation.

-   `newValue` (Number): The new value to display.

```javascript
// Assuming 'myGauge' was returned from the load() function
setInterval(() => {
    const newValue = Math.random() * 100;
    myGauge.update(newValue);
}, 2000);
```

## Configuration Options

All configuration options are optional.

| Option | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `minValue` | `Number` | `0` | The minimum value of the gauge. |
| `maxValue` | `Number` | `100` | The maximum value of the gauge. |
| `circleThickness` | `Number` | `0.05` | The outer circle thickness as a percentage of its radius. |
| `circleFillGap` | `Number` | `0.05` | The gap between the outer circle and wave circle as a percentage of the outer circle's radius. |
| `circleColor` | `String` | `'#178BCA'` | The color of the outer circle. |
| `waveHeight` | `Number` | `0.05` | The wave height as a percentage of the radius of the wave circle. |
| `waveCount` | `Number` | `1` | The number of full waves per width of the wave circle. |
| `waveRiseTime` | `Number` | `1000` | The time in milliseconds for the wave to rise from 0 to its final height. |
| `waveAnimateTime` | `Number` | `18000` | The time in milliseconds for a full wave to scroll across the gauge. |
| `waveRise` | `Boolean` | `true` | If `true`, the wave rises from 0 to its full height on load. |
| `waveHeightScaling` | `Boolean` | `true` | If `true`, wave height is at its maximum at 50% fill and minimum at 0% and 100%. |
| `waveAnimate` | `Boolean` | `true` | If `true`, the wave scrolls horizontally. |
| `waveColor` | `String` | `'#178BCA'` | The color of the fill wave. |
| `waveOffset` | `Number` | `0` |