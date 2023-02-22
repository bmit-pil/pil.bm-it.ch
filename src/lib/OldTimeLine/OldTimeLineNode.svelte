<script>
  import OldTimeLineEvent from "./OldTimeLineEvent.svelte";

  /**
   * @typedef {{label: string, description?: string, timeSpan: {startDate: Date, endDate?: Date}, dateFormat?: string, width?: number}} EventData
   */

  /** @type {EventData} */
  export let event;

  /** @type {EventData?} */
  export let parallelEvent = null;

  /** @type {boolean} */
  export let current = false;

  let parallel = !!parallelEvent;
</script>

<div class="event">
  <OldTimeLineEvent {...event} />
  <div class="event-line" />
  <div class="event-circle{current ? '-current' : ''}" />
  {#if !!parallelEvent}
    <OldTimeLineEvent {...parallelEvent} {parallel} />
  {/if}
</div>

<style lang="scss">
  @import "../../theme/app.scss";

  $line-width: 6px;
  $circle-size: $line-width * 3;

  .event {
    position: relative;
    width: 100%;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;

    &:nth-child(odd) {
      flex-direction: row-reverse;

      :global(.caret-wrapper) {
        right: 0;
        left: -97%;
        transform: rotate(180deg);
      }
    }

    &:nth-child(2) .event-line {
      top: 50%;
    }

    &:last-child .event-line {
      bottom: 50%;
    }

    &-line {
      @include absolute-centered;
      width: $line-width;
      background-color: $primary;
    }

    &-circle {
      @include absolute-centered;
      width: $circle-size;
      height: $circle-size;
      border-radius: 100%;
      border: solid $primary $line-width;
      background-color: $background;

      &-current {
        @extend .event-circle;
        outline: solid $primary $line-width * 1.5;
        outline-offset: -$line-width * 3;
      }
    }
  }
</style>
