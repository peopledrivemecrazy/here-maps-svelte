<script>
  import loader from "@beyonk/async-script-loader";
  import { createEventDispatcher, onMount } from "svelte";
  import { mapsLoaded, mapsLoading } from "./stores.js";
  const dispatch = createEventDispatcher();
  $: $mapsLoaded && dispatch("ready");
  let H = {};
  //   let map = "";
  onMount(() => {
    if ($mapsLoaded) {
      dispatch("ready");
    }
    if (!$mapsLoading) {
      mapsLoading.set(true);
      loader(
        [
          {
            type: "style",
            url: `https://js.api.here.com/v3/3.1/mapsjs-ui.css`,
          },
          {
            type: "script",
            url: `https://js.api.here.com/v3/3.1/mapsjs.bundle.js`,
            options: {
              async: true,
              defer: true,
              module: true,
            },
          },
        ],
        () => {
          return false;
        },
        () => {
          H = window.H;
          console.log(H);
          //   map = H.map;
          mapsLoaded.set(true);
          return true;
        }
      );
    }
  });
</script>
