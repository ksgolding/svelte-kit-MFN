<!-- <svelte:options tag='ui-map' /> -->

<script lang='ts'>
  import {Map, View} from 'ol';
  import TileLayer from 'ol/layer/Tile';
  import OSM from 'ol/source/OSM';
  import {Zoom} from 'ol/control';
  import {onMount, createEventDispatcher} from "svelte";
  import { get_current_component } from 'svelte/internal';

  const component = get_current_component();
  const svelteDispatch = createEventDispatcher();

  const dispatch = (name, detail) => {
    // We need this workaround to send messages to client from a custom component (tag)
    // because Svelte has open issue: "Events are not permitted from components compiled
    // to a custom element #3119".
    // See: https://github.com/sveltejs/svelte/issues/3119.
    svelteDispatch(name, detail);
    component.dispatchEvent &&
      component.dispatchEvent(new CustomEvent(name, { detail }));
  };

  let map: Map = undefined;

  let mapContainerElement = undefined;

  onMount(() => {
    const mapEl = mapContainerElement;

    const style = document.createElement('style');
    style.setAttribute('class', 'ui-map-css');
    style.innerHTML = '.custom-zoom-control {height: 50px; width: 35px; position: relative; top: 1rem}';
    mapEl.appendChild(style);
    
    const zoomControl = new Zoom({
      zoomInTipLabel: 'Zoom closer in',
      zoomOutTipLabel: 'Zoom further out',
      className: 'ol-zoom custom-zoom-control'
    });

    map = new Map({
      controls: [zoomControl],
      layers: [
        new TileLayer({
          source: new OSM(),
        }),
      ],
      target: mapEl,
      view: new View({
        projection: 'EPSG:4326',
        center: [0, 0],
        zoom: 1,
        minZoom: 1
      }),
      keyboardEventTarget: document
    });

    setTimeout(() => {
      dispatch('message', {map: map});
    });
  });
</script>

<div bind:this='{mapContainerElement}' class='ui-map-container'>
</div>

<style lang='scss'>
  // FIXME: Unable style ol map elements included
  // in the dom from the ol map library in this style tag.
  .ui-map-container {
    height: 100%;
    width: 100%;
  }
</style>
