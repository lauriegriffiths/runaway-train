<script lang="ts">
	import { onMount, onDestroy } from 'svelte';

	let ROUND_TIME = 120;
	let timeLeft = ROUND_TIME;

	let intervalId: number;

	function startTimer() {
		intervalId = setInterval(() => {
			if (timeLeft > 0) {
				timeLeft--;
			} else {
				clearInterval(intervalId);
			}
		}, 1000);
	}

	function resetTimer() {
		timeLeft = ROUND_TIME;
		clearInterval(intervalId);
	}

	onMount(() => {
		//startTimer();
	});

	onDestroy(() => {
		clearInterval(intervalId);
	});
</script>

<div class="container">
	<div class="content">
		<div>
			{#if timeLeft > 0}
				<h1>{timeLeft}</h1>
			{:else}
				<h1>Time's up!</h1>
			{/if}
		</div>

		<div>
			<button on:click={startTimer}>Start</button>
			<button on:click={resetTimer}>Reset</button>
		</div>
	</div>
</div>

<style>
	.content {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		text-align: center;
	}
	h1 {
		border-radius: 20rem;
		background-color: rgba(140, 140, 140, 0.8);
		box-shadow: 0 0 20px 30px rgba(140, 140, 140, 0.8);
		font-family: monospace;
		font-size: 10rem;
	}
	button {
		display: inline-block;
		padding: 10px 20px;
		margin: 10px;
		border-radius: 20px;
		border: none;
		background-color: #caa069;
		color: #fff;
		font-family: 'Old Standard TT', serif;
		font-size: 1.2rem;
		text-shadow: 2px 2px 2px #000;
		box-shadow: inset 0 0 10px #000, 0 0 10px #000;
		background-size: 100% 100%;
	}

	button:hover {
		background-color: #fedfa9;
		color: #844b00;
		text-shadow: none;
	}
</style>
