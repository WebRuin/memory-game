<script>
  import { cardBackground, numberOfTries, numberOfPairs } from "./lib/stores";
  import { shuffle } from "./lib/utils";
  import Card from "./lib/Card.svelte";

  import redBrick from "./assets/red-brick.svg";
  import rainbow from "./assets/rainbow.png";
  import network from "./assets/network.svg";
  import subtlePrism from "./assets/subtle-prism.png";
  import waveyFingerprint from "./assets/wavey-fingerprint.png";

  const backgrounds = [
    { name: "Red Brick", img: redBrick },
    { name: "Rainbow", img: rainbow },
    { name: "Network", img: network },
    { name: "Subtle Prism", img: subtlePrism },
    { name: "Wavey Fingerprint", img: waveyFingerprint },
  ];

  cardBackground.set(redBrick);

  function setCardBg(img) {
    console.log(img);
    cardBackground.set(img);
  }

  const icons = [
    "🍺",
    "🍺",
    "👽",
    "👽",
    "🦄",
    "🦄",
    "🍔",
    "🍔",
    "🪨",
    "🪨",
    "🦎",
    "🦎",
    "🤬",
    "🤬",
    "🔥",
    "🔥",
  ];

  const shuffledIcons = shuffle(icons);
</script>

<main>
  <header>
    <h1>The Memory Game</h1>
    <p>
      <strong>Click on the cards</strong> to find matching pairs.
    </p>
  </header>
  <div class="wrapper">
    <div>
      <h2>Themes</h2>
      <div class="backgrounds">
        {#each backgrounds as src}
          <div class="image">
            <img
              on:click={() => setCardBg(src.img)}
              src={src.img}
              alt={src.name}
            />
          </div>
        {/each}
      </div>
    </div>
    <div class="game-wrapper">
      <div class="stats">
        <p>{$numberOfTries} attempts</p>
        <p>{$numberOfPairs} pairs of 8</p>
      </div>
      <div class="grid">
        {#each shuffledIcons as icon}
          <Card {icon} />
        {/each}
      </div>
    </div>
  </div>
</main>

<style>
  .image {
    --size: 80px;
    width: var(--size);
    height: var(--size);
    overflow: hidden;
  }

  img {
    height: 100%;
  }
  .stats,
  .backgrounds {
    display: flex;
    justify-content: space-between;
  }

  .wrapper {
    display: grid;
    grid-template-columns: 1fr 3fr;
    gap: 4rem;
  }
  .grid {
    width: 800px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    justify-items: center;
    align-items: center;
  }
</style>
