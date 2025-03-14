<script lang="ts">
	import RatingSelector from '$lib/RatingSelector.svelte';
	let rating1: number | null = $state(null);
	let rating2: number | null = $state(3.55);
	let iconNumber1: number | null = $state(5);
	let iconNumber2: number | null = $state(5);

	let selectedColor1 = $state('#ffd700');
	let unselectedColor1 = $state('#cccccc');
	let selectedHoverColor1 = $state('#f9dd39');
	let unselectedHoverColor1 = $state('#f9e053');
	let focusColor1 = $state('#ffffff');
	let focusSize1 = $state('3px');
	let iconSize1 = $state('3.5rem');
	let iconSpacing1 = $state('0rem');
	let icon1 = $state('★');
	const style1: { [key: string]: string } = $derived({
			'--icon-selected-color': `${selectedColor1}`,
			'--icon-unselected-hover-color': `${unselectedHoverColor1}`,
			'--icon-selected-hover-color': `${selectedHoverColor1}`,
			'--icon-unslected-color': `${unselectedColor1}`,
			'--focused-stroke-color': `${focusColor1}`,
			'--focused-stroke-size': `${focusSize1}`,
			'--icon-size': `${iconSize1}`,
			'--icon-spacing': `${iconSpacing1}`,
			'--selector-icon': JSON.stringify(`${icon1}`),
		});

	let selectedColor2 = $state('#ffd700');
	let unselectedColor2 = $state('#cccccc');
	let iconSize2 = $state('3.5rem');
	let iconSpacing2 = $state('0rem');
	let icon2 = $state('★');
	const style2: { [key: string]: string } = $derived({
			'--icon-selected-color': `${selectedColor2}`,
			'--icon-unslected-color': `${unselectedColor2}`,
			'--icon-size': `${iconSize2}`,
			'--icon-spacing': `${iconSpacing2}`,
			'--selector-icon': JSON.stringify(`${icon2}`),
		});
</script>

