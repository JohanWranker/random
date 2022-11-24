<script>
  const colours = ["yellow", "red", "green", "blue", "black"];
  let active = false;
  let colour;
  function handleClick() {
    active = !active;
    colour = colours[Math.floor(Math.random() * colours.length)];
  }
</script>

<main>
  <!-- svelte-ignore a11y-click-events-have-key-events -->
  {#if active}
    <div style="--theme-color: {colour}" class="box" on:click={handleClick} />
  {:else}
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <img
      style="--theme-color: transparent"
      class="box"
      on:click={handleClick}
      src="FBC_Lerum_logo.jpg"
      alt="Click me"
    />
  {/if}
</main>

<style>
  .box {
    height: 711px;
    width: 1179px;
    background-color: var(--theme-color);
  }
</style>
