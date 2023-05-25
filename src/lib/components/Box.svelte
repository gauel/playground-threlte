<script>
	import { forwardEventHandlers, T } from '@threlte/core'
	import { useCursor } from '@threlte/extras'
	import { spring } from 'svelte/motion'
	import Mars from '$lib/components/Mars.svelte';
  
	let r = spring(240);
	let color = 'rgb(' + r + ',240,180)'
  
	const scale = spring(1)
	const component = forwardEventHandlers()
  
	const { onPointerEnter, onPointerLeave } = useCursor()
  </script>

  <Mars />
  