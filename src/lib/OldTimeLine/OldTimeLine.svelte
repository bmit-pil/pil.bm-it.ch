<script>
  /** @type {string?} */
  export let title;
</script>

<div class="timeline">
  {#if !!title} <h2 class="title">{title}</h2> {/if}
  <slot />
</div>

<style lang="scss">
  .timeline {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
    flex-wrap: wrap;

    .title {
      align-self: flex-start;
    }
  }
</style>
