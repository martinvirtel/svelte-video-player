<script>
  import { onDestroy } from "svelte";
      
  export let element;
  export let isFullscreen;
  export let isFullscreenEnabled;

  import { screenfull } from "./libs/screenfull.js"; 


  isFullscreenEnabled = screenfull.isEnabled;

   if (isFullscreenEnabled) screenfull.on("change", onChange);

      function onChange(e) {
        if (element == e.target) isFullscreen = screenfull.isFullscreen;
   }


  onDestroy(() => {
    screenfull.off("change", onChange);
   });

      $: {
        if (isFullscreenEnabled)
          isFullscreen ? screenfull.request(element) : screenfull.exit();
          }
</script>
