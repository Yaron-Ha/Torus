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
	​<SC.Canvas antialias background={new THREE.Color('floralwhite')}>
		<SC.Mesh
			geometry={new THREE.TorusGeometry(radius, thickness, 32, 100)}
			rotation={[spin, spin, spin]}
			material={new THREE.MeshStandardMaterial({ color: 0x8b8b83 })}
		/>
		<SC.PerspectiveCamera position={[25, 1, 25]} />
		<SC.OrbitControls enableZoom={false} />
		​</SC.Canvas
	>
</main>

<div class="controls">
	<label><input type="range" bind:value={thickness} min={0.5} max={3} step={0.05} /> thickness</label>
	<label><input type="range" bind:value={radius} min={1} max={10} step={0.1} /> radius</label>
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
