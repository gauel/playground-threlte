<script>
	import { Canvas } from '@threlte/core'
	import Scene from '$lib/components/Scene.svelte'
	import { state } from '$lib/js/store';

</script>
<div class="w-full h-full min-h-screen relative {$state.controls ? "cursor-grab" : "cursor-not-allowed"}">
	<Canvas>
		<Scene />
	</Canvas>
</div>