<script>
	import { onMount } from 'svelte';
	import * as THREE from 'three';

	// Sizing parameters
	export let width;
	export let height;

	// // Observer parameters
	// export let observerDistance;
	// export let observerOrbitalPeriod;

	// // Observee parameters
	// export let observeeDistance;
	// export let observeeOrbitalPeriod;
	// export let observeeSTLFile;

	let canvasElement;

	onMount(() => {
		///////////////////////////////////////////////////////////////////////////////////////
		// THREE.js Setup
		///////////////////////////////////////////////////////////////////////////////////////
		// Create the renderer
		// and append it to the page
		const renderer = new THREE.WebGLRenderer({ antialias: true, canvas: canvasElement });
		renderer.setSize(width, height);

		// Create scene, camera, and light
		const scene = new THREE.Scene();
		const light = new THREE.PointLight(0xffffff, 1, Infinity);
		const camera = new THREE.PerspectiveCamera(75, width / height, 1, 1000);
		camera.position.z = 75;
		camera.add(light); // Add light to camera
		scene.add(camera); // Add camera to scene

		///////////////////////////////////////////////////////////////////////////////////////
		// Object Creation
		///////////////////////////////////////////////////////////////////////////////////////
		// Sun
		const sun = new THREE.Mesh(
			new THREE.SphereGeometry(),
			new THREE.MeshPhongMaterial({ color: 0xc29e00 })
		);
		sun.scale.x = 10;
		sun.scale.y = 10;
		sun.scale.z = 10;
		scene.add(sun); // Add Sun to scene

		// observer
		const observer = new THREE.Mesh(
			new THREE.SphereGeometry(),
			new THREE.MeshPhongMaterial({ color: 0x0000ff })
		);
		observer.position.x = 30;
		observer.position.y = 30;
		observer.scale.x = 1;
		observer.scale.y = 1;
		observer.scale.z = 1;
		scene.add(observer); // Add observer to scene

		// observee
		const observee = new THREE.Mesh(
			new THREE.SphereGeometry(),
			new THREE.MeshPhongMaterial({ color: 0x777777 })
		);
		observee.position.x = -50;
		observee.position.y = 50;
		observee.scale.x = 1;
		observee.scale.y = 1;
		observee.scale.z = 1;
		scene.add(observee); // Add observee to scene

		///////////////////////////////////////////////////////////////////////////////////////
		// Animation Loop
		///////////////////////////////////////////////////////////////////////////////////////
		function animate() {
			requestAnimationFrame(animate);

			// Logic goes here

			// Render the scene
			renderer.render(scene, camera);
		}
		animate();
	});
</script>

<canvas bind:this={canvasElement} />
