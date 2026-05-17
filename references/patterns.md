# D3.js Patterns & Recipes

## The Margin Convention

The standard D3 margin convention creates an inner coordinate space:

```js
const width = 800, height = 500;
const margin = { top: 20, right: 30, bottom: 40, left: 60 };
const innerWidth  = width  - margin.left - margin.right;
const innerHeight = height - margin.top  - margin.bottom;

const svg = d3.select("#chart")
  .append("svg")
    .attr("width", width)
    .attr("height", height)
    .attr("viewBox", `0 0 ${width} ${height}`)
    .style("max-width", "100%")
    .style("height", "auto");     // responsive

const g = svg.append("g")
  .attr("transform", `translate(${margin.left},${margin.top})`);
// All chart elements go inside g, using 0..innerWidth, 0..innerHeight
```

---

## Responsive Charts

Use `viewBox` and `preserveAspectRatio`:

```js
const svg = d3.select("#chart").append("svg")
  .attr("viewBox", `0 0 ${width} ${height}`)
  .attr("preserveAspectRatio", "xMidYMid meet")
  .style("width", "100%")
  .style("height", "auto");
```

For dynamic resize with ResizeObserver:
```js
const observer = new ResizeObserver(([entry]) => {
  const w = entry.contentRect.width;
  const h = w * (height / width);     // maintain aspect ratio
  svg.attr("width", w).attr("height", h);
  xScale.range([0, w - margin.left - margin.right]);
  yScale.range([h - margin.top - margin.bottom, 0]);
  update();
});
observer.observe(document.getElementById("chart"));
```

---

## Data Join Pattern (Enter/Update/Exit)

### Modern join() approach (D3 v5+)
```js
const bars = g.selectAll(".bar")
  .data(data, d => d.id)            // key function for identity
  .join(
    enter => enter.append("rect")
      .attr("class", "bar")
      .attr("fill", "steelblue")
      .attr("y", innerHeight)        // start at bottom for animation
      .attr("height", 0),
    update => update,
    exit => exit
      .transition().duration(300)
      .attr("height", 0).attr("y", innerHeight)
      .remove()
  )
  .transition().duration(500)
    .attr("x",      d => xScale(d.name))
    .attr("width",  xScale.bandwidth())
    .attr("y",      d => yScale(d.value))
    .attr("height", d => innerHeight - yScale(d.value));
```

### Classic pattern
```js
const selection = g.selectAll("circle").data(data, d => d.id);
const enter = selection.enter().append("circle").attr("r", 0);
const update = selection;
const exit = selection.exit().transition().attr("r", 0).remove();
enter.merge(update).transition().attr("r", d => rScale(d.size));
```

---

## Tooltip Pattern

```html
<style>
.tooltip {
  position: absolute;
  background: rgba(0,0,0,.8);
  color: white;
  padding: 6px 10px;
  border-radius: 4px;
  font-size: 12px;
  pointer-events: none;
  opacity: 0;
  transition: opacity 0.15s;
}
</style>
```

```js
const tooltip = d3.select("body").append("div").attr("class", "tooltip");

selection
  .on("mouseover", (event, d) => {
    tooltip
      .html(`<strong>${d.name}</strong><br/>Value: ${d3.format(",.0f")(d.value)}`)
      .style("opacity", 1);
  })
  .on("mousemove", (event) => {
    tooltip
      .style("left",  (event.pageX + 12) + "px")
      .style("top",   (event.pageY - 28) + "px");
  })
  .on("mouseout", () => {
    tooltip.style("opacity", 0);
  });
```

---

## Axis Styling

```js
// Remove the domain line
g.call(axis).call(g => g.select(".domain").remove());

// Dashed grid lines
g.call(
  d3.axisLeft(yScale)
    .tickSize(-innerWidth)          // extend ticks across chart
    .tickFormat("")                 // no labels on grid
).call(g => {
  g.select(".domain").remove();
  g.selectAll(".tick line")
    .attr("stroke-opacity", 0.15)
    .attr("stroke-dasharray", "3,3");
});

// Rotated x-axis labels
g.call(d3.axisBottom(xScale))
  .selectAll("text")
    .attr("transform", "rotate(-45)")
    .attr("text-anchor", "end")
    .attr("dx", "-0.5em")
    .attr("dy", "0.15em");
```

---

## Legend

### Categorical legend
```js
const legend = svg.append("g")
  .attr("transform", `translate(${width - margin.right - 120}, ${margin.top})`);

const legendItems = legend.selectAll(".legend-item")
  .data(color.domain())
  .join("g")
    .attr("class", "legend-item")
    .attr("transform", (d, i) => `translate(0, ${i * 20})`);

legendItems.append("rect")
  .attr("width", 14).attr("height", 14)
  .attr("fill", d => color(d));

legendItems.append("text")
  .attr("x", 18).attr("y", 11)
  .style("font-size", "12px")
  .text(d => d);
```

### Color scale legend (continuous)
```js
const defs = svg.append("defs");
const linearGradient = defs.append("linearGradient").attr("id", "colorGrad");
linearGradient.selectAll("stop")
  .data(d3.ticks(0, 1, 10))
  .join("stop")
    .attr("offset", d => `${d * 100}%`)
    .attr("stop-color", d => colorScale(d));

svg.append("rect")
  .attr("x", x).attr("y", y)
  .attr("width", 200).attr("height", 12)
  .style("fill", "url(#colorGrad)");
```

---

## Loading and Parsing Data

