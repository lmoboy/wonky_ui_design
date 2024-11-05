<script module>
  import Slider from '$lib/Components/SliderVolume.svelte';
  import Braile from '$lib/Components/BrailleInput.svelte';
  import Burger from '$lib/Components/DropBurger.svelte';
  import Date from '$lib/Components/DatePicker.svelte';
</script>

<script>
  let currentPage = 0;
  const pages = [Slider, Braile, Burger, Date];

  function next() {
    currentPage = (currentPage + 1) % pages.length;
  }

  function prev() {
    currentPage = (currentPage - 1 + pages.length) % pages.length;
  }
</script>

<div class="main">
  <div class="buttons">
    <button onclick={prev}>prev</button>
    <button onclick={next}>next</button>
  </div>
  <svelte:component this={pages[currentPage]} />

</div>

<style>
  .main {
    background-color: gray;
    width: 100%;
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin: 0;
    padding: 0;
  }
  .buttons {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 20px;
    top:0;
    position:absolute;
  }
</style>