<h1>DEMO</h1>
<div class="rating-selector-container">
	<h2 class="header-selector">Selector</h2>
	<div class="rating-selector">
		<RatingSelector bind:rating={rating1} enableSelection={true} numberOfIcons={iconNumber1} style={style1} />
	</div>
	<div class="rating">Current rating: {rating1}</div>

	<label class="first-selector-label" for="default-rating1">Change rating</label>
	<input class="first-selector-input" id="default-rating-1" type="number" bind:value={rating1} />

	<label for="number-of-stars-1">Change the number of stars</label>
	<input id="number-of-stars-1" type="number" bind:value={iconNumber1} />

	<label for="selected-color-1">Change the color of the selected stars</label>
	<input
		type="color"
		id="selected-color-1"
		bind:value={selectedColor1}
		name="hexInput"
		pattern="^[0-9a-fA-F]+$"
		title="Please enter a valid hexadecimal value (0-9, a-f, A-F)"
	/>

	<label for="selected-hover-color-1">Change the color of the selected stars when hovered</label>
	<input
		type="color"
		id="selected-hover-color-1"
		bind:value={selectedHoverColor1}
		name="hexInput"
		pattern="^[0-9a-fA-F]+$"
		title="Please enter a valid hexadecimal value (0-9, a-f, A-F)"
	/>

	<label for="unselected-color-1">Change the color of the unselected stars</label>
	<input
		type="color"
		id="unselected-color-1"
		bind:value={unselectedColor1}
		name="hexInput"
		pattern="^[0-9a-fA-F]+$"
		title="Please enter a valid hexadecimal value (0-9, a-f, A-F)"
	/>

	<label for="unselected-hover-color-1">Change the color of the unselected stars when hovered</label>
	<input
		type="color"
		id="unselected-hover-color-1"
		bind:value={unselectedHoverColor1}
		name="hexInput"
		pattern="^[0-9a-fA-F]+$"
		title="Please enter a valid hexadecimal value (0-9, a-f, A-F)"
	/>

	<label for="focus-color-1">Change the color of the focus stroke</label>
	<input
		type="color"
		id="focus-color-1"
		bind:value={focusColor1}
		name="hexInput"
		pattern="^[0-9a-fA-F]+$"
		title="Please enter a valid hexadecimal value (0-9, a-f, A-F)"
	/>

	<label for="focus-size-1">Change the size of the stroke when element is focused</label>
	<input type="text" id="focus-size-1" bind:value={focusSize1} name="icon focused size" />

	<label for="icon-size-1">Change the icon size</label>
	<input type="text" id="icon-size-1" bind:value={iconSize1} name="icon size" />

	<label for="icon-spacing-1">Change the icon spacing</label>
	<input type="text" id="icon-spacing-1" bind:value={iconSpacing1} name="icon spacing" />

	<label class="last-selector-label" for="icon-1">Change the icon</label>
	<input class="last-selector-input" type="text" id="icon-1" bind:value={icon1} name="icon selector" />

	<h2 class="header-display">Display</h2>
	<div class="rating-selector">
		<RatingSelector bind:rating={rating2} numberOfIcons={iconNumber2} style={style2} />
	</div>
	<div class="rating">Current rating: {rating2}</div>

	<label class="default-rating-label" for="default-rating-2">Change rating</label>
	<input class="default-rating-input" id="default-rating-2" type="number" bind:value={rating2} />

	<label class="numbers-of-stars-label" for="number-of-stars-2">Change the number of stars</label>
	<input class="number-of-stars-input" id="number-of-stars-2" type="number" bind:value={iconNumber2} />

	<label for="selected-color-2">Change the color of the selected stars</label>
	<input
		type="color"
		id="selected-color-2"
		bind:value={selectedColor2}
		name="hexInput"
		pattern="^[0-9a-fA-F]+$"
		title="Please enter a valid hexadecimal value (0-9, a-f, A-F)"
	/>

	<label for="unselected-color-2">Change the color of the unselected stars</label>
	<input
		type="color"
		id="unselected-color-2"
		bind:value={unselectedColor2}
		name="hexInput"
		pattern="^[0-9a-fA-F]+$"
		title="Please enter a valid hexadecimal value (0-9, a-f, A-F)"
	/>

	<label for="icon-size-2">Change the icon size</label>
	<input type="text" id="icon-size-2" bind:value={iconSize2} name="icon size" />

	<label for="icon-spacing-2">Change the icon spacing</label>
	<input type="text" id="icon-spacing-2" bind:value={iconSpacing2} name="icon spacing" />

	<label class="last-selector-label" for="icon-1">Change the icon</label>
	<input class="last-selector-input" type="text" id="icon-1" bind:value={icon2} name="icon selector" />
</div>

<style>
	h1 {
		font-size: clamp(2rem, 5vw, 4rem);
		padding-inline: 1em;
		text-align: center;
		padding-bottom: 0;
		margin-bottom: 0;
	}

	.rating-selector-container {
		display: grid;
		grid-template-columns: 1fr 1fr !important;
		row-gap: 1em;
		align-items: center;
		justify-content: center;
		/* padding-top: 0em; */
		padding-bottom: 5em;
		padding-inline: 2em;
		max-width: 100ch;
		margin: auto;
	}

	h2 {
		grid-column: span 2;
		font-size: clamp(1.5rem, 4.5vw, 3.5rem);
		padding-bottom: 0.25em;
		border-bottom: 2px solid var(--main-color-light);
	}

	input {
		margin-inline: auto;
		max-width: 10ch;
		font-size: clamp(1rem, 2vw, 1.5rem);
		padding-left: 0.5rem;
		background-color: var(--main-color-light);
	}

	input[type='color'] {
		width: clamp(5rem, 13vw, 9.25rem);
		max-width: 20rem;
		padding-inline: 0.25rem;
		height: clamp(1.75rem, 4vw, 2.25rem);
	}

	label {
		font-size: clamp(1rem, 2vw, 1.5rem);
		padding-inline: 1em;
		padding-top: 0.5em;
		border-top: 1px solid var(--main-color-light);
	}

	.rating-selector {
		margin: auto;
		padding-inline: 1em;
	}

	.rating {
		font-size: clamp(1rem, 2vw, 1.5rem);
		text-align: center;
	}

	@media (max-width: 439px) {
		.rating-selector-container {
			grid-template-columns: 1fr !important;
		}

		h2 {
			grid-column: span 1;
		}

		label {
			text-align: center;
		}
	}
</style>
