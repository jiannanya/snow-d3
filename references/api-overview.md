# D3.js API Overview (v7)

D3 is a suite of **30 discrete modules**. Import the full bundle or individual modules:

```js
import * as d3 from "https://cdn.jsdelivr.net/npm/d3@7/+esm";           // full bundle
import { scaleLinear } from "https://cdn.jsdelivr.net/npm/d3-scale@4/+esm"; // single module
```

---

## Data Manipulation

### d3-array
Array manipulation, statistics, grouping, binning, searching.
```js
d3.min(arr, d => d.value)           // minimum
d3.max(arr, d => d.value)           // maximum
d3.extent(arr, d => d.value)        // [min, max]
d3.mean(arr, d => d.value)          // arithmetic mean
d3.median(arr, d => d.value)        // median
d3.sum(arr, d => d.value)           // sum
d3.deviation(arr, d => d.value)     // std deviation
d3.group(arr, d => d.category)      // group into Map
d3.rollup(arr, v => v.length, d => d.type) // aggregate Map
d3.index(arr, d => d.id)            // index by key
d3.bin().value(d => d.x)(arr)       // histogram bins
d3.range(0, 100, 10)                // [0,10,20,...,90]
d3.ticks(0, 100, 10)                // nice tick values
d3.sort(arr, d => d.value)          // sort copy
d3.shuffle(arr)                     // Fisher-Yates shuffle
d3.bisect(sorted, x)                // binary search
d3.cross(a, b)                      // Cartesian product
d3.zip(a, b)                        // zip arrays
d3.cumsum(arr, d => d.value)        // cumulative sum
```

### d3-dsv
Parse and format CSV/TSV.
```js
d3.csvParse(string)
d3.tsvParse(string)
d3.csvFormat(rows)
d3.autoType                         // row converter for numeric/date auto-detection
```

### d3-fetch
Load remote data (returns Promises).
```js
d3.csv("data.csv", d3.autoType)     // fetch + parse CSV
d3.json("data.json")                // fetch JSON
d3.tsv("data.tsv")                  // fetch TSV
d3.text("file.txt")                 // fetch plain text
d3.svg("icon.svg")                  // fetch SVG document
d3.xml("data.xml")                  // fetch XML document
```

### d3-format
Format numbers for display.
```js
d3.format(".2f")(3.14159)           // "3.14"
d3.format(",d")(1234567)            // "1,234,567"
d3.format(".0%")(0.753)             // "75%"
d3.format("$.2f")(9.5)              // "$9.50"
d3.format(".2s")(1e6)               // "1.0M"
d3.format("+.1f")(-3.5)             // "-3.5"
```

### d3-time & d3-time-format
Time intervals and formatting.
```js
d3.timeDay.floor(date)
d3.timeMonth.range(start, end)
d3.timeParse("%Y-%m-%d")("2024-01-15")
d3.timeFormat("%b %d, %Y")(date)    // "Jan 15, 2024"
d3.isoFormat(date)                  // ISO 8601 string
```

---

## Scales

### Continuous Scales — d3-scale
```js
// Linear
const scale = d3.scaleLinear()
  .domain([0, 100]).range([0, 500]).clamp(true).nice();

// Log
d3.scaleLog().domain([1, 1000]).range([0, 500]).base(10);

// Power / Sqrt
d3.scalePow().exponent(2)
d3.scaleSqrt()                      // exponent = 0.5

// Time
d3.scaleTime().domain([new Date(2020,0,1), new Date(2024,0,1)]).range([0, 800]);
d3.scaleUtc()                       // UTC version

// Sequential (continuous → interpolator)
d3.scaleSequential(d3.interpolateViridis).domain([0, 100]);

// Diverging
d3.scaleDiverging(d3.interpolateRdBu).domain([-1, 0, 1]);
```

### Discrete / Ordinal Scales
```js
// Band (for bar charts)
d3.scaleBand()
  .domain(categories)
  .range([0, width])
  .padding(0.1)         // inner + outer combined
  .paddingInner(0.05)
  .paddingOuter(0.1);

// Point (for dot plots)
d3.scalePoint().domain(categories).range([0, width]).padding(0.5);

// Ordinal (discrete → discrete)
d3.scaleOrdinal(d3.schemeTableau10).domain(categories);

// Quantize (continuous domain → discrete range)
d3.scaleQuantize().domain([0, 1]).range(["low","mid","high"]);

// Threshold
d3.scaleThreshold().domain([0.33, 0.66]).range(["red","yellow","green"]);
```

---

## Colors — d3-color & d3-scale-chromatic

### Color Parsing & Manipulation
```js
d3.color("steelblue")               // parse
d3.rgb(70, 130, 180)                // RGB
d3.hsl(207, 0.44, 0.49)             // HSL
d3.lab(51, -5, -35)                 // Lab
const c = d3.color("red");
c.brighter(1);   c.darker(0.5);
c.formatHex();   c.formatRgb();
```

