<script>
  const ingredients = [
    "Top Bun",
    "Bacon",
    "Cheese",
    "Lettuce",
    "Bacon",
    "Cheese",
    "Lettuce",
    "Bacon",
    "Cheese",
    "Lettuce",
    "Bottom Bun",
  ];

  const progressionMessages = [
    "are you SURE you want to add this ingredient?",
    "are you REALLY SURE you want to add this ingredient?",
    "are you REALLY REALLY SURE you want to add this ingredient?",
    "are you REALLY REALLY REALLY SURE you want to add this ingredient?",
    "are you REALLY REALLY REALLY REALLY SURE you want to add this ingredient?",
    "ONG YOU WANT TO ADD THIS????",
    "FOR REAL NO CAP YOU WANT TO ADD THIS INGREDIENT???",
    "NO CAP FRFR ONG ADD THIS SHIT??",
    "yk what, no you're not adding this! fuck you👋",
  ];

  let currentIngredient = "";
  let currentMessage = 0;
  let show = false;
  let selectedIngredient = "";
  let message = "are you SURE you want to add this ingredient?";
  function displayPopUp(ingredient) {
    selectedIngredient = ingredient;
    show = true;
  }

  function closePopUp() {
    currentMessage = 0;
    if (Math.random() > 0.8) {
      currentIngredient = selectedIngredient + ": even though confirmation message was wrong, it's okay! 😊";
    } else {
      currentIngredient =
        "there you go, you pissed off the confirmation message 😭";
    }
    show = false;
  }
  function progressPopUp() {
    currentMessage += 1;
    if (currentMessage == progressionMessages.length) closePopUp();
    message = progressionMessages[currentMessage];
  }
</script>
<h2 class="title">
Don't piss of the confirmation box!
</h2>

{#if show}
  <div class="overlay">
    <div class="overlay-content">
      <h2>{selectedIngredient}</h2>
      <p>{message}</p>
      <div class="progression">
        <button onclick={() => closePopUp()}>Close</button>
        <button onclick={() => progressPopUp()}>Yea?</button>
      </div>
    </div>
  </div>
{/if}

<div class="elements">
  <div class="burger">
    <p>{currentIngredient}</p>
    <select name="nigga" id="fr?">
      {#each ingredients as ingredient}
        <option onclick={() => displayPopUp(ingredient)} value={ingredient}
          >{ingredient}</option
        >
      {/each}
    </select>
  </div>
</div>

<style>
  .overlay {
    z-index: 10;
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .progression{
    display: flex;
    justify-content: center;
    align-items: center;
    
  }
  .overlay-content {
    background-color: white;
    padding: 20px;
    border-radius: 10px;
  }

  .burger {
    width: fit-content;
    height: fit-content;
    display: flex;
    flex-direction: column;
  }
</style>
