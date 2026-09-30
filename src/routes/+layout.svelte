<body class="min-h-screen bg-gradient-to-b from-gray-50 to-blue-100">
	<nav class="flex justify-center w-full">
		<a class="mx-4 text-lg" href="/">Home</a>
		<a class="mx-4 text-lg" href="/about">About</a>
	</nav>

	<slot />
</body>

<style>
	@tailwind base;
	@tailwind components;
	@tailwind utilities;
</style>
