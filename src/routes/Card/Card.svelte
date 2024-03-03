<script>
	let timeMinutes = 25;
	let timeSeconds = 0;

	let breakMinutes = 5;
	let breakSeconds = 0;

	let iterations = 0;

	let startTimer = false;

    function incrementTimeMin() {
        timeMinutes++;
    }


    function decrementTimeMin() {
        if(timeMinutes > 0){
            timeMinutes--
        }
    }
    function incrementTimeSec() {
        if(timeSeconds < 59){
            timeSeconds++
        }
        else{
            timeSeconds = 0
        }
    }

    function decrementTimeSec() {
        if(timeSeconds > 0){
            timeSeconds--
        }
    }


    function incrementBreakMin() {
        breakMinutes++
    }

    function decrementBreakMin() {
        if(breakMinutes > 0){
            breakMinutes--
        }
    }
    function incrementBreakSec() {
        if(breakSeconds < 59){
            breakSeconds++
        }
        else{
            breakSeconds = 0
        }
    }

    function decrementBreakSec() {
        if(breakSeconds > 0){
            breakSeconds--
        }
    }

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

<div>
<div class="container max-w-[19rem] md:max-w-[36rem] ml-auto mr-auto p-10 rounded-xl shadow-lg bg-slate-200 dark:bg-[#2f3644]">
	<div class="time flex justify-left gap-2 mb-5">
		<p class="text-xl md:text-2xl text-slate-600 dark:text-[#a6adbb]">Time -</p>
		<div class="timeMinContainer flex">
			<button on:click={decrementTimeMin}> <i class="ri-subtract-line text-slate-600 dark:text-[#a6adbb]"></i> </button>
			<p class="text-xl md:text-2xl font-mono text-slate-600 dark:text-[#a6adbb]">{TimeMinutes}</p>
			<button on:click={incrementTimeMin}> <i class="ri-add-line text-slate-600 dark:text-[#a6adbb]"></i> </button>
		</div>
		<p class="semicolon text-xl md:text-2xl text-slate-600 dark:text-[#a6adbb]">:</p>
		<div class="timeSecContainer flex">
            <button on:click={decrementTimeSec}> <i class="ri-subtract-line text-slate-600 dark:text-[#a6adbb]"></i> </button>
			<p class="text-xl md:text-2xl font-mono text-slate-600 dark:text-[#a6adbb]">{TimeSeconds}</p>
            <button on:click={incrementTimeSec}> <i class="ri-add-line text-slate-600 dark:text-[#a6adbb]"></i> </button>
		</div>

		<!-- <progress id="time-progress" class="progress w-56" value="70" max="100"></progress> -->
	</div>

	<div class="break flex justify-left gap-2 mb-5">
		<p class="text-xl md:text-2xl text-slate-600 dark:text-[#a6adbb]">Break -</p>

        <div class="breakMinContainer flex">
            <button on:click={decrementBreakMin}> <i class="ri-subtract-line text-slate-600 dark:text-[#a6adbb]"></i> </button>
            <p class="text-xl md:text-2xl font-mono text-slate-600 dark:text-[#a6adbb]">{BreakMinutes}</p>
            <button on:click={incrementBreakMin}> <i class="ri-add-line text-slate-600 dark:text-[#a6adbb]"></i> </button>
        </div>
		<p class="semicolon text-xl md:text-2xl text-slate-600 dark:text-[#a6adbb]">:</p>

        <div class="breakSecContainer flex">
            <button on:click={decrementBreakSec}> <i class="ri-subtract-line text-slate-600 dark:text-[#a6adbb]"></i> </button>
            <p class="text-xl md:text-2xl font-mono text-slate-600 dark:text-[#a6adbb]">{BreakSeconds}</p>
            <button on:click={incrementBreakSec}> <i class="ri-add-line text-slate-600 dark:text-[#a6adbb]"></i> </button>
        </div>
		<!-- 
		<progress id="break-progress" class="progress w-56" value="70" max="100"></progress> -->
	</div>

	<div class="iterations flex justify-left gap-2 mb-8">
		<p class="text-xl md:text-2xl text-slate-600 dark:text-[#a6adbb]">Iterations -</p>
		<p class="text-xl md:text-2xl font-mono text-slate-600 dark:text-[#a6adbb]">{iterations}</p>
	</div>

	<div class="flex gap-3">
		<button on:click={startTimerHandler} class="btn btn-outline text-slate-600 dark:text-[#a6adbb] dark:hover:bg-slate-600">Start</button>
		<button on:click={pauseHandler} class="btn btn-outline text-slate-600 dark:text-[#a6adbb] dark:hover:bg-slate-600">Pause</button>
		<button on:click={resetHandler} class="btn btn-outline text-slate-600 dark:text-[#a6adbb] dark:hover:bg-slate-600">Reset</button>
	</div>
</div>
</div>



<style>
	@import url('https://fonts.googleapis.com/css2?family=Pixelify+Sans:wght@400;500;600;700&display=swap');

	@property --gradient-angle {
		syntax: '<angle>';
		initial-value: 0deg;
		inherits: false;
	}

	:root {
		--clr-1: #5fbdd4;
		--clr-2: #1d87e4;
		--clr-3: #5e07ea;
		--clr-4: ;
	}

	.container {
		/* max-width: 600px; */
		/* background: #2f3644; */
		position: relative;
		font-family: 'Pixelify sans';
	}

	.container::before,
	.container::after {
		content: '';
		position: absolute;
		inset: -0.1rem;
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
		filter: blur(6rem);
	}

	@keyframes rotation {
		0% {
			--gradient-angle: 0deg;
		}
		100% {
			--gradient-angle: 360deg;
		}
	}

	.time,
	.break,
	.iterations {
		align-items: center;
		/* justify-content: space-around; */
	}

	.timeMinContainer,
	.timeSecContainer,
    .breakMinContainer,
    .breakSecContainer {
		align-items: center;
	}
</style>
