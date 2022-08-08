<script>
  import Flip from "../lib/Flip.svelte";
  import { cardBackground } from "../lib/stores";

  import {
    firstCard,
    secondCard,
    numberOfTries,
    numberOfPairs,
  } from "../lib/stores";

  let flip = false;

  export let icon;

  function handleClick() {
    if (!$firstCard.flipped) {
      firstCard.set({
        icon,
        flipped: true,
      });
    } else {
      console.log($secondCard);
      secondCard.set({
        icon,
        flipped: true,
      });

      if ($firstCard.icon !== $secondCard.icon) {
        numberOfTries.set($numberOfTries + 1);
        setTimeout(() => {
          flip = !flip;
        }, 1000);
      } else {
        numberOfPairs.set($numberOfPairs + 1);
        firstCard.set({
          icon: "",
          flipped: false,
        });
        secondCard.set({
          icon: "",
          flipped: false,
        });
      }
    }

    flip = !flip;
  }
</script>

<div on:click={handleClick} class="card">
  <Flip height="200px" width="200px" {flip}>
    <img slot="front" src={$cardBackground} alt="card back" />
    <div class="back" slot="back">{icon}</div>
  </Flip>
</div>

<style>
  .back {
    margin: 0;
    padding: 0;
    font-size: 4rem;
    background: #efe;
    text-shadow: 1px 1px 2px black;
  }

  img,
  .back {
    display: block;
    width: var(--card-size);
    height: var(--card-size);
    display: grid;
    place-items: center;
    border-radius: 20px;
    border: 6px solid transparent;
  }

  img {
    height: 100%;
  }
</style>
