<script>
  import Card from "./lib/Card.svelte";

  function shuffle(array) {
    let currentIndex = array.length,
      randomIndex;

    // While there remain elements to shuffle.
    while (currentIndex != 0) {
      // Pick a remaining element.
      randomIndex = Math.floor(Math.random() * currentIndex);
      currentIndex--;

      // And swap it with the current element.
      [array[currentIndex], array[randomIndex]] = [
        array[randomIndex],
        array[currentIndex],
      ];
    }

    return array;
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
  <div class="grid">
    {#each shuffledIcons as icon}
      <Card {icon} />
    {/each}
  </div>
</main>

<style>
  .grid {
    width: 800px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    justify-items: center;
    align-items: center;
  }
</style>
