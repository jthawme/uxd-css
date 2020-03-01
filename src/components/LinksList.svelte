<script>
  export let title = "";
  export let links = [];
</script>

<style lang="scss">
  .title {
    font-size: var(--body-font-size);

    margin: 0 0 var(--size-unit-4);
  }

  ul {
    padding: 0;
    margin: 0;

    list-style: none;

    li {
      margin-bottom: var(--size-unit-2);
    }

    a {
      color: var(--color-text);
      text-decoration: none;

      &:hover,
      &:active {
        opacity: 0.5;
      }

      span {
        display: block;

        color: var(--color-dark-grey);
      }
    }
  }

  @media screen and (min-width: 768px) {
    ul {
      a {
        span {
          display: inline;
        }
      }
    }
  }
</style>

<p class="title">{title}</p>

<ul>
  {#each links as link}
    <li>
      <a href={link.to} target="_blank">
        {link.label}
        {#if link.sublabel}
          <span>– {link.sublabel}</span>
        {/if}
      </a>
    </li>
  {/each}
</ul>
