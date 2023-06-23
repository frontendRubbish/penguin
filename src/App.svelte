<script lang="ts">
	import {onMount, tick} from 'svelte';
  import Confetti from './components/Confetti.svelte';
  import Grid from './components/Grid.svelte'
  import Penguin from './components/Penguin.svelte'

  import { activeCol, activeRow, numberCols, numberRows, solved } from './stores.js';

let solution = '';
let solutionInput: HTMLInputElement;
let penguinComponent: Penguin;

$: allDone = $solved.filter( row => (row.filter( col => !col).length > 0 )).length === 0;

function getNewNumbers() {
  let newRow: number;
  let newCol: number;

  do {
    newRow = Math.floor(Math.random() * 10);
    newCol = Math.floor(Math.random() * 10);
  } while ($solved[newRow][newCol]);

  activeRow.set(newRow);
  activeCol.set(newCol);
}

function resetSolved() {
  solved.set( $solved.map( row => row.map( col => false)));
}

function startMixed() {
  console.log('startMixed');
}

async function startAll() {
  resetSolved();
  getNewNumbers();
  await tick();
  solutionInput.focus();
}

function checkCommit(e:KeyboardEvent) {
  console.log(e.code);
  if (e.code === 'Enter' || e.code === 'NumpadEnter') {
    checkSolution();
  }  
}

async function checkSolution() {
  const rightAnswer = $numberCols[$activeCol] * $numberRows[$activeRow] === parseInt(solution);
  if (rightAnswer) {
    solved.set( $solved.map( (row, rowIndex) => {
      return (rowIndex === $activeRow) ? row.map( ( col, colIndex) => colIndex === $activeCol ? true : col) : row;
    }));

    penguinComponent.startRight();

    solution = '';

    await tick();

    if (!allDone) {
      getNewNumbers();
    } 
    solutionInput.focus();
  } else {
    penguinComponent.startWrong();
  }
}

</script>

<h1 class="text-3xl font-bold underline mb-4 text-center">Wir üben das kleine Ein mal Eins!</h1>
{#if allDone}
  <Confetti />
{/if}
<div class="flex">

  <div class="flex w-1/2 justify-center">
    <Grid></Grid>
  </div>
  <div class="flex w-1/2 justify-center items-end">
    <div class="w-1/2">
      {#if $activeRow > -1 && $activeCol > -1}
        <div class="flex mb-4">
          <span class="text-4xl">
            {$numberRows[$activeRow]} x {$numberCols[$activeCol]} = 
          </span>
          <input bind:value={solution} bind:this={solutionInput} on:keydown={checkCommit} type="number" class="border border-blue-500 h-10 w-16 rounded text-3xl p-2 mx-2 text-right" maxlength="2"/>
          <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" on:click="{checkSolution}">
            ✓
          </button>
        </div>
      {/if}
      <Penguin bind:this={penguinComponent} />
    </div>
  </div>

</div>


<div class="flex w-1/2 justify-between">
  <button on:click={startMixed} class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
    Aufgaben gemischt
  </button>

  <button on:click={startAll} class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
    Aufgaben normal
  </button>
</div>
