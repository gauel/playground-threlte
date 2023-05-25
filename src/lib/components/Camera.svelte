<script>
	import { T, useThrelte } from '@threlte/core'
	import { OrbitControls } from '@threlte/extras'
	
	const { invalidate } = useThrelte()
  </script>
  
<T.PerspectiveCamera
  makeDefault
  fov={50}
>
  <OrbitControls
	enableZoom={true}
	autoRotate
	enableDamping 
  />
</T.PerspectiveCamera>