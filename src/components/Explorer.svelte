<script>
  import RowTitle from "./RowTitle.svelte";
  import Row from "./Row.svelte";
  import Illustration from "./Illustration.svelte";
  import Upload from "./Upload.svelte";

  function capitalise(str) {
    return `${str.charAt(0).toUpperCase()}${str.substring(1)}`;
  }

  const blendModes = [
    "normal",
    "multiply",
    "screen",
    "overlay",
    "darken",
    "lighten",
    "color-dodge",
    "color-burn",
    "difference",
    "exclusion",
    "hue",
    "saturation",
    "color",
    "luminosity"
  ].map(v => ({
    value: v,
    label: capitalise(v)
  }));

  function transformValue(nums, arr, unit, prefix, suffix, def) {
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

  let translateX = 0;
  let translateY = 0;
  let translateZ = 0;

  let scaleY = 1;
  let scaleX = 1;

  let rotate = 0;

  let hueRotate = 0;
  let contrast = 1;
  let saturate = 1;
  let brightness = 1;

  let opacity = 1;
  let blendMode = "normal";

  let foregroundColor = "#ff0000";
  let foregroundImage = "https://source.unsplash.com/random/800x600";
  let foregroundScaling = "cover";

  let backgroundColor = "#0000ff";
  let backgroundImage = false;
  let backgroundScaling = "cover";
  let backgroundAnimate = false;

  let styleArr = [];
  let foregroundArr = [];
  let backgroundArr = [];

  $: {
    styleArr = [];
    foregroundArr = [];
    backgroundArr = [];

    let transformArr = [];
    transformValue(
      [translateX, translateY, translateZ],
      transformArr,
      "px",
      "translate3d(",
      ")",
      0
    );
    transformValue([scaleX, scaleY], transformArr, "", "scale(", ")", 1);
    transformValue([rotate], transformArr, "deg", "rotate(", ")", 0);

    if (transformArr.length) {
      styleArr.push(`transform: ${transformArr.join(" ")}`);
    }

    let filterArr = [];
    transformValue([hueRotate], filterArr, "deg", "hue-rotate(", ")", 0);
    transformValue([contrast], filterArr, "", "contrast(", ")", 1);
    transformValue([saturate], filterArr, "", "saturate(", ")", 1);
    transformValue([brightness], filterArr, "", "brightness(", ")", 1);

    if (filterArr.length) {
      styleArr.push(`filter: ${filterArr.join(" ")}`);
    }

    if (opacity !== 1) {
      styleArr.push(`opacity: ${opacity}`);
    }

    if (blendMode !== "normal") {
      styleArr.push(`mix-blend-mode: ${blendMode}`);
    }

    foregroundArr.push(`background-color: ${foregroundColor}`);
    foregroundArr.push(`background-size: ${foregroundScaling}`);

    if (foregroundImage) {
      foregroundArr.push(`background-image: url(${foregroundImage})`);
    }

    backgroundArr.push(`background-color: ${backgroundColor}`);
    backgroundArr.push(`background-size: ${backgroundScaling}`);

    if (backgroundImage) {
      backgroundArr.push(`background-image: url(${backgroundImage})`);
    }
  }
</script>

<style lang="scss">
  section {
    display: flex;

    align-items: flex-start;
    border-top: 1px solid var(--color-dark-grey);

    .input-list,
    .output {
      flex-basis: 50%;
    }

    .input-list {
      border: 1px solid var(--color-dark-grey);
      border-top: 0;
    }

    .output {
      position: sticky;

      display: flex;

      align-items: center;
      justify-content: center;

      top: 0;

      min-height: 100vh;
    }
  }

  input,
  select {
    width: 100%;

    border: none;

    background-color: transparent;
    border-radius: 0;

    outline: none;
  }
</style>

<section>
  <div class="input-list">
    <RowTitle>
      <span slot="title">Property</span>
      <span slot="subtitle">Sub-Property</span>
      <span slot="value">Value</span>
    </RowTitle>
    <Row>
      <span slot="title">Transform</span>
      <span slot="subtitle">Translate</span>
      <span slot="suffix">X</span>
      <span slot="value">
        <input type="number" bind:value={translateX} />
      </span>
    </Row>
    <Row>
      <span slot="subtitle" />
      <span slot="suffix">Y</span>
      <span slot="value">
        <input type="number" bind:value={translateY} />
      </span>
    </Row>
    <Row>
      <span slot="title">Transform</span>
      <span slot="subtitle">Scale</span>
      <span slot="suffix">X</span>
      <span slot="value">
        <input type="number" step="0.1" bind:value={scaleX} />
      </span>
    </Row>
    <Row>
      <span slot="subtitle" />
      <span slot="suffix">Y</span>
      <span slot="value">
        <input type="number" step="0.1" bind:value={scaleY} />
      </span>
    </Row>
    <Row>
      <span slot="title">Transform</span>
      <span slot="subtitle">Rotate</span>
      <span slot="value">
        <input type="number" bind:value={rotate} />
      </span>
    </Row>
    <Row>
      <span slot="title">Filter</span>
      <span slot="subtitle">Hue Rotate</span>
      <span slot="value">
        <input type="number" step="5" bind:value={hueRotate} />
      </span>
    </Row>
    <Row>
      <span slot="title">Filter</span>
      <span slot="subtitle">Contrast</span>
      <span slot="value">
        <input type="number" step="0.1" bind:value={contrast} />
      </span>
    </Row>
    <Row>
      <span slot="title">Filter</span>
      <span slot="subtitle">Saturate</span>
      <span slot="value">
        <input type="number" step="0.1" bind:value={saturate} />
      </span>
    </Row>
    <Row>
      <span slot="title">Filter</span>
      <span slot="subtitle">Brightness</span>
      <span slot="value">
        <input type="number" step="0.1" bind:value={brightness} />
      </span>
    </Row>
    <Row>
      <span slot="title">Opacity</span>
      <span slot="value">
        <input type="number" step="0.1" bind:value={opacity} />
      </span>
    </Row>
    <Row>
      <span slot="title">Blend Mode</span>
      <span slot="value">
        <select bind:value={blendMode}>
          {#each blendModes as blend}
            <option value={blend.value}>{blend.label}</option>
          {/each}
        </select>
      </span>
    </Row>
    <RowTitle>
      <span slot="title">Demonstration Settings</span>
    </RowTitle>
    <Row>
      <span slot="title">Foreground</span>
      <span slot="subtitle">Colour</span>
      <span slot="value">
        <input type="color" bind:value={foregroundColor} />
      </span>
    </Row>
    <Row>
      <span slot="subtitle">Image</span>
      <span slot="value">
        <Upload onUpload={data => (foregroundImage = data)} />
      </span>
    </Row>
    <Row>
      <span slot="subtitle">Scaling</span>
      <span slot="value">
        <select bind:value={foregroundScaling}>
          <option value="cover">Cover</option>
          <option value="contain">Contain</option>
        </select>
      </span>
    </Row>
    <Row>
      <span slot="title">Background</span>
      <span slot="subtitle">Colour</span>
      <span slot="value">
        <input type="color" bind:value={backgroundColor} />
      </span>
    </Row>
    <Row>
      <span slot="subtitle">Image</span>
      <span slot="value">
        <Upload onUpload={data => (backgroundImage = data)} />
      </span>
    </Row>
    <Row>
      <span slot="subtitle">Scaling</span>
      <span slot="value">
        <select bind:value={backgroundScaling}>
          <option value="cover">Cover</option>
          <option value="contain">Contain</option>
        </select>
      </span>
    </Row>
    <Row>
      <span slot="subtitle">Animated</span>
      <span slot="value">
        <input type="checkbox" bind:checked={backgroundAnimate} />
      </span>
    </Row>
  </div>
  <div class="output">
    <Illustration
      styleString={styleArr.join('; ')}
      foregroundString={foregroundArr.join('; ')}
      backgroundString={backgroundArr.join('; ')}
      animate={backgroundAnimate} />
  </div>
</section>
