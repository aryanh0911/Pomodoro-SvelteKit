<script>
	import Card from './Card/Card.svelte';
	import TimeAndDate from './TimeAndDate/TimeAndDate.svelte';
	export let darkMode;

	$: darkMode = 'false';

	const toggleTheme = () => {
		darkMode = !darkMode
	}
</script>

<div class={darkMode ? "dark" : ""}>
	<div class="min-h-[100dvh] flex flex-col justify-center align-middle bg-slate-300 dark:bg-transparent">
		<TimeAndDate />
		<Card />

		<button id="themeBtn" class="rounded-full w-14 h-14 bg-slate-700 dark:bg-slate-500 dark:text-slate-950 absolute top-8 right-8 md:top-16 md:right-16 hover:scale-105 transition duration-150" on:click={toggleTheme}>
			{darkMode ? 'Light' : 'Dark'}
		</button>
	</div>
</div>

<style>
</style>
