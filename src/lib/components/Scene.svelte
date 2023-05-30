<script>
	import { T, useFrame } from '@threlte/core'
	import { HTML, OrbitControls } from '@threlte/extras'
	import { onMount } from 'svelte';
	import { tweened } from 'svelte/motion';
	import { cubicInOut } from 'svelte/easing';

	const cameraZoom = tweened(24, {
		duration: 6000,
		easing: cubicInOut
	})

	const directionalLightIntensity = tweened(0, {
		duration: 6000,
		easing: cubicInOut
	})

	const ambientLightIntensity = tweened(0, {
		duration: 6000,
		easing: cubicInOut
	})
	
	import Mars from '$lib/components/Mars.svelte';


	let mars;
	console.log("mars", mars);;
	let rotation = 0;

	useFrame(() => {
        rotation += 0.002;
    });

	onMount(() => {
		setTimeout(() => {
			$cameraZoom = 12
			$directionalLightIntensity = 1;
			$ambientLightIntensity = 0.05;
		}, 2000)
	})


</script>

<T.DirectionalLight
	intensity={$directionalLightIntensity}
	position.x={80}
	position.y={80}
	position.z={20}
/>

<T.PerspectiveCamera
	makeDefault
	position.y={0}
	position.z={$cameraZoom}
>
  <OrbitControls
	enableZoom={true}
	enableDamping 
  />
</T.PerspectiveCamera>

<T.AmbientLight intensity={$ambientLightIntensity} />

<Mars rotation.z={-180} rotation.y={rotation} ref={mars} />

<T.Mesh position.y={0.5}>
	<HTML
	    position.y={1.5}
	    position.z={0}
	    transform
	  >
	  <div class="flex flex-col items-center">
	    <button class="bg-white/10 px-3 h-8 rounded-full w-auto border flex items-center gap-2 border-white/30 text-white hover:opacity-90 active:opacity-70 text-xs hover:bg-orange-500 hover:border-orange-300 transition-colors duration-300 group">
			<div class="w-2 h-2 rounded-full bg-orange-500 transition-color duration-300 group-hover:bg-white"/>
			<div>Mars</div>
		</button>
		<div class="w-px h-10 bg-white/30"></div>
	  </div>
  </HTML>
</T.Mesh>
<!--
	<Grid
		position.y={0}
		cellColor="#fff"
		sectionColor="blue"
		sectionThickness={1}
		castShadow
		fadeDistance={30}
		cellSize={.5}
	/>
-->
