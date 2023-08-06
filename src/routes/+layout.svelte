<script lang="ts">
	import Header from './header.svelte'
	// import "@fontsource/nunito";
</script>

<div class="container">
	<Header />
	<main>
		<slot />
	</main>
</div>

<style>
	:root {
		--main-color-dark: #10021c;
		--main-color-light: #ccbad5;
		--secondary-color-dark: #1e0a2d;
		--secondary-color-light: #ca99ff;
		--main-font-family: 'nunito', Verdana, sans-serif;
	}

	:global(body) {
		font-family: var(--main-font-family);
		overflow-y: scroll;
		margin: 0;
  		padding: 0;
	}

	.container {
		margin: 0;
  		padding: 0;
		color: var(--main-color-light);
		font-family: var(--main-font-family);
	}
</style>
