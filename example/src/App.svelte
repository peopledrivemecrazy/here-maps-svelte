<script>
  import Map from "here-maps-svelte";
  let api = "LuNQAP-NMnj9UVtwKxCi3GN4RA23MmSFfZWbH0dlauY";

  let options = {
    api,
    mapdata: {
      zoom: 3,
      center: {
        lat: 48.8567,
        lng: 2.3508,
      },
    },
  };
</script>

<Map {options} />
