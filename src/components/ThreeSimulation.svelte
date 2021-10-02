<script>
	import { onMount } from 'svelte';
	import * as THREE from 'three';

	let ll = 69;

	export let color;

	export let width;
	export let height;

	onMount(() => {
		// Create the renderer
		// and append it to the page
		const renderer = new THREE.WebGLRenderer();
		renderer.setSize(width, height);
		document.body.appendChild(renderer.domElement);

		// Create scene, camera, and light
		const scene = new THREE.Scene();
		const camera = new THREE.PerspectiveCamera(75, width / height, 0.1, 1000);
		camera.position.z = 5;
		camera.add(new THREE.PointLight(0xffffff, 1, Infinity)); // Add light to camera
		scene.add(camera); // Add camera to scene

		// Create the cube's geometry
		const geometry = new THREE.BoxGeometry();
		// Create the cube's material
		var material = new THREE.MeshPhongMaterial({ color: color });
		// Create the cube's mesh
		const cube = new THREE.Mesh(geometry, material);
		scene.add(cube); // Add cube to scene

		// The animation loop
		function animate() {
			requestAnimationFrame(animate);

			// Logic goes here
			cube.rotation.x += 0.01;
			cube.rotation.y += 0.01;

			// Render the scene
			renderer.render(scene, camera);
		}
		animate();
	});
</script>

<h1>Light Level: {ll}</h1>
