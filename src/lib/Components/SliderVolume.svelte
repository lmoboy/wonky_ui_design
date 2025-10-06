<script>
import { fly } from "svelte/transition";

  //region VARIABLES

  let time = $state(0);
  let speed = $state(0);
  let text = $state("");
  let start = $state(false);
  const words = [
    "skibidi",
    "sigma",
    "this",
    "world",
    "has",
    "ever",
    "seen",
    "cat",
    "dog",
    "duck",
    "pig",
    "ohio",
    "giga",
  ];

  let textToMatch = $state(
    Array(Math.floor(Math.random() * 10) + 1)
      .fill(0)
      .map((_, i) => words[Math.floor(Math.random() * words.length)])
      .join(" ")
  );
  //endregion

  //region FUNCTIONS

  function calculateWPM(text, timeInSeconds) {
    const words = text.trim().split(/\s+/).length;
    const timeInMinutes = timeInSeconds / 60;
    return Math.floor(words / timeInMinutes);
  }

  //endregion

  //region TIMERS
  let Timer = setInterval(() => {
    if (!start) return;
    time += 0.1;
    if (time > 20) {
      clearInterval(Timer);
      time = null;
      text = "try again";
    }
    time = Math.round(time * 10) / 10;
  }, 100);

  //endregion

  //region EFFECTS

  $effect(() => {
    if (text == textToMatch) {
      clearInterval(Timer);
      speed = calculateWPM(text, time);
      time = 0;
      text = "";
      textToMatch = Array(Math.floor(Math.random() * 10) + 1)
        .fill(0)
        .map((_, i) => words[Math.floor(Math.random() * words.length)])
        .join(" ");
      Timer = setInterval(() => {
        if (!start) return;
        time += 0.1;
        if (time > 20) {
          clearInterval(Timer);
          time = null;
          text = "try again";
        }
        time = Math.round(time * 10) / 10;
      }, 100);
      start = false;
    }
  });

  function onkeyup(event) {
    if (time === null) return;

    if (event.key === "Backspace") {
      text = text.substring(0, text.length - 1);
      return;
    }
    if (event.key.length > 1) {
      return;
    } else {
      text += event.key;
    }
  }
  //endregion
  // region MARKUP
</script>

<svelte:document on:keyup={onkeyup} />
Words per minute volume slider!


<div class="container">
  {#if !start}
    <input
      oninput={() => {
        start = true;
      }}
      type="range"
      min="0"
      max="100"
      value={speed ? (speed > 100 ? 100 : speed) : speed}
    />
    {speed ? (speed > 100 ? 100 : speed) : speed}%
  {/if}
  {#if start}
    {#if time != null}
      time: {time}
      <p>{textToMatch}</p>
    {/if}
    <div class="textDiv">
      {#each text as letter, i (i)}
        <p
          style={letter === textToMatch[i]
            ? "color: #39FF14"
            : "color:  #ff073a"}
          transition:fly={{ y: 20, duration: 200 }}
        >
          {letter === " " ? "\u00A0" : letter}
        </p>
      {/each}
    </div>
  {/if}
</div>

<style>
  .textDiv {
    display: flex;
    flex-direction: row;
    align-items: start;
    justify-content: start;
    height: 100%;
  }
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: fit-content;
    height: fit-content;
  }
</style>
