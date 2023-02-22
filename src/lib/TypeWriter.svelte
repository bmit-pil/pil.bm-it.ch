<script>
  /** @type {string} */
  export let text;
  /** @type {number} */
  export let speed = 100;

  let content = "";
  let tick = 0;
  let interval = setInterval(() => {
    write();
  }, speed);

  function write() {
    if (!text[tick]) {
      clearInterval(interval);
      return;
    }
    content += text[tick];
    tick++;
  }
</script>

<code class="typewriter">{content}</code>

<style lang="scss">
  $primary: #ba70ff;

  .typewriter {
    font-family: "Fira Code", "Courier New", Courier, monospace;
    overflow: hidden; /* Ensures the content is not revealed until the animation */
    border-right: 0.15em solid $primary; /* The typwriter cursor */
    white-space: nowrap; /* Keeps the content on a single line */
    animation: blink-caret 0.75s step-end infinite;
  }

  /* The typewriter cursor effect */
  @keyframes blink-caret {
    from,
    to {
      border-color: transparent;
    }
    50% {
      border-color: $primary;
    }
  }
</style>
