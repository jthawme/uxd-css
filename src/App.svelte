<script>
  import Explorer from "./components/Explorer.svelte";
  import LinksList from "./components/LinksList.svelte";
  import Tooltip from "./components/Tooltip.svelte";

  const servicesLinks = [
    {
      to: "https://www.figma.com/",
      label: "Figma",
      sublabel: "Design",
      description: "Modern design software"
    },
    {
      to: "https://codesandbox.io/",
      label: "Code Sandbox",
      sublabel: "Development",
      description: "An online development IDE"
    },
    {
      to: "https://code.visualstudio.com/",
      label: "Visual Studio Code",
      sublabel: "Development",
      description: "Industry level code editor"
    },
    {
      to: "https://www.netlify.com/",
      label: "Netlify",
      sublabel: "Hosting",
      description: "Excellent 'static hosting' platform"
    },
    {
      to: "https://pages.github.com/",
      label: "Github Pages",
      sublabel: "Hosting",
      description: "Deploy sites through github, which promotes good standards"
    },
    {
      to: "https://glitch.com/",
      label: "Glitch",
      sublabel: "Code",
      description: "Fun take on a code site, a lot of interesting work"
    }
  ];

  const usefulLinks = [
    {
      to:
        "https://docs.google.com/presentation/d/19q6te9XQ-Moiid5hwJBbRYWJM7J-jfRarWd5rpdgbg0/edit?usp=sharing",
      label: "Slides"
    },
    {
      to: "https://codesandbox.io/s/uxd-mobile-base-n47my",
      label: "Starting Code",
      sublabel: "Designing Layouts"
    },
    {
      to: "https://www.figma.com/education/",
      label: "Figma for Education",
      sublabel: "Free for students",
      description: "Sign up for full features for free"
    },
    {
      to: "https://github.com/jthawme/uxd-css",
      label: "Code for this site",
      sublabel: "View code",
      description: "View all the code it took to make this site"
    }
  ];

  const furtherLinks = [
    {
      to: "https://v-fonts.com/",
      label: "V-Fonts",
      sublabel: "Variable fonts",
      description: "An explorer of current variable fonts out there"
    },
    {
      to: "https://css-tricks.com/",
      label: "CSS Tricks",
      sublabel: "Everything web",
      description: "Find articles about everything to do with the web"
    },
    {
      to: "https://developer.mozilla.org/",
      label: "MDN",
      sublabel: "Web Documentation",
      description: "The authority on web documentation"
    },
    {
      to: "https://ffconf.org/",
      label: "FFConf",
      sublabel: "Creative Web Conference",
      description: "A great conference in Brighton"
    },
    {
      to: "https://www.codecademy.com/",
      label: "Codeacademy",
      sublabel: "Online Course",
      description: "Some free well made online courses"
    },
    {
      to: "https://www.womenwhocode.com/",
      label: "Women Who Code",
      sublabel: "Meetup / Organisation",
      description: "An organisation that helps empower women in tech"
    },
    {
      to: "https://lab.arts.ac.uk/",
      label: "Lab.arts",
      sublabel: "Creative Lab",
      description: "Coding help in your very own university"
    }
  ];
</script>

<style lang="scss">
  .top {
    padding: var(--size-unit-2) var(--size-unit-2);
  }

  .links-group {
    display: grid;

    grid-template-columns: repeat(4, 1fr);
    grid-column-gap: var(--size-unit-2);

    padding-top: var(--size-unit-4);
    margin-bottom: var(--size-unit-4);

    div {
      grid-column-end: span 4;

      margin-bottom: var(--size-unit-8);
    }

    @media screen and (min-width: 560px) {
      div {
        grid-column-end: span 2;
      }
    }

    @media screen and (min-width: 800px) {
      grid-template-columns: repeat(12, 1fr);

      div {
        grid-column-end: span 4;

        &:last-of-type {
          grid-column-start: 9;
        }
      }
    }

    @media screen and (min-width: 1200px) {
      div {
        grid-column-end: span 3;

        &:last-of-type {
          grid-column-start: 10;
        }
      }
    }
  }

  .bottom {
    padding-top: calc(var(--size-unit-8) * 2);
  }

  h2 {
    padding-left: var(--size-unit-2);
    padding-right: var(--size-unit-2);
  }
</style>

<Tooltip />

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

  <section id="explorer" class="bottom">
    <h2>CSS Explorer</h2>
    <Explorer />
  </section>
</main>
