---
name: snow-d3
description: 'D3.js data visualization skill. Use when creating charts, graphs, maps, or any data-driven SVG/Canvas visualizations with D3.js. Covers bar charts, line charts, pie charts, scatter plots, area charts, histograms, force-directed graphs, tree layouts, treemaps, choropleth maps, transitions, zoom, brush, and all 30 D3 modules. Also covers heatmaps, radial/polar charts, Sankey diagrams, box plots, violin plots, waterfall charts, Gantt timelines, parallel coordinates, radar/spider charts, bump/ranking charts, sunburst partitions, Voronoi diagrams, density contours, candlestick OHLC charts, lollipop/dot plots, correlation matrices, and ridgeline/joy plots. Triggers: d3, d3.js, data visualization, chart, graph, svg visualization, interactive chart, force graph, geo map, treemap, sunburst, chord diagram, sankey, heatmap, gantt, candlestick, radar, voronoi, ridgeline, waterfall, parallel coordinates, d3-selection, d3-scale, d3-shape, d3-force, d3-hierarchy, d3-geo.'
argument-hint: 'Describe the chart type or visualization you want to build (e.g. "bar chart", "force graph", "choropleth map")'
---

# D3.js Data Visualization Skill (snow-d3)

D3 (Data-Driven Documents) v7 — the JavaScript library for bespoke data visualization using web standards (SVG, Canvas, HTML).

## When to Use

- Creating any **chart or graph**: bar, line, area, scatter, pie, donut, histogram, box plot
- Building **hierarchical visualizations**: treemap, sunburst, tree, dendrogram, circle packing
- Rendering **network graphs**: force-directed layouts, chord diagrams
- Making **geographic maps**: choropleth, bubble map, globe projections
- Adding **interactivity**: zoom/pan, brush selection, drag-and-drop, tooltips
- Implementing **animated transitions** between data states
- Customizing every pixel of a visualization with full SVG/Canvas control

## Skill Resources

| Resource | Description |
|----------|-------------|
| [API Overview](./references/api-overview.md) | Complete D3 module API quick reference |
| [Module Guide](./references/modules.md) | Deep-dive on each of the 30 D3 modules |
| [Patterns & Recipes](./references/patterns.md) | Common patterns, margin convention, responsive charts |
| [Examples Index](./examples/) | Ready-to-run standalone HTML examples |

## Examples Bundled in this Skill

| File | Chart Type | Key Concepts |
|------|-----------|--------------|
| [01-bar-chart.html](./examples/01-bar-chart.html) | Vertical & horizontal bar chart | `scaleBand`, `scaleLinear`, axes, data join |
| [02-line-chart.html](./examples/02-line-chart.html) | Multi-series line chart | `scaleTime`, `line()`, `curveMonotoneX`, tooltip |
| [03-area-chart.html](./examples/03-area-chart.html) | Stacked area chart | `area()`, `stack()`, `scaleOrdinal`, legend |
| [04-scatter-plot.html](./examples/04-scatter-plot.html) | Interactive scatter plot | `scaleLinear`, `symbol()`, brush selection |
| [05-pie-donut-chart.html](./examples/05-pie-donut-chart.html) | Pie & donut chart | `pie()`, `arc()`, `schemeTableau10`, animation |
| [06-histogram.html](./examples/06-histogram.html) | Histogram with density curve | `bin()`, `scaleLinear`, `area()`, normal distribution |
| [07-force-graph.html](./examples/07-force-graph.html) | Force-directed network graph | `forceSimulation`, `forceLink`, `forceManyBody` |
| [08-tree-layout.html](./examples/08-tree-layout.html) | Collapsible tree diagram | `d3.tree()`, `d3.hierarchy()`, click interaction |
| [09-treemap.html](./examples/09-treemap.html) | Zoomable treemap | `d3.treemap()`, `treemapSquarify`, zoom transition |
| [10-choropleth-map.html](./examples/10-choropleth-map.html) | Choropleth world map | `geoNaturalEarth1`, `geoPath`, `scaleSequential` |
| [11-bubble-chart.html](./examples/11-bubble-chart.html) | Bubble / circle packing | `d3.pack()`, `scaleSqrt`, tooltip, zoom |
| [12-transitions.html](./examples/12-transitions.html) | Animated bar chart update | `selection.transition()`, `easeElastic`, data join |
| [13-brush-zoom.html](./examples/13-brush-zoom.html) | Brush & zoom on time series | `d3.brush()`, `d3.zoom()`, context + focus chart |
| [14-chord-diagram.html](./examples/14-chord-diagram.html) | Chord diagram | `d3.chord()`, `d3.ribbon()`, arc paths |
| [15-heatmap.html](./examples/15-heatmap.html) | Calendar heatmap | `scaleSequential`, `d3-time`, `interpolateGreens`, GitHub-style grid |
| [16-radial-bar.html](./examples/16-radial-bar.html) | Radial / polar bar | `scaleRadial`, `arc()`, coxcomb & nightingale modes |
| [17-sankey.html](./examples/17-sankey.html) | Sankey / alluvial flow | `d3-sankey` (CDN), `sankeyLinkHorizontal()`, node/link tooltips |
| [18-box-plot.html](./examples/18-box-plot.html) | Box plot + violin | `d3.bin()`, `d3.area()` KDE violin, quartile stats, jitter |
| [19-waterfall.html](./examples/19-waterfall.html) | Waterfall / bridge | Running cumulative totals, positive/negative bars, connector lines |
| [20-gantt.html](./examples/20-gantt.html) | Gantt timeline | `scaleTime`, `scaleBand`, progress bars, today marker |
| [21-parallel-coordinates.html](./examples/21-parallel-coordinates.html) | Parallel coordinates | Per-axis `scaleLinear`, `brushY()` filter, polyline rendering |
| [22-radar-chart.html](./examples/22-radar-chart.html) | Radar / spider chart | Radial projection, `curveLinearClosed`, multi-series overlay |
| [23-bump-chart.html](./examples/23-bump-chart.html) | Bump / ranking chart | `scalePoint`, `curveBumpX`, rank badges, hover highlight |
| [24-sunburst.html](./examples/24-sunburst.html) | Sunburst partition | `d3.partition()`, `d3.hierarchy()`, click-to-zoom arc tween |
| [25-voronoi.html](./examples/25-voronoi.html) | Voronoi diagram | `d3.Delaunay.from()`, `.voronoi()`, click to add sites |
| [26-contour.html](./examples/26-contour.html) | Density contour / KDE | `d3.contourDensity()`, `d3.geoPath()`, adjustable bandwidth |
| [27-candlestick.html](./examples/27-candlestick.html) | Candlestick / OHLC | `scaleTime`, `scaleBand`, volume bars, crosshair tooltip |
| [28-lollipop.html](./examples/28-lollipop.html) | Lollipop / dot plot | Sorted stems & dots, animated transitions, comparison mode |
| [29-matrix-chart.html](./examples/29-matrix-chart.html) | Correlation matrix | Pearson correlations, `interpolateRdBu`, hover values |
| [30-ridgeline.html](./examples/30-ridgeline.html) | Ridgeline / joy plot | Stacked KDE, `curveCatmullRom`, adjustable overlap & bandwidth |

