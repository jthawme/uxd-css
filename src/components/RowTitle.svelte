<style lang="scss">
  .row {
    display: grid;

    grid-template-columns: repeat(6, 1fr);
    grid-column-gap: var(--size-unit-2);

    background-color: var(--color-white);

    padding: var(--size-unit-3) var(--size-unit-2);

    border-bottom: 1px solid var(--color-dark-grey);

    .column {
      grid-column-end: span 2;
    }
  }
</style>

<div class="row">
  <div class="column">
    <slot name="title" />
  </div>
  <div class="column">
    <slot name="subtitle" />
  </div>
  <div class="column">
    <slot name="value" />
  </div>
</div>
