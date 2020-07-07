<script>
  import InsertionSortVisualizer from "./InsertionSortVisualizer/InsertionSortVisualizer.svelte";
  import { insertionSort } from "./algorithms.js";

  import { onMount } from "svelte";
  let unsortedArray = [];
  let min = 1;
  let max = 233;

  let resetUnsortedArray = () => {
    let newArr = [];
    for (let index = min; index < max; index++) {
      newArr.push(getRandomArbitrary(min, max));
    }
    unsortedArray = newArr;
  };

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
        await pause(5);
        unsortedArray[j + 1] = unsortedArray[j];
        j = j - 1;
      }
      await pause(5);
      unsortedArray[j + 1] = key;
    }
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
    display: flex;
    justify-content: center;
    align-items: center;
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
  <InsertionSortVisualizer {unsortedArray} />
  <div class="actions">
    <div class="buttons">
      <button on:click={resetUnsortedArray}>Randomize Elements</button>
      <button on:click={run}>Insertion Sort</button>
    </div>
  </div>
</main>
