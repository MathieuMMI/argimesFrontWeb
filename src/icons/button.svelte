<script>
import Circle from './circle.svelte'
let myColor = 'black';
function changeColor() {
    if (myColor === 'purple')
        myColor = 'black'; 
    else
        myColor = 'purple'
}
</script>

<div class="flex justify-center items-center">
  <button on:click={changeColor} class="bg-white hover:bg-gray-100 text-black font-bold py-2 px-4 rounded-lg shadow-lg md:py-3 md:px-6 lg:text-xl lg:py-4 lg:px-8 flex items-center">
    <span class="mr-2">Je veux en savoir plus</span>
    <Circle fillColor={myColor} />
  </button>
</div>


