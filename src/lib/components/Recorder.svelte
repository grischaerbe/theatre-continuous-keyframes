<script lang="ts">
	import type { ISheet } from '@theatre/core'
	import { T, useFrame } from '@threlte/core'
	import { useStudio } from '@threlte/theatre'

	export let sheet: ISheet

	let position = {
		x: 0,
		y: 0,
		z: 0
	}

	let quaternion = {
		x: 0,
		y: 0,
		z: 0,
		w: 0
	}

	const sheetObject = sheet.object(
		'Recorder',
		{
			position,
			quaternion
		},
		{
			reconfigure: true
		}
	)

	const studio = useStudio()
	const runTransaction = () => {
		if (!$studio) return

		$studio.transaction(({ set }) => {
			set(sheetObject.props.position.x, position.x)
			set(sheetObject.props.position.y, position.y)
			set(sheetObject.props.position.z, position.z)
			set(sheetObject.props.quaternion.x, quaternion.x)
			set(sheetObject.props.quaternion.y, quaternion.y)
			set(sheetObject.props.quaternion.z, quaternion.z)
			set(sheetObject.props.quaternion.w, quaternion.w)
		})
	}

	let record = false

	const advanceStudioSequence = (delta: number) => {
		sheet.sequence.position += delta
	}

	useFrame((_, delta) => {
		// Update position and quaternion with random sin values
		position.x = Math.sin(Date.now() / 1000)
		position.y = Math.sin(Date.now() / 1000)
		position.z = Math.sin(Date.now() / 1000)

		quaternion.x = Math.sin(Date.now() / 1000)
		quaternion.y = Math.sin(Date.now() / 1000)
		quaternion.z = Math.sin(Date.now() / 1000)
		quaternion.w = Math.sin(Date.now() / 1000)

		if (record) {
			runTransaction()
			advanceStudioSequence(delta)
		}
	})
</script>

<svelte:window
	on:keypress={(e) => {
		if (e.key === 'r') {
			record = !record
		}
	}}
/>

<T.Group
	position.x={position.x}
	position.y={position.y}
	position.z={position.z}
	quaternion.x={quaternion.x}
	quaternion.y={quaternion.y}
	quaternion.z={quaternion.z}
	quaternion.w={quaternion.w}
>
	<slot />
</T.Group>
