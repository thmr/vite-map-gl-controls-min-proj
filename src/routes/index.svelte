<script>
    import {onMount} from "svelte";
    import mapboxgl from "mapbox-gl";
    import { ZoomControl } from 'mapbox-gl-controls';
    let map
    export let disableZoom = false
    export let initialZoom = 12
    const initialCoords = {lat: 41.2834600, lng: -70.0994600}

    let mapMarkers = []

    $: {
        if(typeof  map !== 'undefined'){
            mapMarkers.forEach((marker) => {
                marker.remove()
            })

        }
    }

    onMount(() => {
        mapboxgl.accessToken = 'your-access-token'
        map = new mapboxgl.Map({
            container: "map",
            style: "mapbox://styles/thmr/cl3wdqg9k001x14n90h95nzeh",
            center: [initialCoords['lng'], initialCoords['lat']],
            zoom: initialZoom,
        })
        if(disableZoom){
            map.scrollZoom.disable()
        }
         map.addControl(new ZoomControl(), 'top-right')

    })

</script>

<svelte:head>
    <link href='https://api.mapbox.com/mapbox-gl-js/v2.8.1/mapbox-gl.css' rel='stylesheet' />
</svelte:head>

<div id="map" style="width: 600px; height: 600px"></div>
