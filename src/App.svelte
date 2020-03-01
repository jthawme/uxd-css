<script>
  import Explorer from "./components/Explorer.svelte";
  import LinksList from "./components/LinksList.svelte";

  const servicesLinks = [
    { to: "https://www.figma.com/", label: "Figma", sublabel: "Design" },
    {
      to: "https://codesandbox.io/",
      label: "Code Sandbox",
      sublabel: "Development"
    },
    {
      to: "https://code.visualstudio.com/",
      label: "Visual Studio Code",
      sublabel: "Development"
    },
    {
      to: "https://www.netlify.com/",
      label: "Netlify",
      sublabel: "Hosting"
    },
    {
      to: "https://pages.github.com/",
      label: "Github Pages",
      sublabel: "Hosting"
    },
    {
      to: "https://glitch.com/",
      label: "Glitch",
      sublabel: "Code"
    }
  ];

  const usefulLinks = [
    { to: "https://www.jthaw.me/", label: "Slides" },
    {
      to: "https://jthaw.me",
      label: "Starting Code",
      sublabel: "Designing Layouts"
    }
  ];

  const furtherLinks = [
    {
      to: "https://www.jthaw.me/",
      label: "CSS Tricks",
      sublabel: "Everything web"
    },
    {
      to: "https://jthaw.me",
      label: "MDN",
      sublabel: "Web Documentation"
    },
    {
      to: "https://jthaw.me",
      label: "FFConf",
      sublabel: "Creative Web Conference"
    },
    {
      to: "https://jthaw.me",
      label: "Codeacademy",
      sublabel: "Online Course"
    },
    {
      to: "https://jthaw.me",
      label: "Lab.arts",
      sublabel: "Creative Lab"
    }
  ];
</script>

<style lang="scss">
  .top {
    padding: var(--size-unit-2) var(--size-unit-2);
  }

  .links-group {
    display: grid;

    grid-template-columns: repeat(12, 1fr);
    grid-column-gap: var(--size-unit-2);

    padding-top: var(--size-unit-4);
    margin-bottom: var(--size-unit-4);

    div {
      grid-column-end: span 3;

      &:last-of-type {
        grid-column-start: 10;
      }
    }
  }

  .bottom {
    padding-top: var(--size-unit-4);
  }

  h2 {
    padding-left: var(--size-unit-2);
    padding-right: var(--size-unit-2);
  }
</style>

<main>
  <section class="top">
    <h1>UXD – Modern CSS</h1>
    <div class="links-group">
      <div>
        <LinksList title="Services" links={servicesLinks} />
      </div>
      <div>
        <LinksList title="Useful Links" links={usefulLinks} />
      </div>

      <div>
        <LinksList title="Further Learning" links={furtherLinks} />
      </div>
    </div>
  </section>

  <section class="bottom">
    <h2>CSS Explorer</h2>
    <Explorer />
  </section>
</main>
