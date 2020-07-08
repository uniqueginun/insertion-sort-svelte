<script>
  import InsertionSortVisualizer from "./InsertionSortVisualizer/InsertionSortVisualizer.svelte";
  import { insertionSort } from "./algorithms.js";

  import { onMount } from "svelte";
  let unsortedArray = [];
  let min = 1;
  let max = 233;
  let lastSortedIndex = 0;

  $: {
    resetUnsortedArray(max);
  }

  let resetUnsortedArray = (maxLen = max) => {
    let newArr = [];
    for (let index = min; index < maxLen; index++) {
      newArr.push(getRandomArbitrary(min, maxLen));
    }
    unsortedArray = newArr;
    lastSortedIndex = 0;
  };

  $: sortedSubArray = unsortedArray.slice(0, lastSortedIndex);

  function getRandomArbitrary(min, max) {
    return Math.random() * (max - min) + min;
  }

  function pause(ms) {
    return new Promise(res => setTimeout(res, ms));
  }

  const insertionSortAlgo = async () => {
    let length = unsortedArray.length;
    for (let i = 1; i < length; i++) {
      let key = unsortedArray[i];
      let j = i - 1;
      while (j >= 0 && unsortedArray[j] > key) {
        await pause(2);
        unsortedArray[j + 1] = unsortedArray[j];
        j = j - 1;
      }
      await pause(2);
      lastSortedIndex = i;
      unsortedArray[j + 1] = key;
    }
    lastSortedIndex = unsortedArray.length - 1;
  };

  function run() {
    insertionSortAlgo();
  }

  onMount(() => {
    resetUnsortedArray();
  });
</script>

<style>
  .actions {
    position: fixed;
    text-align: center;
    display: flex;
    flex-direction: column;
    align-items: center;
    top: 0;
  }
  .buttons {
    margin-top: 20px;
    display: flex;
    justify-content: space-around;
    align-items: center;
    width: 300px;
  }
</style>

<main>
  <InsertionSortVisualizer {unsortedArray} {sortedSubArray} />
  <div style="margin-top: {max * 3 + 50}px;" class="actions">
    <div class="buttons">
      <button on:click={resetUnsortedArray(max)}>Randomize Elements</button>
      <button on:click={run}>Run Insertion Sort</button>
    </div>
    <input
      style="width: 300px"
      type="range"
      bind:value={max}
      min="0"
      max="1000" />
    {max}
  </div>
</main>
