<style lang="scss">
  .row {
    display: grid;

    grid-template-columns: repeat(6, 1fr);
    grid-column-gap: var(--size-unit-2);

    background-color: transparent;

    padding: var(--size-unit-3) var(--size-unit-2);

    border-bottom: 1px solid var(--color-dark-grey);

    &:last-of-type {
      border-bottom: none;
    }

    &:focus-within {
      background-color: var(--color-active);
    }

    .column {
      grid-column-end: span 2;
    }

    .sub-column {
      grid-column-end: span 1;
    }
  }
</style>

<div class="row">
  <div class="column">
    <slot name="title" />
  </div>
  <div class="sub-column">
    <slot name="subtitle" />
  </div>
  <div class="sub-column">
    <slot name="suffix" />
  </div>
  <div class="column">
    <slot name="value" />
  </div>
</div>
