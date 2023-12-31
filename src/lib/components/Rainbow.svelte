<script lang="ts">
	import { Colord, colord } from '../colord';
	import ColourPicker from './ColourPicker.svelte';

	const count = 36;
	const chroma: number = Math.random() * 136;

	const bottomColour = {
		l: 25 + Math.random() * 50,
		h: Math.random() * (360 / count)
	};

	const topColour = {
		position: Math.floor(count / 4),
		l: 60 + Math.random() * 40,
		h: Math.floor(count / 4) * (360 / count) + bottomColour.h
	};

	function lightness(position: number): number {
		const delta =
			position < topColour.position
				? (topColour.l - bottomColour.l) / (topColour.position - 0)
				: (topColour.l - bottomColour.l) / (topColour.position - (count - 1 + 1));
		const offset = topColour.l - topColour.position * delta;

		return position * delta + offset;
	}

	function hue(position: number): number {
		const delta = (topColour.h - bottomColour.h) / topColour.position;
		const offset = topColour.h - topColour.position * delta;

		return position * delta + offset;
	}

	const colours: Colord[] = Array.from<never, Colord>({ length: count }, (_, i) =>
		colord({
			l: lightness(i),
			c: chroma,
			h: hue(i)
		})
	);
</script>

<ul>
	{#each colours as colour}
		<li>
			<ColourPicker bind:colour />
		</li>
	{/each}
</ul>

<style>
	ul {
		padding: 0;
		list-style: none;
		display: flex;
		overflow-x: auto;
	}
</style>
