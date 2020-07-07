<script>
  export let unsortedArray;
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
    background-color: rgb(48, 148, 151);
    margin: 0 1px;
  }
</style>

<main>

  <div class="bars">
    {#each unsortedArray as item, i}
      <div class="bar" style="width: 4px; height: {item * 3}px" />
    {/each}
  </div>

</main>
