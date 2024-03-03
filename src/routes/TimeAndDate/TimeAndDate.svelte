<script>
	import { onMount, onDestroy } from 'svelte';

	let time = new Date();

	$: dynamicTime = time.toLocaleString();

	const updateDateTime = () => {
		time = new Date();
		dynamicTime = time.toLocaleString();
	};

	const interval = setInterval(updateDateTime, 1000);

	onMount(() => {
		interval;
	});

	onDestroy(() => {
		clearInterval(interval);
	});
</script>

<div>
	<h1 class="opacity-50 font-mono text-center px-8  mb-3 text-sm md:text-base text-slate-700 dark:text-slate-400">
		{dynamicTime}
	</h1>
</div>

<style>
</style>
