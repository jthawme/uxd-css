<script>
  let styleString = "";

  let bgColor = "#ff0000";
  let hueRotate = 0;
  let saturate = 1;
  let contrast = 1;
  let brightness = 1;
  let opacity = 1;
  let blendMode = "normal";
  let animate = false;

  let bgImg = "/pic1.jpg";

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

  function onFileChange(e) {
    if (e.target.files.length) {
      const file = e.target.files[0];

      const fr = new FileReader();
      fr.onload = () => {
        bgImg = fr.result;
      };
      fr.readAsDataURL(file);
    }
  }

  $: {
    const cssStr = [];
    const filter = [];

    returnTransform([hueRotate], filter, "deg", "hue-rotate(", ")", 0);
    returnTransform([saturate], filter, "", "saturate(", ")", 1);
    returnTransform([contrast], filter, "", "contrast(", ")", 1);
    returnTransform([brightness], filter, "", "brightness(", ")", 1);

    // returnTransform([scaleX, scaleY], filter, "", "scale(", ")", 1);

    // returnTransform([rotate], filter, "deg", "rotate(", ")", 0);

    if (filter.length) {
      cssStr.push(`filter: ${filter.join(" ")}`);
    }

    if (blendMode !== "normal") {
      cssStr.push(`mix-blend-mode: ${blendMode}`);
    }

    if (opacity !== 1) {
      cssStr.push(`opacity: ${opacity}`);
    }

    styleString = cssStr.join("; \n");
  }
</script>

<style lang="scss">
  section {
    display: flex;
    flex-direction: column;

    scroll-snap-align: start;

    height: 100vh;

    background-color: white;

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

      width: 35vh;
      height: 35vh;

      background-size: cover;
      background-position: center;

      z-index: 5;

      &.original {
        z-index: 1;
        border-radius: 35vh;
        background-image: none;

        display: flex;

        align-items: center;
        justify-content: center;

        font-size: 12px;
        text-align: center;
        font-family: monospace;

        &.animate {
          animation: {
            name: morph;
            duration: 1s;
            direction: alternate;
            iteration-count: infinite;
          }
        }
      }
    }
  }

  @keyframes morph {
    to {
      border-radius: 0;
      transform: scale(0.5);
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

  .row {
    margin-top: 15px;
  }
</style>

<section>

  <div class="output">
    <div class="figure">
      <div
        class="box"
        style={`${styleString}; background-image: url(${bgImg})`} />
      <div
        class="box original"
        class:animate
        style={`background-color: ${bgColor}`}>
        This shape is just to help illustrate the blend mode/filter
      </div>
    </div>
    <textarea readonly on:focus={onFocus}>{styleString}</textarea>
  </div>

  <div class="inputs">
    <h3>Filter Explorer</h3>
    <div class="row">
      <div class="input-labels">
        <label>
          <span>Hue Rotate</span>
          <input type="number" step="5" bind:value={hueRotate} />
        </label>
      </div>
    </div>
    <div class="row">
      <div class="input-labels">
        <label>
          <span>Saturate</span>
          <input type="number" step="0.1" bind:value={saturate} />
        </label>
      </div>
    </div>
    <div class="row">
      <div class="input-labels">
        <label>
          <span>Contrast</span>
          <input type="number" step="0.1" bind:value={contrast} />
        </label>
      </div>
    </div>
    <div class="row">
      <div class="input-labels">
        <label>
          <span>Brightness</span>
          <input type="number" step="0.1" bind:value={brightness} />
        </label>
      </div>
    </div>
    <div class="row">
      <div class="input-labels">
        <label>
          <span>Opacity</span>
          <input
            type="number"
            step="0.1"
            bind:value={opacity}
            max="1"
            min="0" />
        </label>
      </div>
    </div>
    <div class="row">
      <div class="input-labels">
        <label>
          <span>Blend Mode</span>
          <select bind:value={blendMode}>
            <option value="normal">Normal</option>
            <option value="multiply">Multiply</option>
            <option value="darken">Darken</option>
            <option value="lighten">Lighten</option>
            <option value="color-burn">Color Burn</option>
            <option value="difference">Difference</option>
            <option value="exclusion">Exclusion</option>
            <option value="soft-light">Soft Light</option>
            <option value="hard-light">Hard Light</option>
            <option value="color">Color</option>
          </select>
        </label>
      </div>
    </div>
    <div class="row">
      <div class="input-labels">
        <label>
          <span>Change image</span>
          <input type="file" on:change={onFileChange} />
        </label>
      </div>
    </div>
    <div class="row">
      <div class="input-labels">
        <label>
          <span>Background color (only for demonstration)</span>
          <input type="color" bind:value={bgColor} />
        </label>
      </div>
    </div>
    <div class="row">
      <div class="input-labels">
        <label>
          <span>Background animate (only for demonstration)</span>
          <input type="checkbox" bind:checked={animate} />
        </label>
      </div>
    </div>
  </div>
</section>