### Color Schemes (d3-scale-chromatic)
```js
// Categorical
d3.schemeTableau10        // 10 colors (recommended)
d3.schemeCategory10       // original 10 colors
d3.schemeObservable10     // Observable's 10 colors
d3.schemePaired           // 12 paired colors
d3.schemeDark2            // 8 dark colors
d3.schemeSet3             // 12 colors

// Sequential interpolators
d3.interpolateViridis     d3.interpolatePlasma
d3.interpolateInferno     d3.interpolateMagma
d3.interpolateCividis     d3.interpolateTurbo
d3.interpolateBlues       d3.interpolateGreens

// Diverging interpolators
d3.interpolateRdBu        d3.interpolateSpectral
d3.interpolatePiYG        d3.interpolateBrBG
```

---

## Shapes — d3-shape

### Line
```js
const line = d3.line()
  .x(d => xScale(d.date))
  .y(d => yScale(d.value))
  .defined(d => !isNaN(d.value))    // skip null values
  .curve(d3.curveMonotoneX);        // smooth line

svg.append("path").datum(data).attr("d", line);
```

### Area
```js
const area = d3.area()
  .x(d => xScale(d.date))
  .y0(innerHeight)                  // baseline
  .y1(d => yScale(d.value))         // topline
  .curve(d3.curveLinear);
```

### Arc (Pie / Donut)
```js
const arc = d3.arc()
  .innerRadius(0)                   // 0 = pie, >0 = donut
  .outerRadius(radius)
  .cornerRadius(4)
  .padAngle(0.02);

const pie = d3.pie().value(d => d.value).sort(null);
const arcs = pie(data);             // returns array of arc descriptors
```

### Curve Types
```js
d3.curveLinear           // straight lines
d3.curveMonotoneX        // smooth, preserves monotonicity in x
d3.curveBasis            // B-spline
d3.curveCardinal         // cardinal spline (.tension(0.5))
d3.curveCatmullRom       // Catmull-Rom
d3.curveStep             // step function
d3.curveNatural          // natural cubic spline
```

### Stack
```js
const stack = d3.stack()
  .keys(["apples", "bananas", "oranges"])
  .order(d3.stackOrderNone)
  .offset(d3.stackOffsetNone);      // d3.stackOffsetExpand for 100%

const series = stack(data);         // array of [y0, y1] layers
```

---

## Axes — d3-axis
```js
const xAxis = d3.axisBottom(xScale)
  .ticks(10)                        // approximate tick count
  .tickSize(6)
  .tickPadding(3)
  .tickFormat(d3.format(",.0f"));

const yAxis = d3.axisLeft(yScale)
  .tickValues([0, 25, 50, 75, 100]) // explicit ticks
  .tickFormat(d => `${d}%`);

svg.append("g")
  .attr("class", "x-axis")
  .attr("transform", `translate(0,${innerHeight})`)
  .call(xAxis)
  .call(g => g.select(".domain").remove()); // remove axis line
```

---

## Selections & Data Join — d3-selection
```js
// Select
d3.select("#chart")                  // CSS selector
d3.selectAll("circle")
selection.select("rect")             // first descendant per element
selection.selectAll("text")          // all descendants per element

// Modify
selection
  .attr("cx", d => xScale(d.x))     // attribute
  .style("fill", "steelblue")        // style
  .classed("active", true)           // add class
  .text(d => d.label)               // text content
  .html(d => `<b>${d.name}</b>`)    // inner HTML
  .property("checked", true);        // DOM property

// Create / remove
selection.append("g")
selection.insert("circle", ":first-child")
selection.remove()

// Data join
selection.data(data)
  .join(
    enter  => enter.append("rect").attr("fill", "steelblue"),
    update => update.attr("fill", "orange"),
    exit   => exit.remove()
  );

// Events
selection.on("mouseover", (event, d) => { ... })
selection.on("click",     (event, d) => { ... })
d3.pointer(event)                   // [x, y] relative to container
```

---

## Transitions — d3-transition
```js
selection
  .transition()
  .duration(750)
  .delay((d, i) => i * 50)         // stagger by index
  .ease(d3.easeElasticOut)
  .attr("y", d => yScale(d.value))
  .attr("height", d => innerHeight - yScale(d.value));

// Named transition (coordinate updates)
d3.transition("update").duration(500);

// Ease functions
d3.easeLinear   d3.easeQuad    d3.easeCubic
d3.easeSin      d3.easeExp     d3.easeCircle
d3.easeElastic  d3.easeBack    d3.easeBounce
// Each has In / Out / InOut variants: d3.easeQuadIn, d3.easeQuadOut, d3.easeQuadInOut
```

---

## Interactions

