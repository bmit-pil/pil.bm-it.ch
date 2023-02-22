<script>
  import Paper, { Title, Subtitle, Content } from "@smui/paper";

  /** @type {string} */
  export let label;

  /** @type {number} */
  export let lastYear = new Date(Date.now()).getFullYear();

  /** @typedef {{year: number, month: number | undefined}} ShortDate */

  /** @type {ShortDate} */
  export let startDate;

  /** @type {ShortDate} */
  export let endDate = {
    year: new Date(Date.now()).getFullYear(),
    month: new Date(Date.now()).getMonth() + 1,
  };

  /** @type {string} */
  export let className = "";

  /** @type {string?} */
  export let description = null;

  /** @type {"left" | "right"} */
  export let column = "left";

  const start = startDate.year * 12 + (startDate.month || 0);
  const end = endDate.year * 12 + (endDate.month || 0);
  const startRow =
    (lastYear + 1 - endDate.year) * 12 - (endDate.month || 0) + 2;
  const endRow = `span ${end - start}`;

  /**
   * Takes two dates and returns a string representing the timespan.
   *
   * @param {ShortDate} startDate
   * @param {ShortDate | "not-finished"} endDate
   * @returns {string}
   */
  function formatTimeSpan(startDate, endDate) {
    const extract = /** @param {ShortDate} d */ (d) => {
      return (!!d.month ? `${String(d.month).padStart(2, "0")}.` : "") + d.year;
    };
    return (
      extract(startDate) +
      (endDate !== "not-finished" ? ` - ${extract(endDate)}` : "")
    );
  }
</script>

<div
  class="timeline-event-{column} {className}"
  style="grid-row: {startRow} / {endRow}"
>
  <Paper class="paper">
    <Title class="event-title">
      {label}
      <div class="description">{description || ""}</div>
      <!-- <code class="event-timespan">{formatTimeSpan(startDate, endDate)}</code> -->
    </Title>
  </Paper>
</div>

<style lang="scss">
  @import "../../theme/app.scss";

  .timeline-event {
    padding: 2px;

    &-left {
      @extend .timeline-event;
      grid-column: 1;
    }
    &-right {
      @extend .timeline-event;
      grid-column: 3;
    }
  }

  * :global(.paper) {
    background-color: $light-surface;
    padding: 0px 5px;
    height: 100%;
  }

  * :global(.event-title) {
    font-weight: bold;
    font-size: medium;
  }

  * :global(.event-timespan) {
    font-size: small;
    float: right;
  }

  .description {
    float: right;
    font-size: small;
    font-weight: normal;
  }
</style>
