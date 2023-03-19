<script lang="ts">
	import { feature } from 'topojson';
	import * as d3 from 'd3';
	import { onMount } from 'svelte';


	function handleZoom(e: any) {
		d3.select('svg').attr('transform', e.transform);
	}

	onMount(() => {
		const svg = d3.select('svg');
		let zoom = d3.zoom().on('zoom', handleZoom).scaleExtent([1, 5]);
		// .translateExtent([
		// 	[0, 0],
		// 	[960, 500]
		// ]);

		const width = 1460;
		const height = 900;
		d3.select('svg').call(zoom as any);
		const pathGenerator = d3.geoPath(
			d3
				.geoEquirectangular()
				.scale(120)
				.translate([width / 2, height / 2])
		);

		d3.tsv('http://unpkg.com/world-atlas@1.1.4/world/110m.tsv').then((data: any) => {});

		Promise.all([
			d3.tsv('https://unpkg.com/world-atlas@1.1.4/world/50m.tsv'),
			d3.json('https://unpkg.com/world-atlas@1.1.4/world/50m.json')
		]).then(([tsvData, data]: [any, any]) => {
			const countryName = tsvData.reduce((accumulator: any, d: any) => {
				accumulator[d.iso_n3] = d.name;
				return accumulator;
			}, {});

			svg
				.selectAll('path')
				.data((feature(data, data.objects.countries) as any).features)
				.enter()
				.append('path')
				.attr('class', 'country')
				.attr('d', (d: any) => pathGenerator(d))
				.on('click', (d) => {
					console.log(d);
					changeCountry(d.originalTarget.textContent);
				})
				.append('title')
				.text((d: any) => countryName[d.id]);
		});
	});

	let selectedCountry: any;
	let population: any;
	function changeCountry(country: string) {
		let countryData = map.get(country);
		if (countryData !== undefined) {
			selectedCountry.textContent = country;
			population.textContent = countryData.Population;
		}
	}
</script>

<div class="app">
	<div class="title-bar">
		<div class="selected-country">
			<span bind:this={selectedCountry}>Click a country!</span>
		</div>
	</div>

	<div class="map">
		<svg width="100%" height="100%" />
	</div>

	<div class="footer">
		<div class="statistics">
			<p>Population: <span bind:this={population} /></p>
		</div>
	</div>
</div>

<style lang="sass">
	:global(.country)
		fill: #0e430d
		stroke: white

		&:hover
			fill: white

	p
		margin: 0

	.app
		display: flex
		flex-direction: column
		height: 100vh
		font-family: 'Poppins'

	.title-bar
		z-index: 10	
		height: 40px
		position: absolute
		top: 0
		width: calc(100% - 16px)
		color: white
		margin: 8px
		border: 1px solid white
		border-radius: 4px
		background: #1a2b41
		display: flex
		justify-content: center
		align-items: center
		opacity: 0.8
		box-shadow: 0px 1px 3px rgb(255 255 255 / 0.5)

	.footer
		z-index: 10	
		position: absolute
		bottom: 0
		height: 30%
		width: calc(100% - 32px)
		color: white
		margin: 8px
		border: 1px solid white
		border-radius: 4px
		padding: 8px
		background: #1a2b41
		opacity: 0.8
		box-shadow: 0px 1px 3px rgb(255 255 255 / 0.5)

	.map
		height: 100%
		background: #1a2b41
		flex-grow: 1

</style>
