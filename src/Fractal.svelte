<script>
  import P5 from "p5-svelte";

  const WIDTH = 500,
    HEIGHT = 500;

  let p5;

  let line = {
    x1: WIDTH / 2,
    y1: HEIGHT,
    x2: WIDTH / 2,
    y2: HEIGHT / 2,
  };

  let rad = Math.PI / 4;
  let linelength = HEIGHT / 2;

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

  const goLine = (x1, y1, x2, y2, r, l) => {};

  const calculateNewPoint = (x1, y1, radians, plength) => {
    let new_length = plength / 2;
    radians = 2 * Math.PI - radians;
    let x2 = new_length * Math.cos(radians);
    let y2 = new_length * Math.sin(radians);
    return { x: x2 + x1, y: y2 + y1 };
  };
</script>

<P5 {sketch} />