### Zoom — d3-zoom
```js
const zoom = d3.zoom()
  .scaleExtent([1, 40])
  .translateExtent([[0, 0], [width, height]])
  .on("zoom", (event) => {
    g.attr("transform", event.transform);
    // Rescale axes:
    const newX = event.transform.rescaleX(xScale);
    xAxisG.call(xAxis.scale(newX));
  });

svg.call(zoom);
svg.call(zoom.transform, d3.zoomIdentity); // reset
```

### Brush — d3-brush
```js
const brush = d3.brushX()
  .extent([[0, 0], [innerWidth, innerHeight]])
  .on("brush end", (event) => {
    const [x0, x1] = event.selection.map(xScale.invert);
    // filter data to [x0, x1]
  });

svg.append("g").attr("class", "brush").call(brush);
```

### Drag — d3-drag
```js
const drag = d3.drag()
  .on("start", (event, d) => { d.dragging = true; })
  .on("drag",  (event, d) => { d.x = event.x; d.y = event.y; redraw(); })
  .on("end",   (event, d) => { d.dragging = false; });

circles.call(drag);
```

---

## Hierarchical Layouts — d3-hierarchy
```js
const root = d3.hierarchy(nestedData)
  .sum(d => d.value)
  .sort((a, b) => b.value - a.value);

// Tree
const treeLayout = d3.tree().size([width, height]);
treeLayout(root);
// root.descendants() → all nodes with .x, .y
// root.links()       → all edges { source, target }

// Treemap
d3.treemap().size([width, height]).padding(2)(root);
// Each node: .x0, .y0, .x1, .y1

// Circle packing
d3.pack().size([width, height]).padding(3)(root);
// Each node: .x, .y, .r

// Partition (sunburst / icicle)
d3.partition().size([2 * Math.PI, radius])(root);
```

---

## Force Simulation — d3-force
```js
const simulation = d3.forceSimulation(nodes)
  .force("link",    d3.forceLink(links).id(d => d.id).distance(60))
  .force("charge",  d3.forceManyBody().strength(-300))
  .force("center",  d3.forceCenter(width / 2, height / 2))
  .force("collide", d3.forceCollide().radius(d => d.r + 2))
  .force("x",       d3.forceX(width / 2).strength(0.05))
  .force("y",       d3.forceY(height / 2).strength(0.05))
  .on("tick", ticked);             // update DOM each tick

function ticked() {
  link.attr("x1", d => d.source.x).attr("y1", d => d.source.y)
      .attr("x2", d => d.target.x).attr("y2", d => d.target.y);
  node.attr("cx", d => d.x).attr("cy", d => d.y);
}
```

---

## Geographic — d3-geo
```js
const projection = d3.geoNaturalEarth1()     // or geoMercator, geoOrthographic…
  .scale(150)
  .translate([width / 2, height / 2])
  .fitSize([width, height], geoJson);

const path = d3.geoPath().projection(projection);

svg.selectAll("path")
  .data(features)
  .join("path")
    .attr("d", path)
    .attr("fill", d => colorScale(d.properties.value));

// Graticule (lat/lon grid)
svg.append("path")
  .datum(d3.geoGraticule()())
  .attr("d", path)
  .attr("stroke", "#ccc").attr("fill", "none");
```

---

## Miscellaneous Utilities

### d3-interpolate
```js
d3.interpolateNumber(0, 100)(0.5)   // 50
d3.interpolateRgb("red", "blue")(0.5)
d3.interpolateArray([0,1], [10,20])(0.5)
d3.interpolateObject({x:0}, {x:100})(0.5)
```

### d3-random
```js
d3.randomNormal(mean, stddev)()
d3.randomUniform(0, 1)()
d3.randomInt(0, 100)()
d3.randomPoisson(lambda)()
```

### d3-path
```js
const context = d3.path();
context.moveTo(0, 0);
context.lineTo(100, 100);
context.arc(50, 50, 30, 0, Math.PI);
context.toString();                 // SVG path string
```

### d3-chord
```js
const chord = d3.chord().padAngle(0.05).sortSubgroups(d3.descending);
const chords = chord(matrix);       // compute layout

const ribbon = d3.ribbon().radius(innerRadius);
svg.selectAll("path").data(chords).join("path").attr("d", ribbon);
```

### d3-contour
```js
// Density estimation
const density = d3.contourDensity()
  .x(d => xScale(d.x)).y(d => yScale(d.y))
  .size([width, height]).bandwidth(30);

svg.selectAll("path")
  .data(density(data))
  .join("path")
    .attr("d", d3.geoPath())
    .attr("fill", d => colorScale(d.value));
```

### d3-delaunay / Voronoi
```js
const delaunay = d3.Delaunay.from(data, d => d.x, d => d.y);
const voronoi  = delaunay.voronoi([0, 0, width, height]);
svg.selectAll("path").data(data).join("path")
  .attr("d", (d, i) => voronoi.renderCell(i));
```
