<script>
  import P5 from "p5-svelte";

  const WIDTH = 500,
    HEIGHT = 500;

  let line = {
    x1: WIDTH / 2,
    y1: HEIGHT,
    x2: WIDTH / 2,
    y2: HEIGHT / 2,
  };

  let rad = Math.PI / 4;
  let linelength = HEIGHT / 2;

  const sketch = (p5) => {
    p5.setup = () => {
      p5.createCanvas(WIDTH, HEIGHT);
      p5.background(255, 255, 255);
      p5.stroke("green");
      p5.strokeWeight(5);
    };

    p5.draw = () => {
      p5.line(line.x1, line.y1, line.x2, line.y2);
      let x1_dist = line.x1 - WIDTH / 2;
      let x2_dist = line.x2 - WIDTH / 2;
      p5.line(line.x1 - 2 * x1_dist, line.y1, line.x2 - 2 * x2_dist, line.y2);
      line.x1 = line.x2;
      line.y1 = line.y2;
      let new_point = calculateNewPoint(line.x1, line.y1, rad, linelength);
      line.x2 = new_point.x;
      line.y2 = new_point.y;
      rad -= Math.PI / 4;
      linelength *= 0.75;
    };
  };

  const calculateNewPoint = (x1, y1, radians, plength) => {
    let new_length = plength / 2;
    radians = 2 * Math.PI - radians;
    let x2 = new_length * Math.cos(radians);
    let y2 = new_length * Math.sin(radians);
    return { x: x2 + x1, y: y2 + y1 };
  };
</script>

<P5 {sketch} />
