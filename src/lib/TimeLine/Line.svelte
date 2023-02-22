<script>
  /** @type {string} */
  export let width = "6px";

  /** @type {string} */
  export let height = "100%";

  /** @type {string} */
  export let color = "$primary";

  /** @type {"regular" | "dashed"} */
  export let type = "regular";

  /** @type {string} */
  export let gap = "6px";

  /** @type {string} */
  export let dashLength = "6px";
</script>

<div
  class="line-{type}"
  style="
    $color: {color};
    $width: {width};
    height: {height};
  "
/>

<style lang="scss">
  @import "../../theme/app.scss";

  $color: $primary;
  $width: 6px;

  .line {
    &-regular {
      width: $width;
      background-color: $color;
    }
    &-dashed {
      width: 0;
      border-right: $width;
    }
  }
</style>
