# D3.js Module Guide

## The 30 D3 Modules

D3 v7 is organized into 30 independent packages. They group naturally into six categories:

---

## Category 1: DOM & Selection

### d3-selection
**Purpose**: Core DOM manipulation via data-driven selections.

Key concepts:
- **Selection** — a set of DOM nodes
- **Data join** — bind data array to DOM elements
- **Enter/Update/Exit** pattern — handle new, changed, and removed data

Critical methods:
| Method | Description |
|--------|-------------|
| `d3.select(selector)` | Select first matching element |
| `d3.selectAll(selector)` | Select all matching elements |
| `selection.data(data[, key])` | Bind data array |
| `selection.join(enter, update, exit)` | Handle all three phases |
| `selection.attr(name, value)` | Set/get DOM attribute |
| `selection.style(name, value)` | Set/get CSS style |
| `selection.classed(names, bool)` | Toggle CSS classes |
| `selection.text(value)` | Set text content |
| `selection.append(type)` | Append child element |
| `selection.remove()` | Remove elements |
| `selection.on(type, listener)` | Add event listener |
| `selection.call(function)` | Call a function on the selection |
| `selection.each(function)` | Call function per element |
| `d3.create(name)` | Create a detached element |
| `d3.pointer(event[, node])` | Get event coordinates |

### d3-transition
**Purpose**: Smooth animated transitions between DOM states.

Key concepts:
- Transitions are selections with timing
- Multiple simultaneous transitions use named transitions
- Chain transitions with `.transition()` after a transition

```js
selection
  .transition("my-transition")
  .delay(d => d.index * 20)
  .duration(600)
  .ease(d3.easeCubicInOut)
  .attr("x", d => newX(d))
  .on("end", callback);
```

Easing functions (all have `In`, `Out`, `InOut` variants):
- `easeLinear` — no easing
- `easeQuad` / `easeCubic` — polynomial
- `easeSin` — sinusoidal
- `easeExp` — exponential
- `easeCircle` — circular
- `easeElastic` — rubber band (extra params: amplitude, period)
- `easeBack` — overshoot (extra param: overshoot)
- `easeBounce` — bouncing ball

---

## Category 2: Scales & Color

### d3-scale
**Purpose**: Map abstract data to visual properties (position, size, color).

Scale families:

| Family | Scales | Use Case |
|--------|--------|----------|
| Continuous | `scaleLinear`, `scalePow`, `scaleSqrt`, `scaleLog`, `scaleSymlog` | Numeric → numeric |
| Time | `scaleTime`, `scaleUtc` | Date → position |
| Sequential | `scaleSequential` (+ log/pow/sqrt variants) | Numeric → color interpolator |
| Diverging | `scaleDiverging` (+ log/pow/sqrt variants) | Diverging data → color |
| Quantize | `scaleQuantize` | Continuous → discrete buckets |
| Quantile | `scaleQuantile` | Data distribution → buckets |
| Threshold | `scaleThreshold` | Custom thresholds → buckets |
| Ordinal | `scaleOrdinal` | Categorical → categorical |
| Band | `scaleBand` | Ordered categories → intervals |
| Point | `scalePoint` | Ordered categories → points |

All continuous scales share:
- `.domain([min, max])` — input domain
- `.range([a, b])` — output range
- `.invert(value)` — reverse mapping
- `.ticks(count)` — representative values
- `.tickFormat(count, format)` — formatter
- `.nice()` — extend to nice round numbers
- `.clamp(bool)` — clamp output to range
- `.copy()` — create independent copy

### d3-scale-chromatic
**Purpose**: Curated color palettes for D3 scales.

Categorical (fixed arrays):
```js
d3.schemeTableau10    // 10 colors, perceptually distinct
d3.schemeObservable10 // Observable's modern palette
d3.schemeCategory10   // classic D3 colors
d3.schemePaired       // 12 colors in 6 pairs
d3.schemeDark2        // 8 dark colors
d3.schemeSet1/2/3     // ColorBrewer categorical
```

Sequential (continuous interpolators, `t ∈ [0,1]`):
```js
d3.interpolateViridis     d3.interpolatePlasma
d3.interpolateInferno     d3.interpolateMagma
d3.interpolateCividis     d3.interpolateTurbo
d3.interpolateBlues       d3.interpolateYlOrRd
```

Diverging (pivot at `t = 0.5`):
```js
d3.interpolateRdBu   d3.interpolateSpectral
d3.interpolatePiYG   d3.interpolateBrBG
```

### d3-color
**Purpose**: Color space parsing, conversion, and manipulation.

Color spaces supported: RGB, HSL, Lab (CIE L*a*b*), HCL, Cubehelix.
```js
const c = d3.color("hsl(207, 44%, 49%)");
c.brighter(1.0)     // lighter version
c.darker(0.5)       // darker version
c.opacity = 0.5;
c.formatHex()       // "#4682b4"
c.formatRgb()       // "rgb(70,130,180)"
```

