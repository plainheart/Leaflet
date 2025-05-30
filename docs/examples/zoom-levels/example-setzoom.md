---
layout: tutorial_frame
title: Zoom Control Example
---
<script type="module">
	import L, {Map, TileLayer, Control, DomUtil} from 'leaflet';

	const map = new Map('map', {
		minZoom: 0,
		maxZoom: 1
	});

	const cartodbAttribution = '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, &copy; <a href="https://carto.com/attribution">CARTO</a>';

	const positron = new TileLayer('https://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}.png', {
		attribution: cartodbAttribution
	}).addTo(map);

	setInterval(() => {

		map.setZoom(0);

		setTimeout(() => {
			map.setZoom(1);
		}, 2000);

	}, 4000);

	const ZoomViewer = Control.extend({
		onAdd() {
			const gauge = DomUtil.create('div');
			gauge.style.width = '200px';
			gauge.style.background = 'rgba(255,255,255,0.5)';
			gauge.style.textAlign = 'left';
			map.on('zoomstart zoom zoomend', (ev) => {
				gauge.innerHTML = `Zoom level: ${map.getZoom()}`;
			});
			return gauge;
		}
	});

	const zoomViewer = (new ZoomViewer()).addTo(map);

	map.setView([0, 0], 0);

	globalThis.L = L; // only for debugging in the developer console
	globalThis.map = map; // only for debugging in the developer console
</script>
