<!-- your code here -->
<script>
  import Sdk from "./Sdk.svelte";

  export let options;
  let loaded = false;
  function init() {
    loaded = true;
  }
  function createMap(node, options) {
    var platform = new H.service.Platform({
      apikey: options.api,
    });

    var maptypes = platform.createDefaultLayers();
    let map = new H.Map(node, maptypes.vector.normal.map, options.mapdata);

    let ui = H.ui.UI.createDefault(map, maptypes);

    var mapSettings = ui.getControl("mapsettings");
    var zoom = ui.getControl("zoom");
    var scalebar = ui.getControl("scalebar");

    mapSettings.setAlignment("top-left");
    zoom.setAlignment("right-middle");
    scalebar.setAlignment("top-left");

    new H.mapevents.Behavior(new H.mapevents.MapEvents(map));

    window.addEventListener("resize", () => map.getViewPort().resize());

    map.setZoom(map.getZoom() + options.mapdata.zoom, true);

    function addMarkersToMap(markers) {
      if (markers) {
        markers.map((e) => {
          let marker = map.addObject(new H.map.Marker(e));
          if (e.bubbletext) {
            marker.setData(`${e.bubbletext}`);
            marker.addEventListener("tap", (evt) => {
              let bubble = new H.ui.InfoBubble(evt.target.getGeometry(), {
                content: evt.target.getData(),
              });
              ui.addBubble(bubble);
            });
          }
        });
      }
    }

    addMarkersToMap(options.mapdata.markers);
  }
</script>

{#if loaded}
  <div use:createMap={options} />
{/if}

<Sdk on:ready={init} />

<style>
  div {
    height: inherit;
    width: inherit;
  }
</style>
