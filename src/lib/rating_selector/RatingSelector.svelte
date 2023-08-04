<script lang="ts">
	import { onMount } from 'svelte';

	export let rating: number | null = null;
	export let enableSelection: boolean = false;
	export let numberOfIcons: number = 5;
	export let style: CSSAttributes | null = null;

	type CSSAttributes = {
		[key: string]: string;
	};

	let selectorElement: HTMLElement;
	onMount(() => {
		if (!enableSelection && selectorElement) {
			selectorElement.classList.remove('rating-selector-hover');
			if (rating && rating > 0 && rating < numberOfIcons) {
				const partialFillIcon: number = Math.floor(rating) + 1;
				const partialRatingIncon: HTMLElement = selectorElement.getElementsByClassName(`iconLabel${partialFillIcon}`)[0] as HTMLElement;
				if (partialRatingIncon && partialFillIcon != rating) {
					const partialFillAmount = (rating - partialFillIcon + 1) * 100;
					const cssAttributes: CSSAttributes = {
						background: `linear-gradient(90deg, var(--icon-selected-color, gold) ${partialFillAmount}%, var(--icon-unslected-color, #ccc) ${partialFillAmount}%)`,
						'background-clip': 'text',
						'-webkit-background-clip': 'text',
						'-webkit-text-fill-color': 'transparent'
					};
					for (const attribute in cssAttributes) {
						partialRatingIncon.style.setProperty(attribute, cssAttributes[attribute]);
					}
				}
			}
		}
		if (rating) {
			const radio: HTMLInputElement = selectorElement.getElementsByClassName(`icon${Math.floor(rating)}`)[0] as HTMLInputElement;
			if (radio) {
				radio.checked = true;
			}
		}
		if (style) {
			for (const attribute in style) {
				if (attribute) {
					selectorElement.style.setProperty(attribute, style[attribute]);
				}
			}
		}
	});
</script>

<div class="rating-selector rating-selector-hover" bind:this={selectorElement}>
	{#each Array(numberOfIcons) as _, index}
		{@const iconId = numberOfIcons - index}
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
			<input class="icon{iconId}" type="radio" aria-label="icon{iconId}" value={iconId} disabled />
			<label class="iconLabel{iconId}" for="icon{iconId}" title={iconId.toString()} data-label={iconId} style="cursor: default;" />
		{/if}
	{/each}
</div>

<style module>
	.rating-selector {
		display: flex;
		flex-direction: row-reverse;
		flex-wrap: nowrap;
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
		color: var(--icon-unslected-color, #ccc);
		padding-inline: var(--icon-spacing, 0em);
	}

	label:before {
		content: var(--selector-icon, '★');

		background-size: contain;
		background-repeat: no-repeat;
		background-position: center;
	}

	input:checked ~ label {
		color: var(--icon-selected-color, gold);
	}

	.rating-selector-hover:not(:checked) > label:hover,
	.rating-selector-hover:not(:checked) > label:hover ~ label {
		color: var(--icon-unselected-hover-color, rgba(249, 224, 83, 0.695));
	}

	.rating-selector-hover > input:checked + label:hover,
	.rating-selector-hover > input:checked + label:hover ~ label,
	.rating-selector-hover > input:checked ~ label:hover,
	.rating-selector-hover > input:checked ~ label:hover ~ label,
	.rating-selector-hover > label:hover ~ input:checked ~ label {
		color: var(--icon-selected-hover-color, rgb(249, 221, 57));
	}
</style>
