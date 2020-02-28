<script>
  let styleString = "";

  let translateX = 0;
  let translateY = 0;
  let translateZ = 0;
  let translateUnit = "px";

  let scaleX = 1;
  let scaleY = 1;

  let rotate = 0;

  function returnTransform(nums, arr, unit, prefix, suffix, def) {
    if (nums.some(n => n > def || n < def)) {
      arr.push(
        [
          prefix,
          nums.map(n => (n && n !== def ? n + unit : def)).join(", "),
          suffix
        ].join("")
      );
    }
  }

  function onFocus() {
    this.select();
  }

  $: {
    const cssStr = [];
    const transform = [];

    returnTransform(
      [translateX, translateY, translateZ],
      transform,
      translateUnit,
      "translate3d(",
      ")",
      0
    );

    returnTransform([scaleX, scaleY], transform, "", "scale(", ")", 1);

    returnTransform([rotate], transform, "deg", "rotate(", ")", 0);

    if (transform.length) {
      cssStr.push(`transform: ${transform.join(" ")}`);
    }
    styleString = cssStr.join("; ");
  }
</script>

<style lang="scss">
  section {
    display: flex;
    flex-direction: column;

    height: 100vh;

    background-color: white;

    scroll-snap-align: start;

    @media screen and (min-width: 768px) {
      flex-direction: row-reverse;
    }

    .inputs,
    .output {
      position: relative;

      flex-grow: 0;
      flex-shrink: 0;
      flex-basis: 50%;
    }

    .inputs {
      background-color: #e5e5e5;

      padding: 20px;

      overflow: auto;
    }

    .output {
      position: relative;

      display: flex;

      flex-direction: column;
      align-items: stretch;

      .figure {
        position: relative;

        flex-grow: 1;

        display: flex;

        align-items: center;
        justify-content: center;
      }

      textarea {
        display: flex;
        flex-basis: 20vh;

        width: 100%;
        min-height: 50px;

        padding: 10px;

        border: 0;
        background-color: #ffa791;

        text-align: center;

        font-family: sans-serif;
      }
    }

    .box {
      position: absolute;

      width: 40%;
      height: 40%;

      background-color: blue;
      mix-blend-mode: multiply;

      z-index: 5;

      &.original {
        z-index: 1;

        background-color: transparent;
        border: 2px dashed red;
        mix-blend-mode: normal;
      }
    }
  }

  h4 {
    margin: 0;
    padding: 1em 0;
  }

  .input-labels {
    display: flex;

    label {
      flex-grow: 1;

      margin-right: 10px;

      &:last-of-type {
        margin-right: 0;
      }

      span {
        display: block;

        margin-bottom: 5px;
      }
    }

    input,
    select {
      width: 100%;

      background-color: white;
      border: 0;
      border-radius: 0;

      padding: 5px;
    }
  }
</style>

<section>

  <div class="output">
    <div class="figure">
      <div class="box" style={styleString} />
      <div class="box original" />
    </div>
    <textarea readonly on:focus={onFocus}>{styleString}</textarea>
  </div>

  <div class="inputs">
    <h3>Transform Explorer</h3>
    <div class="row">
      <h4>Translate</h4>
      <div class="input-labels">
        <label>
          <span>Translate X</span>
          <input type="number" bind:value={translateX} />
        </label>
        <label>
          <span>Translate Y</span>
          <input type="number" bind:value={translateY} />
        </label>
      </div>
      <h4>Transform Unit</h4>
      <div class="input-labels">
        <label>
          <select bind:value={translateUnit}>
            <option value="px">px</option>
            <option value="%">%</option>
          </select>
        </label>
      </div>
      <h4>Scale</h4>
      <div class="input-labels">
        <label>
          <span>Scale X</span>
          <input type="number" step="0.1" bind:value={scaleX} />
        </label>
        <label>
          <span>Scale Y</span>
          <input type="number" step="0.1" bind:value={scaleY} />
        </label>
      </div>
      <h4>Rotate</h4>
      <div class="input-labels">
        <label>
          <span>Rotate</span>
          <input type="number" bind:value={rotate} />
        </label>
      </div>
    </div>
  </div>
</section>
