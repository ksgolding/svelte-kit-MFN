<script context="module" lang="ts">
	export const prerender = true;
</script>

<script lang="ts">
	import Counter from '$lib/Counter.svelte';
	import Map from '$lib/Map.svelte';
	let olmap: any = undefined;
</script>

<svelte:head>
	<title>Home</title>
</svelte:head>

<section>
	<div class='main-container'>
		<Map on:message={(m) => {olmap = m.detail.map; console.log('map = ', olmap)}}></Map>
	</div>

</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 1;
	}

	h1 {
		width: 100%;
	}

	.welcome {
		position: relative;
		width: 100%;
		height: 0;
		padding: 0 0 calc(100% * 495 / 2048) 0;
	}

	.welcome img {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		display: block;
	}

.main-container {
	flex: 1;
	display: flex;
	flex-direction: column;
	height: 100%;
	width: 100%;
}
</style>
