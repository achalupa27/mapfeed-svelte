<!--ues d3geo, topojson, geojson-->
<script lang="ts">
	import { feature } from 'topojson';
	import * as d3 from 'd3';
	import { onMount } from 'svelte';

	function handleZoom(e: any) {
		d3.select('svg').attr('transform', e.transform);
	}

	onMount(() => {
		const svg = d3.select('svg');
		let zoom = d3
			.zoom()
			.on('zoom', handleZoom)
			.scaleExtent([1, 5])
			.translateExtent([
				[0, 0],
				[960, 500]
			]);

		d3.select('svg').call(zoom);
		const pathGenerator = d3.geoPath(d3.geoEquirectangular());

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
				.on('click', function (d) {
					console.log('country clicked: ', countryName[d.id]);
				})
				.append('title')
				.text((d: any) => countryName[d.id]);
		});
	});
</script>

<div class="app">
	<div class="title-bar">
		<div class="selected-country">
			<span>Country</span>
		</div>
	</div>

	<div class="map">
		<svg width="960" height="500" />
	</div>

	<div class="footer">
		<div class="statistics" />
	</div>
</div>

<style lang="sass">
	:global(.country)
		fill: #245a2d

		&:hover
			fill: red

	.app
		display: flex
		flex-direction: column
		height: 100%
		font-family: 'Poppins'

	.title-bar, .footer
		background: #0d1a2c

	.title-bar
		height: 40px
		display: flex
		justify-content: center
		align-items: center

	.selected-country
		color: white

	.footer
		height: 30%

	.map
		height: 100%
		display: flex
		background: #1a2b41
		flex-grow: 1
		justify-content: center
		align-items: center

</style>
