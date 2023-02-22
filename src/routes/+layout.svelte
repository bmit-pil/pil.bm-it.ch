<script>
  import Button from "@smui/button";
  import IconButton, { Icon } from "@smui/icon-button";
  import { page } from "$app/stores";

  /**
   * @typedef {{label:string, url:string}} navRoute
   * @type {navRoute[]}
   */
  const navRoutes = [
    { label: "Home", url: "/" },
    { label: "Projekte", url: "/projects" },
    { label: "Kontakt", url: "/contact" },
  ];

  let isDarkMode = false;

  function switchMode() {
    isDarkMode = !isDarkMode;
    console.log("switch pls");
  }
</script>

<nav>
  {#each navRoutes as navRoute}
    <Button
      href={navRoute.url}
      variant={$page.url.pathname === navRoute.url ? "unelevated" : "text"}
      class="nav-button"
    >
      {navRoute.label}
    </Button>
  {/each}
  <!-- <IconButton on:click={switchMode} toggle>
    <Icon class="material-icons mode-toggle" on>dark_mode</Icon>
    <Icon class="material-icons mode-toggle">light_mode</Icon>
  </IconButton> -->
</nav>
<div class="main">
  <slot />
</div>
<footer>FOOTER</footer>

<style lang="scss">
  @import "../theme/app.scss";

  nav,
  footer {
    left: 0;
    right: 0;
    padding: 10px;
    display: flex;
    flex-direction: row;
    align-items: center;
    height: fit-content;
    justify-content: center;
    background: #414141;
    z-index: 99;
  }

  nav {
    position: fixed;
  }

  footer {
    margin-top: auto;
  }

  * :global(hr) {
    border: solid $dark 1px;
    margin: 30px 0;
  }

  .main {
    background: #353535;
    padding: 100px 20px;
    justify-content: center;

    @media (min-width: 700px) {
      padding: 100px;
    }

    @media (min-width: 1000px) {
      padding: 100px 250px;
    }
  }

  * :global(.nav-button) {
    padding: 0px 16px;

    &::before {
      opacity: 1;
    }

    &:hover::before {
      opacity: 0.5;
    }
  }
</style>
