<script>
  const colours = ["yellow", "red", "green", "blue", "black"];

  let sounds = [];
  let active = false;
  let index = 0;
  let init = false;
  let innerHeight;

  let last_time = window.performance.now();
  

  async function playsound() {
    if (init == false) {
      init = true;
      for (let name of colours) {
        console.log(name);
        var path = name + ".mp3";
        var sound = new Audio(path);
        sound.preload = "auto";
        sound.playbackRate = 2;
        sounds.push(sound);
      }
    }
    if (active) {
      sounds[index].play();
    }
  }

  function validClick() {
    var now = window.performance.now();
    var diff = now - last_time; /* ms*/
    if (active && diff < 200) {
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
    index = Math.floor(Math.random() * colours.length);
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
          background-color: {colours[index]}"
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
