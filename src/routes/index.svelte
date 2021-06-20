<script>
	import { onMount } from 'svelte';
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
</script>

{#each toggles as t}
    <div style="padding:0; margin:0;">
        <div style="width:100px; display:inline-block">{t.id}:</div> <Toggle id={t.id} value={t.value} duration="200" />
    </div>
{/each}

<style>
    div{
        font-family: Arial, Helvetica, sans-serif;
    }
</style>