### d3-interpolate
**Purpose**: Interpolate between two values of any type.

```js
d3.interpolateNumber(a, b)(t)       // numeric lerp
d3.interpolateString(a, b)(t)       // interpolate embedded numbers in strings
d3.interpolateRgb(a, b)(t)          // RGB color
d3.interpolateHsl(a, b)(t)          // HSL color (shorter arc)
d3.interpolateLab(a, b)(t)          // perceptually uniform
d3.interpolateCubehelix(a, b)(t)    // Cubehelix (vivid)
d3.interpolateArray(a, b)(t)        // element-wise array
d3.interpolateObject(a, b)(t)       // property-wise object
d3.interpolateZoom(a, b)(t)         // semantic zoom transition
```

---

## Category 3: Shapes & Layouts

### d3-shape
**Purpose**: Generate SVG path data strings for common chart shapes.

Key generators:
- **`d3.line()`** — line chart paths (takes array of points)
- **`d3.area()`** — filled area between two lines
- **`d3.arc()`** — pie/donut slices
- **`d3.pie()`** — convert values to arc angle descriptors
- **`d3.stack()`** — stack multiple data series
- **`d3.symbol()`** — point symbols (circle, square, diamond, etc.)
- **`d3.link()` / `d3.linkHorizontal()` / `d3.linkVertical()`** — smooth Bézier connectors

### d3-hierarchy
**Purpose**: Layout algorithms for tree-structured data.

Layouts:
| Layout | Function | Output Geometry |
|--------|----------|----------------|
| Tree (tidy tree) | `d3.tree()` | `node.x`, `node.y` coordinates |
| Cluster (dendrogram) | `d3.cluster()` | Leaf nodes aligned |
| Treemap | `d3.treemap()` | `node.x0`, `y0`, `x1`, `y1` rectangles |
| Partition (sunburst) | `d3.partition()` | `x0`, `y0`, `x1`, `y1` in radial coords |
| Pack (bubble) | `d3.pack()` | `node.x`, `node.y`, `node.r` circles |

Common workflow:
```js
const root = d3.hierarchy(rawData)
  .sum(d => d.value)            // aggregate values upward
  .sort((a, b) => b.value - a.value);

d3.treemap()
  .size([width, height])
  .padding(2)
  .paddingTop(18)               // space for label
  (root);
```

### d3-chord
**Purpose**: Chord diagrams for flow/relationship matrices.

```js
const chords = d3.chord()
  .padAngle(0.04)
  .sortSubgroups(d3.descending)
  (matrix);                     // n×n flow matrix

// Groups (outer arcs)
svg.selectAll(".group")
  .data(chords.groups)
  .join("path")
    .attr("d", d3.arc().innerRadius(innerR).outerRadius(outerR));

// Ribbons (inner curves)
svg.selectAll(".ribbon")
  .data(chords)
  .join("path")
    .attr("d", d3.ribbon().radius(innerR));
```

---

## Category 4: Geography

### d3-geo
**Purpose**: Geographic projections, path generation, and spherical math.

Available projections:
- **Azimuthal**: `geoAzimuthalEqualArea`, `geoAzimuthalEquidistant`, `geoGnomonic`, `geoOrthographic`, `geoStereographic`
- **Conic**: `geoConicConformal`, `geoConicEqualArea` (Albers), `geoConicEquidistant`, `geoAlbers`, `geoAlbersUsa`
- **Cylindrical**: `geoEquirectangular`, `geoMercator`, `geoTransverseMercator`, `geoEqualEarth`, `geoNaturalEarth1`

Working with GeoJSON:
```js
// Fit projection to GeoJSON object
const projection = d3.geoNaturalEarth1()
  .fitSize([width, height], geojsonObject);

// Path generator
const path = d3.geoPath().projection(projection);

// Render features
svg.selectAll("path").data(features).join("path").attr("d", path);

// Compute centroid for labels
const [cx, cy] = path.centroid(feature);

// Graticule
const graticule = d3.geoGraticule();
svg.append("path").datum(graticule()).attr("d", path).attr("stroke", "#ccc").attr("fill","none");
```

---

## Category 5: Interactions & Physics

### d3-force
**Purpose**: Velocity Verlet integration for force-directed layouts.

Available forces:
| Force | Description |
|-------|-------------|
| `forceCenter(x, y)` | Pull nodes toward a center point |
| `forceManyBody()` | N-body (attraction or repulsion) |
| `forceLink(links)` | Spring forces between linked nodes |
| `forceCollide(radius)` | Prevent node overlap |
| `forceX(x)` / `forceY(y)` | Push nodes toward x/y coordinate |
| `forceRadial(r, x, y)` | Push nodes to a circle |

