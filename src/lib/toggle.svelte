<script>
	import { tweened } from 'svelte/motion';
	import { cubicOut } from 'svelte/easing';
	import { createEventDispatcher } from 'svelte';

	export let value = false;
	export let id = '';
    export let size=20;
    export let onColor='#42d442'
    export let offColor='#ccc'
    export let multiplier=2;
    export let duration=100;

	const dispatch = createEventDispatcher();

	const switchPosition = tweened(1, {
		duration: duration,
		easing: cubicOut
	});

	$: if (value) {
		switchPosition.set(size*(multiplier-1));
		dispatch('state', {id, value:true});
	} else {
		switchPosition.set(3);
		dispatch('state', {id, value:false});
	}

	function handleClick() {
		value = !value;
	}
</script>

<div class="toggle_outer" class:on={value} on:click={handleClick} style="--size:{size + 'px'}; --onColor:{onColor}; --offColor:{offColor}; --multiplier:{multiplier}; --duration:{duration + 'ms'} ">
	<div class="toggle_knob" style="left:{$switchPosition}px">&nbsp;</div>
</div>

<style>
	.toggle_outer {
		background-color: var(--offColor);
		width: calc(var(--size)*var(--multiplier));
		height: var(--size);
		position: relative;
		border-radius: var(--size);
		/* border: solid 1px #000000; */
		user-select: none;
		transition: all var(--duration);
        display: inline-block;
	}

	.on {
		background-color: var(--onColor);
	}

	.toggle_knob {
		background-color: #333;
        top: 1px;
		width: calc(var(--size) - 3px);
		height: calc(var(--size) - 3px);
		border-radius: 50%;
		border: none;
		position: absolute;
		user-select: none;
	}
</style>
