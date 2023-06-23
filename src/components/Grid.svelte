<script>
import { numberRows, numberCols, activeRow, activeCol, solved } from '../stores.js';
</script>


<div class="mb-2">
  <div class="flex">
    <div class="w-14 h-14 p-2 flex items-center justify-center"></div> 
    {#each $numberCols as col, colIndex}
      <div class="w-14 h-14 p-2 flex items-center justify-center" class:bg-blue-100={colIndex === $activeCol}>{col}</div> 
    {/each}
  </div>
  {#each $numberRows as row, rowIndex}
    <div class="flex">
      <div class="w-14 h-14 p-2 flex items-center justify-center"  class:bg-blue-100={rowIndex === $activeRow}>{row}</div> 
      {#each $numberCols as col, colIndex}
        <div class="w-14 h-14 p-2" class:bg-blue-100={colIndex === $activeCol || rowIndex === $activeRow}>
          {#if $solved[rowIndex][colIndex]}
            <div class="rounded-full h-full bg-blue-500 text-white flex items-center justify-center" class:bg-blue-700={colIndex === $activeCol && rowIndex === $activeRow}>
              {row * col}
            </div>
          {:else}
            <div class="rounded-full h-full text-white flex items-center justify-center" class:bg-blue-700={colIndex === $activeCol && rowIndex === $activeRow}>
              { colIndex === $activeCol && rowIndex === $activeRow ? '?' : '' }
            </div>
          {/if}
        </div> 
      {/each}
    </div>
  {/each}
</div>