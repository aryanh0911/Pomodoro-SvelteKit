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
  
  <div class="container max-w-[19rem] md:max-w-[36rem] ml-auto mr-auto p-10 rounded-xl shadow-lg">
    <div class="time flex justify-left gap-5 mb-5">
      <p class="text-xl md:text-2xl">Time -</p>
      <p class="text-xl md:text-2xl font-mono">{TimeMinutes}</p>
      <p class="semicolon text-xl md:text-2xl">:</p>
      <p class="text-xl md:text-2xl font-mono">{TimeSeconds}</p>
    </div>
  
    <div class="break flex justify-left gap-5 mb-5">
      <p class="text-xl md:text-2xl">Break -</p>
      <p class="text-xl md:text-2xl font-mono">{BreakMinutes}</p>
      <p class="semicolon text-xl md:text-2xl">:</p>
      <p class="text-xl md:text-2xl font-mono">{BreakSeconds}</p>
    </div>
  
    <div class="iterations flex justify-left gap-5 mb-8">
      <p class="text-xl md:text-2xl">Iterations -</p>
      <p class="text-xl md:text-2xl font-mono">{iterations}</p>
    </div>
  
    <div class="flex gap-3">
      <button on:click={startTimerHandler} class="btn btn-outline">Start</button>
      <button on:click={pauseHandler} class="btn btn-outline">Pause</button>
      <button on:click={resetHandler} class="btn btn-outline">Reset</button>
    </div>
  
  </div>



  <style>

    @property --gradient-angle {
        syntax: "<angle>";
            initial-value: 0deg;
            inherits: false
    }

    :root {
        --clr-1: #5fbdd4;
        --clr-2: #1d87e4;
        --clr-3: #5e07ea;
        --clr-4: ;
    }

	.container {
		/* max-width: 600px; */
		background: #2f3644;
        position: relative;
	}

    .container::before,
    .container::after {
        content: "";
        position: absolute;
        inset: -.1rem;
        z-index: -1;
        background: conic-gradient(
            from var(--gradient-angle),
            var(--clr-1),
            var(--clr-2),
            var(--clr-3),
            var(--clr-2),
            var(--clr-1)
            );
        border-radius: inherit;
        animation: rotation 8s linear infinite;
    }

    .container::after {
        filter: blur(6rem)
    }

    @keyframes rotation {
        0% { --gradient-angle: 0deg }
        100% { --gradient-angle: 360deg }
    }
</style>

  