<script>
  /** @type {number} */
  export let startYear;

  /** @type {number} */
  export let endYear = new Date(Date.now()).getFullYear();

  /** @type {string} */
  export let leftLabel;

  /** @type {string} */
  export let rightLabel;

  /** @type {number?} */
  export let width = null;

  /** @type {number[][]?} */
  export let collapse = null;

  if (!!endYear && endYear <= startYear)
    throw new Error("endYear must be higher than startYear");

  const years = 1 + endYear - startYear;
</script>

<div
  class="timeline"
  style="
    width: {!!width ? `${width}px` : '100%'};
    display: grid;
    grid-template: repeat({years * 13}, auto) / 1fr 125px 1fr;"
>
  <h2 class="timeline-header">{leftLabel}</h2>
  <div class="timeline-line fade-top" />
  <h2 class="timeline-header">{rightLabel}</h2>
  {#each Array(years) as _unused, i}
    {@const year = startYear + (years - i) - 1}
    {@const collapsed =
      !collapse?.every((c) => year > c[0] || year < c[1]) || false}
    {@const lineCollapsed =
      !collapse?.every((c) => year > c[0] || year < c[1] + 1) || false}
    <div class="timeline-circle{i === 0 ? '-current' : ''}" class:collapsed>
      <div class="timeline-circle-year">{year}</div>
    </div>
    <div
      class="timeline-line"
      class:fade-bottom={i + 1 >= years}
      class:lineCollapsed
    />
  {/each}
  <slot />
</div>

<style lang="scss">
  @import "../../theme/app.scss";

  $line-width: 6px;
  $circle-size: $line-width * 3;

  .timeline {
    &-line {
      min-height: 30px;
      width: $line-width;
      grid-row: span 11;
      grid-column: 2;
      background-color: $primary;
      border-radius: 3px;
      margin: -2px 0;

      .fade-top,
      .fade-bottom {
        grid-row: span 1;
      }

      &.lineCollapsed,
      &.startCollapse {
        min-height: 6px;
        margin: 3px;
      }
    }

    &-circle {
      width: $circle-size;
      height: $circle-size;
      grid-column: 2;
      border-radius: 100%;
      border: solid $primary $line-width;
      background-color: $background;

      &-current {
        @extend .timeline-circle;
        outline: solid $primary $line-width * 1.5;
        outline-offset: -$line-width * 3;
      }

      &.collapsed {
        height: 0;
        border: 0;

        .timeline-circle-year {
          display: none;
        }
      }

      &-year {
        transform: translate(-40px, 2px);
        font-size: small;
      }
    }

    &-line,
    &-circle {
      justify-self: center;
      // transform: translateY(($circle-size + $line-width * 2) * -0.5);
    }
  }

  .timeline-header {
    text-align: center;
  }
</style>
