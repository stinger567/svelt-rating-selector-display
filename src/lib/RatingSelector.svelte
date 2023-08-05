<script lang="ts">
	import { tick } from 'svelte';

	type CSSAttributes = {
		[key: string]: string;
	};

	export let rating: number | null = null;
	export let enableSelection: boolean | null = false;
	export let numberOfIcons: number | null = 5;
	export let style: CSSAttributes | null = null;

	let selectorElement: HTMLElement;
	let ratingWhole: number;
	let numberOfIconsDefault: number;

	$: if (style && selectorElement) {
		for (const attribute in style) {
			if (attribute) {
				selectorElement.style.setProperty(attribute, style[attribute]);
			}
		}
	}

	$: ratingWhole = rating ? Math.floor(rating) : 0;
	$: numberOfIconsDefault = numberOfIcons ? numberOfIcons : 5;

	$: if (!enableSelection && selectorElement) {
		selectorElement.classList.remove('rating-selector-hover');
		removePartialFillStylig();
		if (rating && rating > 0 && numberOfIconsDefault > rating) {
			tick().then(() => {
				updatePartialFillRating();
			});
		}
	}

	function updatePartialFillRating() {
		const partialFillIcon: number = ratingWhole + 1;
		const partialRatingIcon: HTMLElement = selectorElement.getElementsByClassName(`iconLabel${partialFillIcon}`)[0] as HTMLElement;
		if (partialRatingIcon && ratingWhole != rating) {
			const partialFillAmount: number = (rating! - ratingWhole) * 100;
			const cssAttributes: CSSAttributes = {
				background: `linear-gradient(90deg, var(--icon-selected-color, gold) ${partialFillAmount}%, var(--icon-unslected-color, #ccc) ${partialFillAmount}%)`,
			};
			for (const attribute in cssAttributes) {
				partialRatingIcon.style.setProperty(attribute, cssAttributes[attribute]);
			}
		}
	}

	function removePartialFillStylig() {
		const allLabelElements: NodeListOf<HTMLLabelElement> = selectorElement.querySelectorAll('label');
		for (const labelElement of allLabelElements) {
			const cssAttributes: Array<string> = ['background'];
			for (const attribute of cssAttributes) {
				labelElement.style.removeProperty(attribute);
			}
		}
	}
</script>

<div class="rating-selector rating-selector-hover" bind:this={selectorElement}>
	{#each Array(numberOfIcons) as _, index}
		{@const iconId = numberOfIconsDefault - index}
		{#if enableSelection}
			<input class="icon{iconId}" type="radio" aria-label="icon{iconId}" value={iconId} bind:group={rating} />
			<!-- svelte-ignore a11y-click-events-have-key-events -->
			<!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
			<label
				for="icon{iconId}"
				title={iconId.toString()}
				data-label={iconId}
				on:click={() => {
					rating = iconId;
				}}
			/>
		{:else}
			<input class="icon{iconId}" type="radio" aria-label="icon{iconId}" value={iconId} bind:group={ratingWhole} disabled />
			<label class="iconLabel{iconId}" for="icon{iconId}" title={iconId.toString()} data-label={iconId} style="cursor: default;" />
		{/if}
	{/each}
</div>

<style module>
	.rating-selector {
		display: flex;
		flex-direction: row-reverse;
		flex-wrap: nowrap;
		width: fit-content;
		height: fit-content;
	}

	input {
		position: fixed;
		opacity: 0;
		pointer-events: none;
	}

	label {
		font-size: 10vw;
		cursor: pointer;
		font-size: var(--icon-size, 3.5rem);
		background: var(--icon-unslected-color, #ccc);
		padding-inline: var(--icon-spacing, 0em);
		background-clip: text !important;
		-webkit-background-clip: text !important;
		-webkit-text-fill-color: transparent !important;
	}

	label:before {
		content: var(--selector-icon, '★');
	}

	input:focus + label {
		-webkit-text-stroke: var(--focused-stroke-size, 3px) var(--focused-stroke-color, white);
	}

	input:checked ~ label {
		background: var(--icon-selected-color, gold);
	}

	.rating-selector-hover:not(:checked) > label:hover,
	.rating-selector-hover:not(:checked) > label:hover ~ label {
		background: var(--icon-unselected-hover-color, rgba(249, 224, 83, 0.695));
	}

	.rating-selector-hover > input:checked + label:hover,
	.rating-selector-hover > input:checked + label:hover ~ label,
	.rating-selector-hover > input:checked ~ label:hover,
	.rating-selector-hover > input:checked ~ label:hover ~ label,
	.rating-selector-hover > label:hover ~ input:checked ~ label {
		background: var(--icon-selected-hover-color, rgb(249, 221, 57));
	}
</style>
