<script>
  import Flip from "../lib/Flip.svelte";
  import bg from "../assets/bg.svg";

  let flip = false;

  export let icon;

  function handleClick() {
    flip = !flip;
  }
</script>

<div on:click={handleClick} class="card">
  <Flip height="200px" width="200px" {flip}>
    <img slot="front" src={bg} alt="card back" />
    <p slot="back">{icon}</p>
  </Flip>
</div>

<style>
  p {
    margin: 0;
    padding: 0;
    font-size: 4rem;
    background: #efe;
    text-shadow: 1px 1px 2px black;
  }
  p,
  img {
    width: 200px;
    height: 200px;
    display: grid;
    place-items: center;
    border-radius: 20px;
    border: 6px solid transparent;
  }
</style>
