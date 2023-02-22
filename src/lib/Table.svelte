<script>
  /** @type {any[][]} */
  export let data;

  /** @type {string[]} */
  export let rowStyles = [];

  /** @type {string[]} */
  export let colStyles = [];
</script>

<table>
  {#each data as row, r}
    <tr style={rowStyles[r]}>
      {#each row as col, c}
        <td style={colStyles[c]}>
          {col || ""}
        </td>
      {/each}
    </tr>
  {/each}
</table>

<style lang="scss">
  table {
    border-collapse: collapse;
  }

  tr {
    height: 30px;
  }

  td {
    font-size: large;

    &:first-child {
      padding-right: 20px;
    }
  }
</style>