```js
// CSV with auto-type inference
const data = await d3.csv("data.csv", d3.autoType);

// CSV with manual type coercion
const data = await d3.csv("data.csv", d => ({
  date:  new Date(d.date),
  value: +d.value,                  // coerce to number
  name:  d.name
}));

// JSON (already parsed)
const data = await d3.json("data.json");

// Multiple concurrent fetches
const [csv1, json1] = await Promise.all([
  d3.csv("data.csv", d3.autoType),
  d3.json("meta.json")
]);

// Inline data (no fetch)
const data = [
  { name: "Alpha", value: 30 },
  { name: "Beta",  value: 80 },
];
```

---

## Common Chart Patterns

### Grouped Bar Chart
```js
const groups   = [...new Set(data.map(d => d.group))];
const subgroups = [...new Set(data.map(d => d.category))];

const xScale = d3.scaleBand().domain(groups).range([0, innerWidth]).padding(0.1);
const x1     = d3.scaleBand().domain(subgroups).range([0, xScale.bandwidth()]).padding(0.05);
const yScale = d3.scaleLinear().domain([0, d3.max(data, d => d.value)]).range([innerHeight, 0]).nice();

const grouped = d3.group(data, d => d.group);

g.selectAll(".group-bar")
  .data(grouped)
  .join("g")
    .attr("transform", ([key]) => `translate(${xScale(key)},0)`)
  .selectAll("rect")
  .data(([, values]) => values)
  .join("rect")
    .attr("x",      d => x1(d.category))
    .attr("width",  x1.bandwidth())
    .attr("y",      d => yScale(d.value))
    .attr("height", d => innerHeight - yScale(d.value))
    .attr("fill",   d => color(d.category));
```

### Zoom + Axis Rescale
```js
const zoom = d3.zoom()
  .scaleExtent([1, 20])
  .extent([[0, 0], [innerWidth, innerHeight]])
  .translateExtent([[0, 0], [innerWidth, innerHeight]])
  .on("zoom", (event) => {
    const newX = event.transform.rescaleX(xScale);
    xAxisG.call(d3.axisBottom(newX));
    dots.attr("cx", d => newX(d.x));
  });

svg.call(zoom);
```

### Focus + Context (Overview + Detail)
```js
// Context (small overview at the bottom)
const contextBrush = d3.brushX()
  .extent([[0, 0], [innerWidth, contextHeight]])
  .on("brush end", (event) => {
    const [x0, x1] = event.selection ? event.selection.map(xContext.invert) : xContext.domain();
    xFocus.domain([x0, x1]);
    focusLine.attr("d", lineFocus);
    xAxisFocusG.call(d3.axisBottom(xFocus));
  });
```

### Voronoi Hover (nearest point tooltip)
```js
const delaunay = d3.Delaunay.from(data, d => xScale(d.x), d => yScale(d.y));

svg.on("mousemove", (event) => {
  const [mx, my] = d3.pointer(event, g.node());
  const idx = delaunay.find(mx, my);
  const d = data[idx];
  // show tooltip for d
});
```

---

## Performance Tips

1. **Avoid innerHTML / DOM string building** — use D3 selections, which are faster.
2. **Use `selection.join()` not enter/update/exit manually** for cleaner code.
3. **Canvas for >10,000 elements** — SVG slows down. Use `d3-path` with Canvas context.
4. **requestAnimationFrame for real-time** — use `d3.timer()` for animation loops.
5. **Key functions in data join** — always provide a key `d => d.id` to prevent mis-mapping.
6. **Memoize scale ticks** — don't call `.ticks()` in render loops.
7. **Debounce resize** — delay resizing scale recalculations.
8. **Use `d3.rollup` / `d3.group`** for data aggregation — it's O(n).

---

## Dark Mode Support

```js
const isDark = window.matchMedia("(prefers-color-scheme: dark)").matches;

const textColor  = isDark ? "#e5e5e5" : "#333";
const gridColor  = isDark ? "rgba(255,255,255,0.1)" : "rgba(0,0,0,0.1)";
const bgColor    = isDark ? "#1a1a2e" : "white";

svg.style("background", bgColor);
g.selectAll("text").style("fill", textColor);
```

---

## Canvas Rendering (High-Performance)

```js
const canvas = d3.select("#chart").append("canvas")
  .attr("width", width).attr("height", height);
const ctx = canvas.node().getContext("2d");

function render() {
  ctx.clearRect(0, 0, width, height);
  data.forEach(d => {
    ctx.beginPath();
    ctx.arc(xScale(d.x), yScale(d.y), rScale(d.r), 0, 2 * Math.PI);
    ctx.fillStyle = color(d.group);
    ctx.fill();
  });
}
```

For custom shapes, use `d3.path()`:
```js
const path = d3.path();
// issue Canvas commands
path.arc(x, y, r, 0, 2 * Math.PI);
// either render to SVG:
pathEl.attr("d", path.toString());
// or to Canvas:
ctx.stroke(new Path2D(path.toString()));
```

---

## Common Pitfalls

| Pitfall | Fix |
|---------|-----|
| `NaN` in axis / scale | Check data types — strings don't auto-coerce. Use `+d.value` |
| Transition conflicts | Use named transitions `selection.transition("name")` |
| Missing data gaps in line | Use `.defined(d => !isNaN(d.y))` on line generator |
| Overlapping labels | Rotate with `transform="rotate(-45)"` or use `d3.forceSimulation` |
| SVG blur on zoom | Use `shape-rendering: crispEdges` for rectangles |
| Chart not visible | Forgot `margin.left` offset — check the `g` group transform |
| Tooltip behind chart | Set `z-index` on tooltip, use `position: absolute` |
| Slow with big data | Switch to Canvas; reduce DOM nodes with aggregation |
