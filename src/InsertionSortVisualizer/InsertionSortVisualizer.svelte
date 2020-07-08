<script>
  export let unsortedArray;
  export let sortedSubArray;
  export let currentlyCompare;
</script>

<style>
  .bars {
    background-color: rgb(255, 255, 255);
    width: 100vw;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    height: 1000px;
  }
  .bar {
    background-color: #002fff;
    margin: 0 1px;
  }
</style>

<main>

  <div class="bars">
    {#each unsortedArray as item, i}
      <div
        class="bar"
        style="width: 4px; height: {item * 3}px; background-color: {currentlyCompare[0] === item ? '#002fff' : currentlyCompare[1] === item ? '#000' : sortedSubArray.includes(item) ? 'green' : 'red'}" />
    {/each}
  </div>

</main>
