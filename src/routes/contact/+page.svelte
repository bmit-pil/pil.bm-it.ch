<script>
  import Table from "$lib/Table.svelte";
  import TypeWriter from "$lib/TypeWriter.svelte";
</script>

<h1><TypeWriter text="Kontakt" /></h1>
<Table
  data={[
    ["E-Mail", "leandro@piras.li"],
    ["E-Mail Geschäft", "leandro.piras@espas.ch"],
    ["Mobile", "076 496 93 20"],
    ["Festnetz", "052 343 93 20"],
  ]}
/>
