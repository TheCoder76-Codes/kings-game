<script>
  import './app.css'
  let players = 3;
  let inRound = false;
  let currentNumber = null;
  let playersArray = [];
  function startTheTapping() {
    if (players < 3 || !players || typeof players !== 'number') players = 3
    playersArray = Array.from({length: players - 1}).map((_,i) => i+1);
    playersArray.push('King!')
    playersArray = playersArray.sort(() => Math.random() - 0.5);
    inRound = true;
    currentNumber = '';
  }
  function nextItem() {
    if (!currentNumber) currentNumber = playersArray.shift()
    else if (currentNumber) {
      currentNumber = ''
      if (playersArray.length == 0) window.location.reload()
    }
  }
</script>

<main class="p-10 w-screen h-screen overflow-hidden">
  {#if !inRound}
    <h1 class="text-3xl font-semibold mb-2">Welcome!</h1>
    <p class="text-lg mb-2">Please select the number of players (min 3).</p>
    <input type="number" min="3" class="px-4 py-2 bg-slate-50 rounded-lg block" bind:value={players}>
    <button class="bg-blue-500 hover:bg-blue-600 px-4 py-2 rounded-lg text-white mt-2" on:click={startTheTapping}>Continue</button>
    <h2 class="text-xl font-medium mt-2">How it works</h2>
    <p class="text-base">Firstly, enter the number of players, then click 'Continue'.</p>
    <p class="text-base">Then, the screen will be blank. Tap the screen to reveal the first character's delegation, then tap it again to hide it. This is where you pass your device over to the next person, and continue around the circle. Tap the screen to reveal the next delegation, and continue until everyone is done.</p>
  {:else}
    <div class="w-full h-full grid place-content-center" on:click={nextItem}>
      <div>
        <h1 class="text-3xl font-medium">{currentNumber}</h1>
      </div>
    </div>
  {/if}
</main>