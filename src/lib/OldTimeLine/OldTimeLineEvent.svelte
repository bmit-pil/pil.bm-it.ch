<script>
  import Paper, { Title, Subtitle, Content } from "@smui/paper";

  /** @type {string} */
  export let label;

  /** @type {{startDate: Date, endDate?: Date}} */
  export let timeSpan;

  /** @type {string?} */
  export let description = null;

  /** @type {string} */
  export let dateFormat = "dd.mm.yyyy";

  /** @type {number?} */
  export let width = null;

  /** @type {boolean} */
  export let current = false;

  /** @type {boolean} */
  export let parallel = false;

  /**
   * Takes a `Date` and returns it formatted after the `dateFormat`.
   *
   * The date format must be a string
   * and supports so far: `y` = year, `m` = month, `d` = day.
   *
   * @param {Date} date
   * @param {string} dateFormat
   * @returns {string}
   */
  function formatDate(date, dateFormat = "dd.mm.yyyy") {
    let separators = dateFormat.split(/[ymd]/).filter((d) => !!d);
    let formats = dateFormat.split(/[^ymd]/);
    let data = formats.map((f) => {
      let retval = ((v) => {
        switch (v) {
          case "y":
            return date.getFullYear();
          case "m":
            return date.getMonth();
          case "d":
            return date.getDay();
        }
      })(f[0])?.toString();
      return retval?.padStart(f.length, "0")?.substring(0, f.length);
    });
    return data.map((d) => `${d}${separators.pop() || ""}`).join("");
  }
</script>

<div
  class="paper-wrapper{parallel ? ' parallel' : ''}"
  style="width: {!!width ? `${width}px` : '44%'};"
>
  <Paper class="paper">
    <Title class="event-title">{label}</Title>
    <Subtitle class="event-subtitle">
      <code>
        {formatDate(timeSpan.startDate, dateFormat)}
        {timeSpan.endDate
          ? ` - ${formatDate(timeSpan.endDate, dateFormat)}`
          : current
          ? " - Aktuell"
          : ""}
      </code>
    </Subtitle>
    <Content class="event-content">
      {description || ""}
    </Content>
  </Paper>
  <div class="caret-wrapper">
    <div class="caret" />
  </div>
</div>

<style lang="scss">
  @import "../../theme/app.scss";

  $caret-size: 5px * 5; // $line-width = 5px

  .caret-wrapper {
    @include absolute-centered;
    right: -97%;
    width: fit-content;
    height: fit-content;
    padding: 5px;
    clip-path: polygon(55% 0, 100% 0, 100% 100%, 55% 100%);

    .caret {
      width: $caret-size;
      height: $caret-size;
      background-color: $light-surface;
      border-radius: 5px;
      transform: rotate(45deg);
    }
  }

  .paper-wrapper {
    position: relative;
    height: 100%;
  }

  * :global(.paper) {
    padding: 15px;
    background-color: $light-surface;
    height: max-content;
  }

  * :global(.event-title) {
    font-weight: bold;
    font-size: medium;
  }

  * :global(.event-subtitle) {
    font-size: small;
  }
</style>
