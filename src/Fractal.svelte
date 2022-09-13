<script>
  import P5 from "p5-svelte";

  const WIDTH = 500,
    HEIGHT = 500;

  let p5;
  let radian_slider = 3,
    radian_start = 3,
    length = HEIGHT / 2;

  const sketch = (_p5) => {
    _p5.setup = () => {
      _p5.createCanvas(WIDTH, HEIGHT);
      _p5.background(255, 255, 255);
      _p5.stroke("green");
      _p5.strokeWeight(5);
      p5 = _p5;
    };

    _p5.draw = () => {};
  };

  const goLine = (x1, y1, x2, y2, r, l, angle2diff) => {
    // base case
    if (l < 1) return;
    // draw line
    p5.line(x1, y1, x2, y2);
    const deg_shift = 0.9;
    // // calculate rotated point
    let angle1 = r * deg_shift;
    // let angle2 = angle1 + Math.PI / 2;
    let angle2 = angle1 + angle2diff;
    let rot1 = calculateNewPoint(x2, y2, angle1, l * 0.6);
    let rot2 = calculateNewPoint(x2, y2, angle2, l * 0.6);
    goLine(x2, y2, rot1.x, rot1.y, angle1, l * 0.6, angle2diff);
    goLine(x2, y2, rot2.x, rot2.y, angle2, l * 0.6, angle2diff);

    // p5.ellipse(rot1.x, rot1.y, 5, 5);
    // p5.ellipse(rot2.x, rot2.y, 5, 5);
  };

  const calculateNewPoint = (x1, y1, radians, plength) => {
    radians = 2 * Math.PI - radians;
    let x2 = plength * Math.cos(radians);
    let y2 = plength * Math.sin(radians);
    return { x: x2 + x1, y: y2 + y1 };
  };

  const updateFractal = (rad, rad_start, length) => {
    if (!p5) return;
    p5.background((255, 255, 255));
    goLine(WIDTH / 2, HEIGHT, WIDTH / 2, HEIGHT / 2, radian_start, length, rad);
  };

  $: updateFractal(radian_slider, radian_start, length);
</script>

<P5 {sketch} />
<input
  id="radian"
  type="range"
  bind:value={radian_slider}
  min="0"
  max="20"
  step="0.01"
/>
<label for="radian">Radian</label>

<input
  id="radian_start"
  type="range"
  bind:value={radian_start}
  min="0"
  max="20"
  step="0.01"
/>
<label for="radian_start">Radian Start</label>

<input
  id="length"
  type="range"
  bind:value={length}
  min="0"
  max="500"
  step="1"
/>
<label for="length">Length</label>
