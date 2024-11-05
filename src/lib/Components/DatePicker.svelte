<script module>
  import { onMount } from "svelte";
</script>

<script>
  //region VARIABLES
  let date = $state("");
  let curImage = $state(0);
  let tempDate = $state("");
  let setDate = $state("");
  let hasMatch = $state(false);

  let matchDate = $state("");

  let dateContainer;

  const links = [
    "https://nineplanets.org/wp-content/uploads/2019/09/mercury.png",
    "https://nineplanets.org/wp-content/uploads/2019/09/venus.png",
    "https://nineplanets.org/wp-content/uploads/2019/09/earth.png",
    "https://nineplanets.org/wp-content/uploads/2019/09/mars.png",
    "https://nineplanets.org/wp-content/uploads/2019/09/jupiter.png",
    "https://nineplanets.org/wp-content/uploads/2019/09/saturn.png",
    "https://nineplanets.org/wp-content/uploads/2019/09/uranus.png",
    "https://nineplanets.org/wp-content/uploads/2019/09/neptune.png",
  ];
  //endregion
  //region ONMOUNT
  onMount(() => {
    dateContainer = document.querySelector(".dateContainer");
    const currentDate = new Date();
    date = currentDate.toDateString();
  });
  //endregion
  //region FUNCTIONS
  function niggawhat() {
    matchDate = date;
    setDate = tempDate.toJSON().slice(0, 10);
    hasMatch = false;
  }
  function close() {
    hasMatch = false;
  }

  function tryMatch(){
    let current = Math.random();
    if(current > 0.9){
        forceMatch()
    }
 }



  function swipeRight() {
    dateContainer.style = "transform: translateX(100px) rotate(45deg); opacity: 0;";
    const newDate = new Date(date);
    newDate.setDate(newDate.getDate() + 1);
    date = newDate.toDateString();
    tempDate = newDate;
    curImage = (curImage + 1) % links.length;
    setTimeout(() => {
        tryMatch();
      dateContainer.style = "";
    }, 500);
  }

  function swipeLeft() {
    dateContainer.style = "transform: translateX(-100px) rotate(-45deg); opacity: 0; ";
    const newDate = new Date(date);
    newDate.setDate(newDate.getDate() - 1);
    date = newDate.toDateString();
    tempDate = newDate;
    curImage = (curImage - 1 + links.length) % links.length;
    setTimeout(() => {
      dateContainer.style = "";
    }, 500);
  }

  function forceMatch() {
    hasMatch = true;
  }


  //endregion
</script>
<input type="date" disabled value={setDate} style="width: fit-content; height: fit-content"/>
<h2>
    Match your date simulator 💘
</h2>

<div class="match" style="{hasMatch ? 'opacity: 1;  display: flex' : 'opacity: 0; display: none'}">
    <div class="matchText">MATCH</div>
    {#each links as link, index}
      <img
        src={link}
        alt=""
        style="display: {curImage === index ? 'block' : 'none'}"
      />
    {/each}
    <div class="matchText">YOU HIT A MATCH WITH THIS DATE</div>
    <div class="matchText">IT IS {date}</div>
    <div class="matchText">ACCEPT?</div>
    <div class="matchButtons">
      <button onclick={niggawhat}>ACCEPT</button>
      <button onclick={close}>DECLINE</button>
    </div>
  </div>
<div class="container">


  <button class="swipeLeft" onclick={swipeLeft} >❌</button>
  <div class="dateContainer">
    <div class="date">DATING:{matchDate ? matchDate : 'no bitches 😭😭😭😭😭😭😭'}</div>
    <div class="mercuryContainer">
      {#each links as link, index}
        <img
          src={link}
          alt=""
          style="display: {curImage === index ? 'block' : 'none'};"
        />
      {/each}
    </div>
    <div class="textContainer">
      <div class="text">would you like to date this?</div>
      <div>{date}</div>
    </div>
  </div>
  <button class="swipeRight" onclick={swipeRight}>✔️</button>
</div>

<style>
  .container {
    width: 300px;
    height: 400px;
    display: flex;
    justify-content: center;
    align-items: center;
  
    gap: 20%;
    z-index: 1;
  }

  .match {
    position: absolute;
    transition: all 0.5s ease;
    backdrop-filter: blur(30px);
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    z-index: 100;
  }

  .match .matchText {
    font-size: 20px;
    font-weight: bold;
    color: black;
    padding: 10px;
    background-color: white;
    font-family: "Courier New", Courier, monospace;
  }
  .matchButtons {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }
  .matchButtons button {
    margin: 10px;
    padding: 10px;
    border-radius: 20px;
    background-color: white;
    font-size: 15px;
    font-weight: bold;
    color: black;
    font-family: "Courier New", Courier, monospace;
  }

  .matchButtons button:hover {
    background-color: gray;
    color: white;
  }

  .dateContainer {
    transition: all 0.5s ease;
    position: inherit;
    padding: 10px;
    background-color: white;


    border-radius: 20px;



    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    width: 100%;
    height: 100%;
  }
  .dateContainer img {
    position: static;
    top: 0;
    width: fit-content;
    height: fit-content;
  }

  .dateContainer .text {
    font-size: 10px;
    font-weight: bold;
    color: black;
    font-family: "Courier New", Courier, monospace;
  }

  .swipeLeft {
    left: 0;
    top: 0;
    width: 50px;
    height: 100%;
  }

  .swipeRight {
    right: 0;
    top: 0;
    width: 50px;
    height: 100%;
  }
</style>




