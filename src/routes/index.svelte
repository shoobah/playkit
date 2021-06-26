<script>
	import { onMount } from 'svelte';
	import Toggle from '../lib/toggle.svelte';

	let toggles = [];

	function getRandom() {
		return !!Math.floor(Math.random() * 2);
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

	function onStateChange(s){
		const t = toggles.find(i=>i.id===s.detail.id)
		t.value = s.detail.value;
		toggles=toggles;
	}
</script>

{#each toggles as t}
	<div style="padding:0; margin:0;">
		<div style="width:200px; display:inline-block">{t.id} - {t.value}:</div>
		<Toggle id={t.id} value={t.value} duration="200" on:state={onStateChange} />
	</div>
{/each}

<style>
	div {
		font-family: Arial, Helvetica, sans-serif;
	}
</style>
