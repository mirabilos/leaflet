---
layout: tutorial
title: Markers With Custom Icons
---

## Markers With Custom Icons

In this tutorial, you'll learn how to easily define your own icons for use by the markers you put on the map.

<div id="map" class="map" style="height: 220px"></div>

[View example on a separate page &rarr;](custom-icons-example.html)


### Preparing the images

To make a custom icon, we usually need two images --- the actual icon image and the image of its shadow. For this tutorial, we took the Leaflet logo and created four images out of it --- 3 leaf images of different colors and one shadow image for the three:

<p>
	<img style="border: 1px solid #ccc" src="../docs/images/leaf-green.png" />
	<img style="border: 1px solid #ccc" src="../docs/images/leaf-red.png" />
	<img style="border: 1px solid #ccc" src="../docs/images/leaf-orange.png" />
	<img style="border: 1px solid #ccc" src="../docs/images/leaf-shadow.png" />
</p>

Note that the white area in the images is actually transparent.

### Creating an icon

Marker icons in Leaflet are defined by [L.Icon](../reference.html#icon) objects, which are passed as an option when creating markers. Let's create a green leaf icon:

	var greenIcon = L.icon({
		iconUrl:      'leaf-green.png',
		shadowUrl:    'leaf-shadow.png',

		iconSize:     [38, 95], // size of the icon
		shadowSize:   [50, 64], // size of the shadow
		iconAnchor:   [22, 94], // point of the icon which will correspond to marker's location
		shadowAnchor: [4, 62],  // the same for the shadow
		popupAnchor:  [-3, -76] // point from which the popup should open relative to the iconAnchor
	});

Now putting a marker with this icon on a map is easy:

	L.marker([51.5, -0.09], {icon: greenIcon}).addTo(map);

<div id="map2" class="map" style="height: 220px"></div>

### Defining an icon class

What if we need to create several icons that have lots in common? Let's define our own icon class containing the shared options, inheriting from `L.Icon`! It's really easy in Leaflet:

	var LeafIcon = L.Icon.extend({
		options: {
			shadowUrl:    'leaf-shadow.png',
			iconSize:     [38, 95],
			shadowSize:   [50, 64],
			iconAnchor:   [22, 94],
			shadowAnchor: [4, 62],
			popupAnchor:  [-3, -76]
		}
	});

Now we can create all three of our leaf icons from this class and use them:

	var greenIcon = new LeafIcon({iconUrl: 'leaf-green.png'}),
	      redIcon = new LeafIcon({iconUrl: 'leaf-red.png'}),
	   orangeIcon = new LeafIcon({iconUrl: 'leaf-orange.png'});

You may have noticed that we used the `new` keyword for creating LeafIcon instances. So why do all Leaflet classes get created without it? The answer is simple: the real Leaflet classes are named with a capital letter (e.g. `L.Icon`), and they also need to be created with `new`, but there are also shortcuts with lowercase names (`L.icon`), created for convenience like this:

	L.icon = function (options) {
		return new L.Icon(options);
	};

You can do the same with your classes too. OK, lets finally put some markers with these icons on the map:

	L.marker([51.5, -0.09], {icon: greenIcon}).addTo(map).bindPopup("I am a green leaf.");
	L.marker([51.495, -0.083], {icon: redIcon}).addTo(map).bindPopup("I am a red leaf.");
	L.marker([51.49, -0.1], {icon: orangeIcon}).addTo(map).bindPopup("I am an orange leaf.");

That's it. Now take a look at the [full example](custom-icons-example.html), the [L.Icon docs](../reference.html#icon), or browse [other examples](../examples.html).

<script>
	var map = L.map('map').setView([51.5, -0.09], 13);

	L.tileLayer(MB_URL, {attribution: MB_ATTR, id: 'mapbox.light'}).addTo(map);

	var LeafIcon = L.Icon.extend({
		options: {
			iconUrl: '../docs/images/leaf-green.png',
			shadowUrl: '../docs/images/leaf-shadow.png',
			iconSize: [38, 95],
			shadowSize: [50, 64],
			iconAnchor: [22, 94],
			shadowAnchor: [4, 62],
			popupAnchor: [-3, -76]
		}
	});

	var greenIcon = new LeafIcon(),
		redIcon = new LeafIcon({iconUrl: '../docs/images/leaf-red.png'}),
		orangeIcon = new LeafIcon({iconUrl: '../docs/images/leaf-orange.png'});

	var marker1 = new L.Marker(new L.LatLng(51.5, -0.09), {icon: greenIcon}),
		marker2 = new L.Marker(new L.LatLng(51.495, -0.083), {icon: redIcon}),
		marker3 = new L.Marker(new L.LatLng(51.49, -0.1), {icon: orangeIcon});

	marker1.bindPopup("I am a green leaf.");
	marker2.bindPopup("I am a red leaf.");
	marker3.bindPopup("I am an orange leaf.");

	map.addLayer(marker1).addLayer(marker2).addLayer(marker3);



	var map2 = L.map('map2').setView([51.505, -0.09], 13);

	L.tileLayer(MB_URL, {attribution: MB_ATTR, id: 'mapbox.light'}).addTo(map2);

	var greenIcon2 = L.icon({
		iconUrl: '../docs/images/leaf-green.png',
		shadowUrl: '../docs/images/leaf-shadow.png',
		iconSize: [38, 95],
		shadowSize: [50, 64],
		iconAnchor: [22, 94],
		shadowAnchor: [4, 62],
		popupAnchor: [-3, -76]
	});

	L.marker([51.5, -0.09], {icon: greenIcon2}).addTo(map2);

</script>
