<script>
	import { T, useFrame, useTask } from '@threlte/core';
  import { interactivity } from '@threlte/extras'
  import { spring, tweened } from "svelte/motion";
  interactivity()
	let rotate = tweened(0)
	let posY = tweened(1);
	let posX = 0;
	let rotY = rotate;
	let rotZ = rotate;
	let rotX = rotate;
	let speed = 900
	/**
	 * @type {number}
	 */
	let handle;
	const tick = () => {
		posY.set(Math.sin(Date.now() / speed) * 0.05 + 1)
		// posX = Math.cos(Date.now() / 1500) * 0.025;
		rotY.set(Math.sin(Date.now() / speed + 200) * 0.1);
		rotX.set(Math.sin(Date.now() / speed) * 0.1);
		rotZ.set(Math.sin(Date.now() / speed) * 0.1);
		handle = window.requestAnimationFrame(tick);
	};
	tick();
</script>

  <T.Mesh position.y={$posY} position.x={posX} rotation.y={$rotY} rotation.x={$rotX} rotation.z={$rotZ}

  on:pointerenter={() =>
  {
	rotY.set(0);
	rotX.set(0);
	rotZ.set(0);
	posY.set(1);
	cancelAnimationFrame(handle);
}
  }

  on:pointerleave={() =>
  {
	tick();
  }
  }
  >
    <T.BoxGeometry />
    <T.MeshStandardMaterial color="#0059BA" />
  </T.Mesh>
<T.Group>
	<T.PerspectiveCamera
		makeDefault
		position={[-10, 1.5, 1]}
		fov={15}
		on:create={({ ref }) => {
			ref.lookAt(0, 1, 0);
		}}
	/>
</T.Group>

<T.DirectionalLight intensity={0.8} position.x={5} position.y={10} />
<T.AmbientLight intensity={0.2} />