## Procedure

### 1. Choose the right chart type
Use the table above or the [Module Guide](./references/modules.md) to identify which D3 modules are needed.

### 2. Set up the HTML skeleton
Every standalone D3 chart starts with this template:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>My Chart</title>
  <style>/* chart styles */</style>
</head>
<body>
<div id="chart"></div>
<script type="module">
import * as d3 from "https://cdn.jsdelivr.net/npm/d3@7/+esm";
// chart code here
</script>
</body>
</html>
```

### 3. Apply the margin convention
```js
const width = 800, height = 500;
const margin = { top: 20, right: 30, bottom: 40, left: 50 };
const innerWidth  = width  - margin.left - margin.right;
const innerHeight = height - margin.top  - margin.bottom;

const svg = d3.select("#chart")
  .append("svg")
    .attr("width", width)
    .attr("height", height)
  .append("g")
    .attr("transform", `translate(${margin.left},${margin.top})`);
```

### 4. Define scales
```js
// Continuous → continuous
const xScale = d3.scaleLinear().domain([0, d3.max(data, d => d.value)]).range([0, innerWidth]);
// Time
const xTime  = d3.scaleUtc().domain(d3.extent(data, d => d.date)).range([0, innerWidth]);
// Ordinal / categorical
const xBand  = d3.scaleBand().domain(data.map(d => d.name)).range([0, innerWidth]).padding(0.1);
// Color
const color  = d3.scaleOrdinal(d3.schemeTableau10);
```

### 5. Draw shapes using data join
```js
svg.selectAll("rect")
  .data(data)
  .join("rect")
    .attr("x", d => xBand(d.name))
    .attr("y", d => yScale(d.value))
    .attr("width", xBand.bandwidth())
    .attr("height", d => innerHeight - yScale(d.value))
    .attr("fill", d => color(d.name));
```

### 6. Add axes
```js
svg.append("g").attr("transform", `translate(0,${innerHeight})`).call(d3.axisBottom(xBand));
svg.append("g").call(d3.axisLeft(yScale).ticks(6).tickFormat(d3.format(",.0f")));
```

### 7. Add interactivity (tooltips, zoom, brush)
See [Patterns & Recipes](./references/patterns.md) and the bundled HTML examples.

## Key Concepts Quick Reference

| Concept | API | Notes |
|---------|-----|-------|
| Data join | `selection.data(data).join(enter, update, exit)` | Core D3 pattern |
| Scales | `d3.scaleLinear`, `scaleBand`, `scaleTime`, `scaleOrdinal` | Map domain→range |
| Shapes | `d3.line()`, `d3.area()`, `d3.arc()`, `d3.pie()` | Generate SVG path `d` strings |
| Axes | `d3.axisBottom(scale)`, `axisLeft`, `axisTop`, `axisRight` | Render tick marks & labels |
| Transitions | `selection.transition().duration(ms).ease(fn)` | Smooth animations |
| Zoom | `d3.zoom().on("zoom", handler)` | Pan & zoom behavior |
| Brush | `d3.brush()` / `d3.brushX()` | Range selection |
| Force | `d3.forceSimulation(nodes).force("link", d3.forceLink(links))` | Network physics |
| Hierarchy | `d3.hierarchy(data)`, `d3.tree()`, `d3.treemap()`, `d3.pack()` | Tree / nested layouts |
| Geo | `d3.geoPath()`, `d3.geoNaturalEarth1()` | Geographic projections |

## External Resources
- **Official docs**: https://d3js.org/
- **API index**: https://d3js.org/api
- **Gallery (Observable)**: https://observablehq.com/@d3/gallery
- **GitHub**: https://github.com/d3/d3
- **CDN**: `https://cdn.jsdelivr.net/npm/d3@7/+esm`
- **npm**: `npm install d3`
