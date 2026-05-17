# snow-d3 — D3.js Visualization Skill for Agent

A comprehensive Agent skill that gives Agent deep, expert-level knowledge of [D3.js v7](https://d3js.org/), covering all major modules, patterns, and idioms for building production-quality data visualizations.

---

## Overview

`snow-d3` is a `./` skill file that is loaded automatically by Agent when you ask it to build charts, graphs, or data visualizations using D3.js. Once in context, Agent gains access to:

- A curated API cheatsheet for all 30 D3 modules
- Deep-dive module documentation covering the full D3 ecosystem
- Proven patterns and recipes for real-world chart building
- 30 fully working, standalone HTML example files

---

## Features

| Feature | Details |
|---|---|
| **D3 version** | v7.9+ (ES module CDN, no build tools required) |
| **Coverage** | All 30 D3 modules across 6 categories |
| **Examples** | 30 standalone HTML files, zero dependencies |
| **Patterns** | Margin convention, responsive charts, data joins, tooltips, zoom, brush |

---

## Skill Structure

```
skills/
    └── snow-d3/
        ├── SKILL.md                  ← Main skill entry point (loaded by Agent)
        ├── references/
        │   ├── api-overview.md       ← Quick API reference for all modules
        │   ├── modules.md            ← Deep-dive module documentation
        │   └── patterns.md          ← Common D3 patterns & recipes
        └── examples/
            ├── 01-bar-chart.html
            ├── 02-line-chart.html
            ├── 03-area-chart.html
            ├── 04-scatter-plot.html
            ├── 05-pie-donut-chart.html
            ├── 06-histogram.html
            ├── 07-force-graph.html
            ├── 08-tree-layout.html
            ├── 09-treemap.html
            ├── 10-choropleth-map.html
            ├── 11-bubble-chart.html
            ├── 12-transitions.html
            ├── 13-brush-zoom.html
            ├── 14-chord-diagram.html
            ├── 15-heatmap.html
            ├── 16-radial-bar.html
            ├── 17-sankey.html
            ├── 18-box-plot.html
            ├── 19-waterfall.html
            ├── 20-gantt.html
            ├── 21-parallel-coordinates.html
            ├── 22-radar-chart.html
            ├── 23-bump-chart.html
            ├── 24-sunburst.html
            ├── 25-voronoi.html
            ├── 26-contour.html
            ├── 27-candlestick.html
            ├── 28-lollipop.html
            ├── 29-matrix-chart.html
            └── 30-ridgeline.html
```

---

## Example Files

Each example is a **fully self-contained, zero-dependency HTML file**. Open any one directly in a browser — no server needed. All examples import D3.js from CDN using ES modules:

```html
<script type="module">
import * as d3 from "https://cdn.jsdelivr.net/npm/d3@7/+esm";
// ...
</script>
```

| # | File | Chart Type | Key D3 Concepts |
|---|------|-----------|-----------------|
| 01 | [01-bar-chart.html](./snow-d3/examples/01-bar-chart.html) | Vertical & Horizontal Bar | `scaleBand`, `scaleLinear`, data join, tooltip, animated sort |
| 02 | [02-line-chart.html](./snow-d3/examples/02-line-chart.html) | Multi-Series Line | `scaleTime`, `line()`, `curveMonotoneX`, Delaunay hover, legend toggle |
| 03 | [03-area-chart.html](./snow-d3/examples/03-area-chart.html) | Stacked Area / Streamgraph | `stack()`, `area()`, `stackOffsetWiggle`, `stackOffsetExpand` |
| 04 | [04-scatter-plot.html](./snow-d3/examples/04-scatter-plot.html) | Scatter Plot | `scaleSqrt`, `brush()`, Delaunay, size encoding |
| 05 | [05-pie-donut-chart.html](./snow-d3/examples/05-pie-donut-chart.html) | Pie & Donut | `pie()`, `arc()`, `arcTween`, explode on click, polyline labels |
| 06 | [06-histogram.html](./snow-d3/examples/06-histogram.html) | Histogram + KDE | `bin()`, Epanechnikov kernel, adjustable bins, distribution picker |
| 07 | [07-force-graph.html](./snow-d3/examples/07-force-graph.html) | Force-Directed Network | `forceSimulation`, `forceLink`, `drag()`, `zoom()`, neighbor highlight |
| 08 | [08-tree-layout.html](./snow-d3/examples/08-tree-layout.html) | Collapsible Tree | `d3.tree()`, `d3.hierarchy()`, click-collapse, horizontal/vertical toggle |
| 09 | [09-treemap.html](./snow-d3/examples/09-treemap.html) | Zoomable Treemap | `d3.treemap()`, `treemapSquarify`, breadcrumb navigation, click-to-zoom |
| 10 | [10-choropleth-map.html](./snow-d3/examples/10-choropleth-map.html) | World Choropleth | `geoNaturalEarth1`, `geoPath`, `scaleSequential`, projection switcher |
| 11 | [11-bubble-chart.html](./snow-d3/examples/11-bubble-chart.html) | Circle Packing | `d3.pack()`, `d3.hierarchy()`, animated zoom, breadcrumb |
| 12 | [12-transitions.html](./snow-d3/examples/12-transitions.html) | Animated Transitions | Enter/update/exit, easing gallery, stagger delays, `d3.interval` |
| 13 | [13-brush-zoom.html](./snow-d3/examples/13-brush-zoom.html) | Focus + Context | `brushX()`, `zoom()`, linked panels, crosshair tooltip |
| 14 | [14-chord-diagram.html](./snow-d3/examples/14-chord-diagram.html) | Chord Diagram | `d3.chord()`, `d3.ribbon()`, `d3.arc()`, hover highlight, pin |
| 15 | [15-heatmap.html](./snow-d3/examples/15-heatmap.html) | Calendar Heatmap | `scaleSequential`, `d3-time` utilities, `interpolateGreens`, GitHub-style grid |
| 16 | [16-radial-bar.html](./snow-d3/examples/16-radial-bar.html) | Radial / Polar Bar | `scaleRadial`, `arc()`, coxcomb vs nightingale mode, `interpolateTurbo` |
| 17 | [17-sankey.html](./snow-d3/examples/17-sankey.html) | Sankey Diagram | `d3-sankey` (CDN), `sankeyLinkHorizontal()`, flow highlight, `schemeTableau10` |
| 18 | [18-box-plot.html](./snow-d3/examples/18-box-plot.html) | Box Plot + Violin | `d3.bin()`, `d3.area()` KDE violin, quartile stats, jitter overlay |
| 19 | [19-waterfall.html](./snow-d3/examples/19-waterfall.html) | Waterfall / Bridge | Running totals, positive/negative coloring, connector lines, subtotals |
| 20 | [20-gantt.html](./snow-d3/examples/20-gantt.html) | Gantt Timeline | `scaleTime`, `scaleBand`, progress fill, today marker, phase grouping |
| 21 | [21-parallel-coordinates.html](./snow-d3/examples/21-parallel-coordinates.html) | Parallel Coordinates | `scaleLinear` per axis, `d3.line()`, `brushY()` filter, category highlight |
| 22 | [22-radar-chart.html](./snow-d3/examples/22-radar-chart.html) | Radar / Spider | `d3.line()` with `curveLinearClosed`, radial projection, legend toggle |
| 23 | [23-bump-chart.html](./snow-d3/examples/23-bump-chart.html) | Bump / Ranking | `scalePoint`, `curveBumpX`, rank badges, hover highlight, left/right labels |
| 24 | [24-sunburst.html](./snow-d3/examples/24-sunburst.html) | Sunburst | `d3.partition()`, `d3.hierarchy()`, click-to-zoom, `interpolateRgb` depth tinting |
| 25 | [25-voronoi.html](./snow-d3/examples/25-voronoi.html) | Voronoi Diagram | `d3.Delaunay.from()`, `.voronoi()`, click to add sites, nearest-neighbor highlight |
| 26 | [26-contour.html](./snow-d3/examples/26-contour.html) | Density Contour | `d3.contourDensity()`, `d3.geoPath()`, adjustable bandwidth & thresholds, color schemes |
| 27 | [27-candlestick.html](./snow-d3/examples/27-candlestick.html) | Candlestick / OHLC | `scaleTime`, `scaleBand`, OHLC rendering, volume bars, crosshair tooltip |
| 28 | [28-lollipop.html](./snow-d3/examples/28-lollipop.html) | Lollipop / Dot Plot | Sorted stems + dots, animated transitions, dual-series comparison mode |
| 29 | [29-matrix-chart.html](./snow-d3/examples/29-matrix-chart.html) | Correlation Matrix | Pearson correlations, `interpolateRdBu`, hover insight, factor-model data |
| 30 | [30-ridgeline.html](./snow-d3/examples/30-ridgeline.html) | Ridgeline / Joy Plot | Stacked KDE, `curveCatmullRom`, adjustable overlap & bandwidth, hover stats |

---

## D3 Module Coverage

| Category | Modules Covered |
|----------|----------------|
| **DOM & Selection** | `d3-selection`, `d3-transition` |
| **Scales & Color** | `d3-scale` (all types), `d3-scale-chromatic`, `d3-color`, `d3-interpolate` |
| **Shapes & Layouts** | `d3-shape` (line, area, arc, pie, stack, curves), `d3-hierarchy` (tree, treemap, pack, partition), `d3-chord` |
| **Geography** | `d3-geo` (projections, path, graticule) |
| **Interactions** | `d3-force`, `d3-zoom`, `d3-brush`, `d3-drag`, `d3-dispatch` |
| **Computation** | `d3-array`, `d3-contour`, `d3-delaunay`, `d3-random`, `d3-path`, `d3-polygon`, `d3-quadtree`, `d3-timer` |
| **I/O & Format** | `d3-dsv`, `d3-fetch`, `d3-format`, `d3-time`, `d3-time-format` |

---

## Reference Documents

### [`references/api-overview.md`](./snow-d3/references/api-overview.md)

A fast-lookup cheatsheet covering the most-used APIs across all 30 D3 modules. Organized by module with the key functions, constructors, and method chains you reach for most often.

### [`references/modules.md`](./snow-d3/references/modules.md)

A deep-dive guide to all 30 D3 modules, organized in 6 categories. For each module: purpose, core API surface, usage patterns, and code examples.

### [`references/patterns.md`](./snow-d3/references/patterns.md)

A recipe book of proven D3 patterns including:
- Margin convention
- Responsive / `viewBox` charts
- Modern data join (`selection.join()`)
- Tooltip (HTML overlay pattern)
- Axis styling
- Color legends (categorical + continuous)
- Data loading patterns (`d3.json`, `d3.csv`)
- Grouped bar chart
- Zoom + axis rescaling
- Focus + context with brush
- Voronoi hover
- Canvas rendering
- Performance tips
- Dark mode
- Common pitfalls

---

## Usage

### As a Agent Skill

1. Place this repository (or copy `./snow-d3/`) into your workspace.
2. When you ask Agent to build a D3 chart or visualization, it will automatically pick up and use the skill.
3. Reference a specific example by name when asking: _"Create a chart like example 07, but for my network data."_

### Opening Examples Directly

All 30 examples open directly in any modern browser. No build step, no server required:

```
# On Windows
start ./snow-d3/examples/01-bar-chart.html

# On macOS
open ./snow-d3/examples/01-bar-chart.html

# On Linux
xdg-open ./snow-d3/examples/01-bar-chart.html
```

### Using the CDN Import in Your Own Code

All examples use D3 v7 via ES module import — copy this snippet into any HTML file:

```html
<script type="module">
import * as d3 from "https://cdn.jsdelivr.net/npm/d3@7/+esm";

// Your chart code here
const svg = d3.select("#chart").append("svg")
  .attr("width", 600).attr("height", 400);
</script>
```

---

## D3.js Quick-Start Pattern

Every chart in this skill follows the standard **margin convention**:

```js
// 1. Dimensions
const width = 700, height = 400;
const margin = { top: 20, right: 20, bottom: 50, left: 55 };
const innerW = width  - margin.left - margin.right;
const innerH = height - margin.top  - margin.bottom;

// 2. SVG
const svg = d3.select("#chart").append("svg")
  .attr("width", width).attr("height", height)
  .attr("viewBox", `0 0 ${width} ${height}`)
  .style("max-width", "100%").style("height", "auto");

const g = svg.append("g")
  .attr("transform", `translate(${margin.left},${margin.top})`);

// 3. Scales
const xScale = d3.scaleBand().domain(data.map(d => d.name))
  .range([0, innerW]).padding(0.2);
const yScale = d3.scaleLinear()
  .domain([0, d3.max(data, d => d.value)]).nice()
  .range([innerH, 0]);

// 4. Axes
g.append("g").attr("transform", `translate(0,${innerH})`).call(d3.axisBottom(xScale));
g.append("g").call(d3.axisLeft(yScale));

// 5. Data join
g.selectAll(".bar")
  .data(data, d => d.name)
  .join("rect")
    .attr("class", "bar")
    .attr("x", d => xScale(d.name))
    .attr("y", d => yScale(d.value))
    .attr("width", xScale.bandwidth())
    .attr("height", d => innerH - yScale(d.value))
    .attr("fill", "#4f86c6");
```

---

## External Resources

| Resource | URL |
|----------|-----|
| D3.js Official Documentation | https://d3js.org/ |
| D3 API Reference | https://github.com/d3/d3/blob/main/API.md |
| Observable Plot (D3 companion) | https://observablehq.com/plot/ |
| Observable D3 Gallery | https://observablehq.com/@d3/gallery |
| D3 in Depth | https://www.d3indepth.com/ |
| CDN (ES module) | https://cdn.jsdelivr.net/npm/d3@7/+esm |

---

## Requirements

- A modern browser with ES module support (Chrome 61+, Firefox 60+, Safari 10.1+, Edge 16+)
- No build tools, no npm install, no server required for the examples
- For the choropleth map example ([10-choropleth-map.html](./snow-d3/examples/10-choropleth-map.html)): an internet connection to fetch world atlas GeoJSON from CDN
- For the Sankey diagram example ([17-sankey.html](./snow-d3/examples/17-sankey.html)): an internet connection to load `d3-sankey@0.12` from CDN

---

## License

MIT — free to use, modify, and distribute.
