<script lang="ts">
  import Counter from './lib/Counter.svelte'
  import { MapLibre, MapEvents, DefaultMarker } from 'svelte-maplibre';
  import { MapMouseEvent } from 'maplibre-gl';
  // Create basic marker:
  let markers = [];
  function addMarker(e: CustomEvent<MapMouseEvent>) {
    markers = [...markers, { lngLat: e.detail.lngLat }];
  }
  // Counter of how many markers:
  $: markerCount = markers.length;
</script>

<main>
  <div>
    <h1>WldMap</h1>
    <MapLibre 
    center={[-1,53]}
    zoom={2}
    class="map"
    standardControls
    style="https://basemaps.cartocdn.com/gl/positron-gl-style/style.json">
    <MapEvents on:click={addMarker} />
  
    {#each markers as marker}
      <DefaultMarker lngLat={marker.lngLat} />
    {/each}
  </MapLibre>
  </div>


  <div class="card">
    <p>You have {markerCount} markers</p>
    <Counter />
  </div>

</main>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .read-the-docs {
    color: #888;
  }
  :global(.map) {
    width: 500px;
    height: 500px;
  }
</style>
