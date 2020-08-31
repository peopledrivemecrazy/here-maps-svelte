# Svelte wrapper for Here Maps

Check [here maps JavaScript API](https://developer.here.com/develop/javascript-api) for detailed documentation.



## Setup

You need to add this before `</head>` to make it work.

```html

	<script src="https://js.api.here.com/v3/3.1/mapsjs-core.js" type="text/javascript" charset="utf-8"></script>
	<script src="https://js.api.here.com/v3/3.1/mapsjs-service.js" type="text/javascript" charset="utf-8"></script>
	<script src="https://js.api.here.com/v3/3.1/mapsjs-mapevents.js" type="text/javascript" charset="utf-8"></script>
	<script src="https://js.api.here.com/v3/3.1/mapsjs-ui.js" type="text/javascript" charset="utf-8"></script>
	<script src="https://js.api.here.com/v3/3.1/mapsjs-clustering.js" type="text/javascript" charset="utf-8"></script>
	<link rel="stylesheet" type="text/css" href="https://js.api.here.com/v3/3.1/mapsjs-ui.css" />
    
```

## Quick Start

Install `npm i here-maps-svelte`

```html

<script>
import Map from 'here-maps-svelte'

let options = {
		api: "Your API Key",
		mapdata: {
			zoom: 3,
			center: {
       			lat: 48.8567,
				lng: 2.3508
			},
			markers: [
				{	bubbletext:`<p>Bubble text</p>`,
					lat: 48.8567,
					lng: 2.3508
				} 
			]
		}
	}
</script>

<div id="map">
  <Map options={options}></Map>
</div>

<style>
  #map {
    height: inherit;
    width: inherit;
  }
</style>

```


## Note

* Currently supports bubble texts and accepts html. You might need to play with it.
* Have `<Map {options}/>` a child of a `div` and supply custom css for height/width.


## Upcoming features

* Dynamic Markers
* Search
* Polylines, routing, shapes
* Custom Icon Support