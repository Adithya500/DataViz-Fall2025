# Example 2 — D3 Threshold Scale

This example shows 10 adjacent 10×10 squares using:

```js
const color = d3.scaleSequential(d3.interpolateViridis).domain([min, max]);
```

```javascript

<script>
  const n = 10;           // number of squares
  const size = 10;        // square size (px)
  const gap = 2;          // gap between squares (px)

  const min = 0, max = n - 1; // domain
  const color = d3.scaleSequential(d3.interpolateViridis).domain([min, max]);

  const svg = d3.select("#viz")
    .attr("width", n * (size + gap) - gap)
    .attr("height", size);

  svg.selectAll("rect")
    .data(d3.range(n))
    .enter().append("rect")
      .attr("x", (d, i) => i * (size + gap))
      .attr("y", 0)
      .attr("width", size)
      .attr("height", size)
      .attr("fill", d => color(d));
</script>
```

## ScaleSequential
- **Scale:** `scaleSequential(interpolator)` expects a numeric domain; it outputs colors by sampling the interpolator between 0 and 1.
- **Domain:** `[min, max]` maps your data range to the scale:
    - With `min = 0` and `max = 9`, `0 → color(0)`, `9 → color(9)`, and values in between are interpolated.
- **Drawing:** We bind `d3.range(n)` to `<rect>` elements and set `fill` using `color(d)`.

## Customize
- `n` — number of squares.
- `size` — square side length.
- `gap` — spacing between squares.
- `min`, `max` — the scale’s numeric domain (match your data range).
- Try other perceptual interpolators: `d3.interpolateCividis`, `d3.interpolatePlasma`, `d3.interpolateMagma`.

## In practice
Replace `d3.range(n)` with your values and set the domain to `[d3.min(data), d3.max(data)]`:
```js
const data = [3, 7, 2, 9, 4, 5, 1, 6, 8, 0];
const color = d3.scaleSequential(d3.interpolateViridis)
                .domain([d3.min(data), d3.max(data)]);

svg.selectAll("rect")
  .data(data)
  .enter().append("rect")
    .attr("x", (d, i) => i * (size + gap))
    .attr("y", 0)
    .attr("width", size)
    .attr("height", size)
    .attr("fill", d => color(d));
```
