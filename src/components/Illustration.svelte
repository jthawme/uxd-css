<script>
  export let styleString;
  export let foregroundString;
  export let backgroundString;
  export let animate;
</script>

<style lang="scss">
  .figure {
    position: relative;

    width: 60%;
  }

  .box {
    width: 100%;
    height: 0;
    padding-bottom: 56.25%;

    background-color: red;
    background-position: center;
    background-repeat: no-repeat;

    &.top {
      position: absolute;

      z-index: 2;
    }
  }

  .animate {
    animation: {
      name: PULSE;
      iteration-count: infinite;
      direction: alternate;
      duration: 1s;
    }
  }

  @keyframes PULSE {
    to {
      border-radius: 100%;
      transform: scale(0.4);
    }
  }
</style>

<div class="figure">
  <div
    class="box top"
    style={`${[styleString, foregroundString].join('; ')}`} />
  <div class="box" class:animate style={`${backgroundString}`} />
</div>
