<script>
	import { tweened } from 'svelte/motion';
	import { cubicOut } from 'svelte/easing';
	import { createEventDispatcher } from 'svelte';

	export let value = false;
	export let id = '';

	const dispatch = createEventDispatcher();

	const switchPosition = tweened(0, {
		duration: 200,
		easing: cubicOut
	});

	$: if (value) {
		switchPosition.set(20);
		dispatch('state', {id, value:true});
	} else {
		switchPosition.set(0);
		dispatch('state', {id, value:false});
	}

	function handleClick() {
		value = !value;
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
        display: inline-block;
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
