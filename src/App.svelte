<script>
  const colours = ["yellow", "red", "green", "blue", "black"];

  let sounds = {};
  let active = false;
  let colour;
  let innerHeight;
  let last_time;

  (function () {
    for (let name of colours) {
      var sound = new Audio(name + ".mp3");
      sound.preload = "auto";
      sound.playbackRate = 2;
      sounds[name] = sound;
    }
  })();

  async function playsound() {
    sounds[colour].play();
  }

  function validClick() {
    var now = window.performance.now();
    if (active && now - last_time < 200 /* ms*/) {
      return false; /* ignore the click */
    }
    last_time = now;
    return true;
  }

  function handleClick() {
    if (!validClick()) {
      return;
    }
    active = !active;
    if (!active) {
      return;
    }
    colour = colours[Math.floor(Math.random() * colours.length)];
    playsound();
  }
</script>

<svelte:window bind:innerHeight />

<main>
  <!-- svelte-ignore a11y-click-events-have-key-events -->
  <div on:click={handleClick}>
    {#if active}
      <div
        style="height: {innerHeight * 0.9}px; 
          width: 100%; 
          background-color: {colour}"
      />
    {:else}
      <img
        style="height: auto; max-width: 100%"
        src="FBC_Lerum_logo.jpg"
        alt="Click me"
      />
    {/if}
  </div>
</main>

<style>
</style>
