<script>
	import { tweened } from 'svelte/motion';
	import { cubicOut } from 'svelte/easing';

	let value = false;

	const switchPosition = tweened(0, {
		duration: 200,
		easing: cubicOut
	});

	function handleClick() {
		value = !value;
		if (value) switchPosition.set(20);
		else switchPosition.set(0);
	}
</script>

<div class="toggle_outer" class:on={value} on:click={handleClick}>
	<div class="toggle_knob" style="left:{$switchPosition}px">&nbsp;</div>
</div>

<style>
	.toggle_outer {
		background-color: white;
		width: 40px;
		height: 20px;
		position: relative;
		border-radius: 20px;
		border: solid 1px black;
		user-select: none;
		transition: all 200ms;
	}

	.on {
		background-color: rgb(70, 255, 70);
	}

	.toggle_knob {
		background-color: black;
		width: 20px;
		height: 20px;
		border-radius: 50%;
		position: absolute;
		user-select: none;
	}
</style>