Simulation lifecycle:
```js
const sim = d3.forceSimulation(nodes)
  .alphaDecay(0.02)               // cooling rate
  .velocityDecay(0.4)             // friction
  .on("tick", ticked)             // each frame
  .on("end",  () => console.log("stable"));

// Reheat on data update
sim.alpha(0.3).restart();
// Stop completely
sim.stop();
// Single tick
sim.tick();
```

### d3-zoom
**Purpose**: Pan and zoom SVG, HTML, or Canvas using mouse/touch.

```js
const zoom = d3.zoom()
  .scaleExtent([0.5, 32])
  .on("zoom", ({ transform }) => {
    zoomLayer.attr("transform", transform);
  });

// Programmatic zoom
svg.call(zoom.translateTo, 100, 200);      // pan to point
svg.call(zoom.scaleTo, 2);                 // zoom to scale
svg.call(zoom.transform, d3.zoomIdentity); // reset
```

### d3-brush
**Purpose**: Click-and-drag region selection.

```js
// 2D brush
const brush = d3.brush()
  .extent([[0, 0], [width, height]])
  .on("start brush end", handler);

// 1D brushes
d3.brushX()   // horizontal extent only
d3.brushY()   // vertical extent only

// In handler
function handler({ selection }) {
  if (!selection) return;           // cleared
  const [[x0,y0],[x1,y1]] = selection;
  // filter: data.filter(d => x0<=xS(d.x)&&xS(d.x)<=x1)
}
```

### d3-drag
**Purpose**: Mouse/touch drag interaction.

```js
const drag = d3.drag()
  .subject(d => d)                  // what is being dragged
  .on("start", (e, d) => { ... })
  .on("drag",  (e, d) => {
    d3.select(this).attr("cx", d.x = e.x).attr("cy", d.y = e.y);
  })
  .on("end",   (e, d) => { ... });

nodes.call(drag);
```

### d3-dispatch
**Purpose**: Custom event dispatcher for loosely coupled components.

```js
const dispatch = d3.dispatch("highlight", "select");
dispatch.on("highlight", function(d) { ... });
dispatch.call("highlight", this, datum);
```

---

## Category 6: Computation & Utility

### d3-array
See API Overview. Key utilities for analysis:
- `d3.bin()` — histogram binning
- `d3.group()` / `d3.rollup()` — grouping and aggregation
- `d3.cross()` — Cartesian product
- `d3.zip()` — transpose array of arrays
- `d3.cumsum()` — cumulative sum
- `d3.fsum()` — precise floating point sum
- `d3.least()` / `d3.greatest()` — argmin/argmax
- `d3.rank()` — rank order
- `d3.quantile()` — percentiles
- `d3.InternMap` — Map with value equality

### d3-contour
**Purpose**: Compute contour polygons (isocontours) from scalar fields.

```js
// From a grid of values
const contours = d3.contours()
  .size([cols, rows])
  .thresholds(d3.range(0, 1, 0.1))
  (values);

// Kernel density estimate from points
const density = d3.contourDensity()
  .x(d => xScale(d.x))
  .y(d => yScale(d.y))
  .size([width, height])
  .bandwidth(20);
```

### d3-delaunay
**Purpose**: Fast Delaunay triangulation and Voronoi tessellation.

```js
const delaunay = d3.Delaunay.from(points, d => d.x, d => d.y);
delaunay.find(mx, my);              // nearest point to mouse
const voronoi = delaunay.voronoi([xmin, ymin, xmax, ymax]);
```

### d3-random
**Purpose**: Generate random numbers from statistical distributions.
```js
d3.randomUniform(min, max)()
d3.randomNormal(μ, σ)()
d3.randomLogNormal(μ, σ)()
d3.randomPoisson(λ)()
d3.randomBeta(α, β)()
d3.randomWeibull(k, λ, θ)()
```

### d3-path
**Purpose**: Serialize Canvas 2D path commands to SVG path strings.

### d3-polygon
**Purpose**: Geometric operations on 2D polygons.
```js
d3.polygonArea(polygon)
d3.polygonCentroid(polygon)
d3.polygonHull(points)              // convex hull
d3.polygonContains(polygon, point)
```

### d3-quadtree
**Purpose**: 2D spatial index using recursive subdivision.
```js
const qt = d3.quadtree().x(d => d.x).y(d => d.y).addAll(data);
qt.find(x, y, radius)               // nearest neighbor
```

### d3-timer
**Purpose**: High-precision timer queue for animations.
```js
d3.timer(callback, delay, time)     // repeating timer
d3.timeout(callback, delay)         // single-shot timer
d3.interval(callback, period)       // periodic timer
d3.now()                            // current high-res time
```
