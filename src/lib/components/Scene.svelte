<script>
	import { T, useFrame } from '@threlte/core'
	import { HTML, OrbitControls, Environment } from '@threlte/extras'
	import { onMount } from 'svelte';
	import { animate, timeline } from "motion";
	import { state } from '$lib/js/store';

	/* animate via svelte */
	import { tweened } from 'svelte/motion';
	import { cubicInOut, circOut } from 'svelte/easing';

	let mars, testing = 0, zoomDuration = 6000;

	const cameraZoom = tweened(24, {
		duration: zoomDuration,
		easing: $state.controls ? cubicInOut : circOut
	})

	const directionalLightIntensity = tweened(0, {
		duration: 6000,
		easing: cubicInOut
	})

	const ambientLightIntensity = tweened(0, {
		duration: 6000,
		delay: 1000,
		easing: cubicInOut
	})
	
	
	import Mars from '$lib/components/Mars.svelte';


	$state.controls = false;
	$state.controlsVisible = true;
	console.log("mars", mars);;
	let rotation = 0;

	useFrame(() => {
			rotation += 0.002;
	});

	const zoomToMars = () => {
		zoomDuration = 6000;
		$cameraZoom = 6;
	}

	onMount(() => {
		$cameraZoom = 12
		$directionalLightIntensity = 1;
		$ambientLightIntensity = 0.02;

		/*
		animate("#note-pointer", {opacity: [0, 1]}, { duration: 2, delay: 6 })
		animate("#note-track", {height: ["0rem", "2rem"]}, { duration: 2, delay: 6 })
		*/

		//animate((progress) => {testing = progress}, { duration: 2, delay: 6 })


		timeline([
			["#note-pointer", {opacity: [0, 1]}, { duration: 2, delay: 6 }],
			["#note-track", {height: ["0rem", "2rem"]}, { duration: 2, at: "-2"}]
		]).finished.then(() => {
			$state.controls = true;
		});
	})


</script>

<!--
<Environment
  path = '/'
  files='enviroment.jpg'
  isBackground={true}
  groundProjection={{ radius: 2000, height: 5, scale: {x: 100,y: 100,z: 100} }}
/>
-->

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
		enableDamping={true}
		enabled={$state.controls}
	/>
</T.PerspectiveCamera>

<T.AmbientLight intensity={$ambientLightIntensity} />

<Mars rotation.z={-180} rotation.y={rotation} ref={mars} />

<T.Mesh position.y={0}>
	<HTML
		position.y={2}
		position.z={0}
		transform
	>
		<div class="flex flex-col items-center" id="note-pointer">
			<button class="bg-white/10 px-3 h-8 rounded-full w-auto border flex items-center gap-2 border-white/30 text-white active:opacity-70 text-xs transition-colors duration-300 group {$state.controls ? "cursor-pointer hover:opacity-90 hover:bg-orange-500 hover:border-orange-300 " : "cursor-not-allowed"}" on:click={zoomToMars} disabled={!$state.controls}>
				<div class="w-2 h-2 rounded-full bg-orange-500 transition-color duration-300 {$state.controls && "group-hover:bg-white"}"/>
				<div>Mars</div>
			</button>
			<div class="w-px bg-white/30" id="note-track"></div>
		</div>
	</HTML>
	<HTML
		position.y={-2}
		position.z={0}
		transform
	>
		<div class="text-white/80 uppercase tracking-widest text-[6px] text-center transition-opacity duration-[1s] {($state.controls && $state.controlsVisible) ? "opacity-100" : "opacity-0"}" id="interact-note">You can now interact<br />with the planet.</div>
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
