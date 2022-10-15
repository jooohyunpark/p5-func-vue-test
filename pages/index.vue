<template>
  <div class="p5-page">
    <div class="container">
      <div class="row">
        <h4>p5 boilerplate</h4>
        <p>This is an p5.js starter page. Check the code.</p>
        <div id="p5-canvas" class="col" ref="canvas"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  mounted() {
    const sketch = (p5) => {
      /* polyfill p5 */
      for (const [key, value] of Object.entries(p5.__proto__)) {
        window[key] = value;
      }

      var e = new P5.Ease(); // easing function object

      // assign 'foo' to a 10-point Array filled with
      // a "doubleQuadraticBezie" easing function:
      var foo = e.fillArray("doubleQuadraticBezier", 10);

      // assign 'bar' to a 100-point Float32Array filled with
      // a "smoothStep" easing function:
      var bar = e.fillFloat32Array("smoothStep", 100);

      // assign a 1000-point "doubleCircularSigmoid" with
      // a coefficient of 0.8 to the Float64Array 'biz':
      var biz = e.fillFloat64Array("doubleCircularSigmoid", 1000, 0.8);

      console.log(foo); // print
      fplot(foo, "color: red; font-size:9px;"); // plot
      console.log(bar); // print
      fplot(bar, "color: green; font-size:9px;"); // plot
      console.log(biz); // print
      fplot(biz, "color: blue; font-size:9px;"); // plot

      var a = new P5.ArrayEval(); // array evaluation object

      // 10-point 'normal map' (0 to 1):
      var foo = a.eval("u", 10);

      // 20x20 two-dimensional signed normal map (-1 to 1):
      var bar = a.eval2d(["su", "sv"], 20, 20);

      // 8x8x8 array with a volumetric distance function:
      var biz = a.eval3d("sqrt(su*su+sv*sv+sw*sw)", 8, 8, 8);

      console.log(foo); // print
      console.log(bar); // print
      console.log(biz); // print

      p5.setup = () => {
        const { width, height } = this.$refs.canvas.getBoundingClientRect();
        const canvas = p5.createCanvas(width, height);
        canvas.parent("p5-canvas");

        // Your setup code here
        p5.colorMode(p5.HSB);
      };

      p5.draw = () => {
        // Your draw code here
      };
    };

    // NOTE: Use p5 as an instance mode
    const P5 = require("p5");

    // import p5.func.js
    require("../scripts/p5.func");

    new P5(sketch);
  },
};
</script>

<style scoped lang="scss">
.p5-page {
  margin: 80px 0;

  #p5-canvas {
    width: 100%;
    height: 500px;
  }
}
</style>
