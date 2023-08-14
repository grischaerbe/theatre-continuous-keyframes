<script lang="ts">
	import { T } from '@threlte/core';
	import { ContactShadows, Float, Grid, OrbitControls } from '@threlte/extras';
	import { Sheet } from '@threlte/theatre';
	import Recorder from './Recorder.svelte';
</script>

<Sheet let:sheet>
	<T.PerspectiveCamera makeDefault position={[-10, 10, 10]}>
		<OrbitControls />
	</T.PerspectiveCamera>

	<T.DirectionalLight intensity={0.8} position.x={5} position.y={10} />
	<T.AmbientLight intensity={0.2} />

	<Grid
		position.y={-0.001}
		cellColor="#ffffff"
		sectionColor="#ffffff"
		sectionThickness={0}
		fadeDistance={25}
		cellSize={2}
	/>

	<Recorder {sheet}>
		<T.Mesh position={[-1.4, 1.5, 0.75]} rotation={[-5, 128, 10]}>
			<T.IcosahedronGeometry />
			<T.MeshStandardMaterial color="#F8EBCE" />
		</T.Mesh>
	</Recorder>
</Sheet>
