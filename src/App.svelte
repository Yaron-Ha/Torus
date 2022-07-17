<script lang="ts">
	import * as THREE from 'three'
	import * as SC from 'svelte-cubed'

	// torus data
	let thickness = 0.5
	let radius = 5
	let isPaused = true
	let spin = 0

	SC.onFrame(() => {
		// animate spin
		if (!isPaused) spin += 0.01
	})
</script>

<main>
	​<SC.Canvas antialias background={new THREE.Color(0x080808)}>
		<SC.Mesh
			geometry={new THREE.TorusGeometry(radius, thickness, 32, 100)}
			rotation={[0 + spin, 7 + spin, 0 + spin]}
			material={new THREE.MeshBasicMaterial({ color: 0xfcfcfc })}
		/>
		<SC.PerspectiveCamera position={[25, 0, 25]} />
		<SC.OrbitControls enableZoom={false} />
		​</SC.Canvas
	>
</main>

<div class="controls">
	<label><input type="range" bind:value={thickness} min={0} max={3} step={0.01} /> thickness</label>
	<label><input type="range" bind:value={radius} min={0} max={10} step={0.1} /> radius</label>
	<label><input type="checkbox" bind:checked={isPaused} selected /> pause</label>
</div>

<style>
	.controls {
		/* position */
		position: absolute;
		left: 1em;
		top: 1em;
		/* make it flex */
		display: flex;
		flex-direction: column;
	}
</style>
