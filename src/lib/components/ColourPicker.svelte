<script lang="ts">
	import { Colord } from '$lib/colord';

	export let colour: Colord;

	let dialog: HTMLDialogElement;

	const colourGradient = `linear-gradient(to right, ${colour.toLchString()} 50%, ${colour.toHex()} 50%)`;
</script>

<button
	class="sample"
	class:dark={colour.isDark()}
	style:background={colourGradient}
	on:click={() => {
		dialog.showModal();
	}}
/>

<!-- svelte-ignore a11y-click-events-have-key-events a11y-no-noninteractive-element-interactions -->
<dialog
	bind:this={dialog}
	on:click|self={() => {
		dialog.close();
	}}
>
	<!-- svelte-ignore a11y-no-static-element-interactions -->
	<div class:dark={colour.isDark()} style:background={colourGradient} on:click|stopPropagation>
		<ul>
			<li>{colour.toHex()}</li>
			<li>{colour.toRgbString()}</li>
			<li>{colour.toLchString()}</li>
		</ul>
	</div>
</dialog>

<style>
	.sample {
		appearance: none;
		border: none;
		min-width: 2em;
		min-height: 2em;
		padding: 1em;
		cursor: pointer;
		font-family: monospace;
	}

	.dark {
		color: white;
	}

	dialog {
		border: none;
		padding: 0;
		font-family: monospace;
	}

	dialog::backdrop {
		background: rgba(0, 0, 0, 0.3);
	}

	dialog > div {
		padding: 2em;
	}

	dialog ul {
		padding: 0;
		list-style: none;
	}
</style>
