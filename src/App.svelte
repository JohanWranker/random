<script>
  const colours = ["yellow", "red", "green", "blue", "black"];
  let soundddd = [
    new Audio("yellow.mp3"),
    new Audio("red.mp3"),
    new Audio("green.mp3"),
    new Audio("blue.mp3"),
    new Audio("black.mp3"),
  ];

  let sounds = [];
  let active = false;
  let index = 0;
  let init = false;

  //for (let i = 0; i < colours.length; i++) {
  //var path = colours[i] + ".mp3";
  //var sound = new Audio(path);
  //sound.preload = "auto";
  //sounds.push(sound);
  //}

  //for (let name of colours)
  //var path = name + ".mp3";
  // var sound = new Audio(path);
  // sound.preload = "auto";
  // sounds.push(sound);

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
      console.log(index);
    }
  }

  function handleClick() {
    active = !active;
    index = Math.floor(Math.random() * colours.length);
    playsound();
  }
</script>

<main>
  <!-- svelte-ignore a11y-click-events-have-key-events -->
  {#if active}
    <div
      style="--theme-color: {colours[index]}"
      class="box"
      on:click={handleClick}
    />
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
