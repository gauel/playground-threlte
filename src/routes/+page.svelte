<script>
	import { Canvas } from '@threlte/core'
	import Scene from '$lib/components/Scene.svelte'
	import { state } from '$lib/js/store';
	import { timeline } from "motion";

	const hideUI = () => {
		timeline([
			["#note-pointer, #interact-note", {opacity: [null, 0]}, { duration: 0.5 }],
			["#note-track", {height: [null, "0rem"]}, { duration: 0.5, at: "<"}]
		])
	}

</script>
<button class="w-full h-full min-h-screen relative {$state.controls ? "cursor-grab active:cursor-grabbing" : "cursor-not-allowed"}" disabled={!$state.controls} on:mousedown={hideUI}>
	<Canvas>
		<Scene />
	</Canvas>
</button>