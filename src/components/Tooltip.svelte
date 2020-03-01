<script context="module">
  import { writable, get } from "svelte/store";

  export const tooltipDisplay = writable(false);

  const isTouch =
    "ontouchstart" in window ||
    navigator.MaxTouchPoints > 0 ||
    navigator.msMaxTouchPoints > 0;

  export function tooltip(node, txt) {
    if (!txt || isTouch) {
      return;
    }

    node.addEventListener("mouseenter", () => {
      tooltipDisplay.set(txt);
    });
    node.addEventListener("mouseleave", () => {
      if (get(tooltipDisplay) === txt) {
        tooltipDisplay.set(false);
      }
    });
  }
</script>

<script>
  import { onMount } from "svelte";

  let mouseX = 0;
  let mouseY = 0;
  let windowWidth = 0;
  let invert = false;

  function addMouseListener() {
    document.addEventListener("mousemove", e => {
      mouseX = e.x;
      mouseY = e.y;

      invert = mouseX > windowWidth - 300;
    });
  }

  onMount(() => {
    addMouseListener();
  });
</script>

<style lang="scss">
  div {
    position: fixed;

    z-index: 20;

    padding: var(--size-unit-2);

    background-color: var(--color-white);
    border: 1px solid var(--color-dark-grey);

    pointer-events: none;

    max-width: 250px;

    line-height: 1.4;
  }
</style>

<svelte:window bind:innerWidth={windowWidth} />

{#if $tooltipDisplay}
  <div style={`top: ${mouseY}px; left: ${mouseX - (invert ? 250 : 0)}px`}>
    {$tooltipDisplay}
  </div>
{/if}
