<script lang="ts">
	import RatingSelector from '../lib/RatingSelector.svelte';
</script>

<h1>Rating Selector and Display for Svelte</h1>
<div class="wrapper">
	<h2>Features</h2>
	<ul>
		<li>Custom Theming</li>
		<li>Custom Icons Using Unicode Characters</li>
		<li>Get customer Ratings</li>
		<li>Present Ratings with Utmost Precision</li>
		<li>Set the Number Rating Icons</li>
		<li>All Props are Reactive</li>
		<li>Keyboard Shortcuts</li>
		<li>Built in User Accesability</li>
		<li>Handles Null values</li>
	</ul>
	<h2>Install</h2>
	<div>npm i -D svelt-rating-selector-display</div>
	<h2>Rating Selector</h2>
	<RatingSelector enableSelection={true} />

	<h2>Rating Display</h2>
	<RatingSelector rating={4.55} />
</div>

<style>
	h1 {
		font-size: clamp(2rem, 5vw, 4rem);
		padding-inline: 1em;
		text-align: center;
		padding-bottom: 0;
		margin-bottom: 0;
	}

	.wrapper {
		margin: auto;
		max-width: 80ch;
		padding-bottom: 5em;
		padding-inline: 2em;
		--icon-size: clamp(2.5rem, 10vw, 4rem);
	}

	h2 {
		font-size: clamp(1.5rem, 5vw, 3rem);
		text-align: left;
		padding-bottom: 0.5em;
		padding-top: 1em;
		margin-bottom: 0;
	}
</style>
