<script>
	import { onMount } from 'svelte';
	import { toggle_class } from 'svelte/internal';
	import Toggle from '../lib/toggle.svelte';

	let toggles = [];

function getRandom() {
  return Math.floor(Math.random() * 2);
}

	onMount(() => {
		for (let i = 0; i < 10; i++) {
			toggles = [
				...toggles,
				{
					id: 'toggle-' + i,
					value: getRandom()
				}
			];
		}
	});

	const handleOn = (event) => {
		if (event.detail.value) {
			status = 'on';
		} else status = 'off';
	};
</script>

{#each toggles as t}
    <div style="margin-bottom: 5px;">
        <Toggle id={t.id} value={t.value} on:state={handleOn} />
    </div>
{/each}
