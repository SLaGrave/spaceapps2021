<script>
	import { onMount } from 'svelte';
	import * as THREE from 'three';

	// Sizing parameters
	export let width = 500;
	export let height = 500;

	// // Observer parameters
	// export let observerDistance;
	// export let observerOrbitalPeriod;

	// // Observee parameters
	// export let observeeDistance;
	// export let observeeOrbitalPeriod;
	// export let observeeSTLFile;
	// export let observeeSize;

	///////////////////////////////////////////////////////////////////////////////////////
	// Visualizer control variables
	///////////////////////////////////////////////////////////////////////////////////////
	// Observer
	let thetaObserver = 0;
	let deltaThetaObserver = 0.01; // Positive value = counter clockwise
	let observerScale = 30;

	// Observee
	let thetaObservee = 0;
	let deltaThetaObservee = 0.05; // Positive value = counter clockwise
	let observeeScale = 50;

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

		// Observer
		const observer = new THREE.Mesh(
			new THREE.SphereGeometry(),
			new THREE.MeshPhongMaterial({ color: 0x0000ff })
		);
		observer.scale.x = 1;
		observer.scale.y = 1;
		observer.scale.z = 1;
		scene.add(observer); // Add observer to scene

		// Observee
		const observee = new THREE.Mesh(
			new THREE.BoxGeometry(),
			new THREE.MeshPhongMaterial({ color: 0x777777 })
		);
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
			thetaObserver += deltaThetaObserver;
			observer.position.x = observerScale * Math.cos(thetaObserver);
			observer.position.y = observerScale * Math.sin(thetaObserver);

			thetaObservee += deltaThetaObservee;
			observee.position.x = observeeScale * Math.cos(thetaObservee);
			observee.position.y = observeeScale * Math.sin(thetaObservee);

			// Render the scene
			renderer.render(scene, camera);
		}
		animate();
	});
</script>

Position(s) of the observer and observee
<br />
<canvas bind:this={canvasElement} />
