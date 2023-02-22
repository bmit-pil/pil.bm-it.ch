<script>
  import OldTimeLine from "$lib/OldTimeLine/OldTimeLine.svelte";
  import OldTimeLineNode from "$lib/OldTimeLine/OldTimeLineNode.svelte";
  import Table from "$lib/Table.svelte";
  import TimeLine from "$lib/TimeLine/TimeLine.svelte";
  import TimeLineEvent from "$lib/TimeLine/TimeLineEvent.svelte";
  import TypeWriter from "$lib/TypeWriter.svelte";
  import Card, { Media, MediaContent } from "@smui/card";

  const birthday = new Date(2004, 8, 2);
  const age = new Date(Date.now() - birthday.getTime()).getUTCFullYear() - 1970;
</script>

<h1><TypeWriter text="Welcome" /></h1>
<div class="grid">
  <Card class="portrait">
    <Media>
      <img
        src="https://via.placeholder.com/300x400"
        alt="Portrait Leandro Piras"
      />
      <MediaContent>
        <div class="portrait-content">
          <h2>Leandro Piras ({age})</h2>
          <br />
          <p>🎂 02.09.2004 | 🇨🇭 🇮🇹</p>
        </div>
      </MediaContent>
    </Media>
  </Card>

  <span class="vertical-rule" />

  <TimeLine
    startYear={2011}
    leftLabel="Berufliche Tätigkeiten"
    rightLabel="Schulische Ausbildung"
    collapse={[[2017, 2012]]}
    width={800}
  >
    <TimeLineEvent
      label="ESPAS, Zürich"
      description="Lehre als Applikationsentwickler"
      startDate={{ year: 2022, month: 11 }}
    />
    <TimeLineEvent
      label="Appisberg, Männedorf"
      description="Berufsabklärung"
      startDate={{ year: 2022, month: 9 }}
      endDate={{ year: 2022, month: 10 }}
      className="appisberg"
    />
    <TimeLineEvent
      label="SIX, Zürich"
      description="Lehre als Applikationsentwickler"
      startDate={{ year: 2020, month: 8 }}
      endDate={{ year: 2022, month: 8 }}
      className="six"
    />
    <TimeLineEvent
      label="Technische Berufsschule Zürich"
      column="right"
      startDate={{ year: 2020, month: 8 }}
    />
    <TimeLineEvent
      label="Sekundarschule Watt"
      column="right"
      startDate={{ year: 2017, month: 8 }}
      endDate={{ year: 2020, month: 8 }}
    />
    <TimeLineEvent
      label="Primarschule Eselriet"
      column="right"
      startDate={{ year: 2011, month: 8 }}
      endDate={{ year: 2017, month: 8 }}
    />
  </TimeLine>
  <hr />
  <div class="languages">
    <h2>Sprachkenntnisse</h2>
    <Table
      data={[
        ["Deutsch (CH)", "C2"],
        ["Englisch", "B2+"],
        ["Italienisch", "A2"],
        ["Französisch", "A2"],
      ]}
      colStyles={["", "font-size: x-large; color: #ba70ff; font-weight: bold;"]}
    />
  </div>
</div>
<hr />
<!-- <div class="row timelines">
  <OldTimeLine title="Berufliche Tätigkeiten">
    <OldTimeLineNode
      event={{
        label: "ESPAS, Zürich",
        description: "Lehre als Applikationsentwickler",
        timeSpan: { startDate: new Date(2022, 11) },
      }}
      current
    />
    <OldTimeLineNode
      event={{
        label: "Appisberg, Männedorf",
        description: "Berufsabklärung",
        timeSpan: { startDate: new Date(2022, 8), endDate: new Date(2022, 11) },
      }}
    />
    <OldTimeLineNode
      event={{
        label: "SIX, Zürich",
        description: "Lehre als Applikationsentwickler",
        timeSpan: { startDate: new Date(2020, 8), endDate: new Date(2022, 8) },
      }}
    />
  </OldTimeLine>
  <OldTimeLine title="Schulische Ausbildung">
    <OldTimeLineNode
      event={{
        label: "Technische Berufsschule Zürich",
        timeSpan: { startDate: new Date(2022, 0) },
      }}
      current
    />
    <OldTimeLineNode
      event={{
        label: "Sekundarschule Watt",
        timeSpan: { startDate: new Date(2017, 0), endDate: new Date(2020, 0) },
      }}
    />
    <OldTimeLineNode
      event={{
        label: "Primarschule Eselriet",
        timeSpan: { startDate: new Date(2011, 0), endDate: new Date(2017, 0) },
      }}
    />
  </OldTimeLine>
</div> -->
<hr />

<style lang="scss">
  @import "../theme/app.scss";

  .grid {
    display: grid;
    grid-template-columns: auto auto auto;
    grid-template-rows: auto auto auto;
    align-items: start;
    justify-content: space-between;

    &.timelines {
      align-items: stretch;
      justify-content: start;
      gap: 150px;
    }

    hr {
      grid-row: 2;
      grid-column: 1;
    }
  }

  .languages {
    grid-column: 1;
    grid-row: 3;

    h2 {
      margin-top: 0;
    }
  }

  .vertical-rule {
    width: 2px;
    height: 100%;
    background: $dark;
  }

  * :global(.timeline),
  .vertical-rule {
    grid-row: 1 / span 3;
  }

  * :global(.portrait) {
    width: max-content;
    overflow: hidden;
    line-height: 0%;
  }

  :global(.portrait-content) {
    position: absolute;
    left: 5%;
    bottom: 2%;

    h2 {
      color: white;
    }
  }

  * :global(.appisberg) {
    height: fit-content;
    margin-bottom: 28px;
  }

  * :global(.six) {
    margin-top: -35px;
  }
</style>
