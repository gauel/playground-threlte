<script>
	import { Canvas } from '@threlte/core'
	import Scene from '$lib/components/Scene.svelte'
	import { state } from '$lib/js/store';
	import { timeline } from "motion";

	const hideUI = () => {
		$state.controlsVisible = false;
	}

</script>
<button class="w-full h-full min-h-screen relative {$state.controls ? "cursor-grab active:cursor-grabbing" : "cursor-not-allowed"}" disabled={!$state.controls} on:mousedown={$state.controls && hideUI} on:touchstart={$state.controls && hideUI}>
	<Canvas>
		<Scene />
	</Canvas>
</button>