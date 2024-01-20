<script>
    let timeMinutes = 25;
    let timeSeconds = 0;
  
    let breakMinutes = 5;
    let breakSeconds = 0;
  
    let iterations = 0;
  
    let startTimer = false;
  
    function startTimerHandler() {
      if (startTimer === false) {
        startTimer = setInterval(timer, 1000);
      } else {
        alert('Timer is already running');
      }
    }
  
    function resetHandler() {
      timeMinutes = 25;
      timeSeconds = 0;
  
      breakMinutes = 5;
      breakSeconds = 0;
  
      iterations = 0;
  
      stopInterval();
      startTimer = false;
    }
  
    function pauseHandler() {
      stopInterval();
      startTimer = false;
    }
  
    function timer() {
      // Work Timer Countdown
      if (timeSeconds !== 0) {
        timeSeconds--;
      } else if (timeMinutes !== 0 && timeSeconds === 0) {
        timeSeconds = 59;
        timeMinutes--;
      }
  
      // Break Timer Countdown
      if (timeMinutes === 0 && timeSeconds === 0) {
        if (breakSeconds !== 0) {
          breakSeconds--;
        } else if (breakMinutes !== 0 && breakSeconds === 0) {
          breakSeconds = 59;
          breakMinutes--;
        }
      }
  
      // Iteration is incremented by 1
      if (timeMinutes === 0 && timeSeconds === 0 && breakMinutes === 0 && breakSeconds === 0) {
        timeMinutes = 25;
        timeSeconds = 0;
  
        breakMinutes = 5;
        breakSeconds = 0;
  
        iterations++;
      }
    }
  
    function stopInterval() {
      clearInterval(startTimer);
    }
  
    $: TimeMinutes = timeMinutes;
    $: TimeSeconds = timeSeconds;
    $: BreakMinutes = breakMinutes;
    $: BreakSeconds = breakSeconds;
  </script>
  
  <div class="container max-w-2xl ml-auto mr-auto mt-60 p-10 rounded-xl shadow-lg">
    <div class="time flex justify-left gap-5 mb-5">
      <p class="text-2xl">Time -</p>
      <p class="text-2xl">{TimeMinutes}</p>
      <p class="semicolon text-2xl">:</p>
      <p class="text-2xl">{TimeSeconds}</p>
    </div>
  
    <div class="break flex justify-left gap-5 mb-5">
      <p class="text-2xl">Break -</p>
      <p class="text-2xl">{BreakMinutes}</p>
      <p class="semicolon text-2xl">:</p>
      <p class="text-2xl">{BreakSeconds}</p>
    </div>
  
    <div class="iterations flex justify-left gap-5 mb-8">
      <p class="text-2xl">Iterations -</p>
      <p class="text-2xl">{iterations}</p>
    </div>
  
    <div class="flex gap-3">
      <button on:click={startTimerHandler} class="btn btn-outline">Start</button>
      <button on:click={pauseHandler} class="btn btn-outline">Pause</button>
      <button on:click={resetHandler} class="btn btn-outline">Reset</button>
    </div>
  </div>



  <style>
	.container {
		/* max-width: 600px; */
		background: #2f364476;
	}
</style>

  