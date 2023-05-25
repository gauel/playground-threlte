<script>
	import { T } from '@threlte/core'
	import { HTML, OrbitControls } from '@threlte/extras'
	
	import Mars from '$lib/components/Mars.svelte';

	let mars;
</script>

<T.DirectionalLight
	intensity={1}
	position.x={80}
	position.y={80}
	position.z={20}
/>

<T.PerspectiveCamera
	makeDefault
	position.y={0}
	position.z={16}
>
  <OrbitControls
	enableZoom={true}
	enableDamping 
  />
</T.PerspectiveCamera>

<T.AmbientLight intensity={.05} />

<Mars rotation.y={90} ref={mars} />

<T.Mesh position.y={0.5}>
	<HTML
	    position.y={1.5}
	    position.z={0}
	    transform
		occlude={mars}
	  >
	  <div class="flex flex-col items-center">
	    <button class="bg-white/10 rounded-full px-3 h-8 border border-white/30 text-white hover:opacity-90 active:opacity-70 text-xs hover:bg-orange-500 transition-colors duration-300">
			
			Marz
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
