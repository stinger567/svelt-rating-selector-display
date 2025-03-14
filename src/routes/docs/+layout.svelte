<script lang="ts">
	interface Props {
		children?: import('svelte').Snippet;
	}

	let { children }: Props = $props();
</script>

<article class="markdown-body">
	{@render children?.()}
</article>

<style>
	article {
		max-width: 80ch;
		padding: clamp(0.5em, 5vw, 2em);
		margin: auto;
		margin-top: 5em;
		margin-bottom: 5em;
	}
</style>
