<script lang="ts">
	import { tick } from 'svelte';

	type CSSAttributes = {
		[key: string]: string;
	};

	interface Props {
		rating?: number | null;
		enableSelection?: boolean | null;
		numberOfIcons?: number | null;
		style?: CSSAttributes | null;
	}

	let {
		rating = $bindable(null),
		enableSelection = false,
		numberOfIcons = 5,
		style = null
	}: Props = $props();

	let selectorElement: HTMLElement;
	let roudedRating: {rating: number} = {
		get rating(){
			return Math.min(rating ? Math.floor(rating) : 0, numberOfIcons || Number.MAX_VALUE);
		},
		set rating(rating: number){rating=rating}};
	const numberOfIconsDefault: number = $derived(numberOfIcons ? numberOfIcons : 5);

	function updatePartialFillRating() {
		const partialFillIcon: number = roudedRating.rating + 1;
		const partialRatingIcon: HTMLElement = selectorElement.getElementsByClassName(`iconLabel${partialFillIcon}`)[0] as HTMLElement;
		if (partialRatingIcon && roudedRating.rating != rating) {
			const partialFillAmount: number = (rating! - roudedRating.rating) * 100;
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
	
	$effect(() => {
		if (style && selectorElement) {
			for (const attribute in style) {
				if (attribute) {
					selectorElement.style.setProperty(attribute, style[attribute]);
				}
			}
		}
	});

	$effect(() => {
		if (!enableSelection && selectorElement) {
			selectorElement.classList.remove('rating-selector-hover');
			removePartialFillStylig();
			if (rating && rating > 0 && numberOfIconsDefault > rating) {
				tick().then(() => {
					updatePartialFillRating();
				});
			}
		}
	});
</script>

<div class="rating-selector rating-selector-hover" bind:this={selectorElement}>
	{#each Array(numberOfIcons) as _, index}  
		{@const iconId = numberOfIconsDefault - index}
		{#if enableSelection}
			<input class="icon{iconId}" type="radio" aria-label="icon{iconId}" value={iconId} bind:group={roudedRating.rating} />
			<!-- svelte-ignore a11y_click_events_have_key_events -->
			<!-- svelte-ignore a11y_no_noninteractive_element_interactions -->
			<label
				for="icon{iconId}"
				title={iconId.toString()}
				data-label={iconId}
				onclick={() => {
					rating = iconId;
				}}
			></label>
		{:else}
			<input class="icon{iconId}" type="radio" aria-label="icon{iconId}" value={iconId} bind:group={roudedRating.rating} disabled />
			<label class="iconLabel{iconId}" for="icon{iconId}" title={iconId.toString()} data-label={iconId} style="cursor: default;"></label>
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
		position: absolute;
		opacity: 0;
		pointer-events: none;
	}

	label {
		font-size: 10vw;
		cursor: pointer;
		font-size: var(--icon-size, 3.5rem);
		background: var(--icon-unslected-color, #cccccc);
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
