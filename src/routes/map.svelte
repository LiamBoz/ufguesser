
<script>
    import { onMount } from 'svelte';

    let map;
    let marker;

    onMount(() => {
        (g => {
            var h, a, k, p = "The Google Maps JavaScript API", c = "google", l = "importLibrary", q = "__ib__", m = document, b = window;
            b = b[c] || (b[c] = {});
            var d = b.maps || (b.maps = {}), r = new Set, e = new URLSearchParams,
                u = () => h || (h = new Promise(async (f, n) => {
                    await (a = m.createElement("script"));
                    e.set("libraries", [...r] + "");
                    for (k in g) e.set(k.replace(/[A-Z]/g, t => "_" + t[0].toLowerCase()), g[k]);
                    e.set("callback", c + ".maps." + q);
                    a.src = `https://maps.${c}apis.com/maps/api/js?` + e;
                    d[q] = f;
                    a.onerror = () => h = n(Error(p + " could not load."));
                    a.nonce = m.querySelector("script[nonce]")?.nonce || "";
                    m.head.append(a)
                }));
            d[l] ? console.warn(p + " only loads once. Ignoring:", g) : d[l] = (f, ...n) => r.add(f) && u().then(() => d[l](f, ...n))
        })({
            key: "AIzaSyDhEt6Yj7fgNaOEO1z7DwjUkTfmJynck54",  // Replace with your API key
            v: "weekly"
        });

        // Wait for Google Maps API to load, then initialize the map
        window.google.maps.importLibrary("maps").then(() => {
            const mapOptions = {
                center: { lat: 29.6465, lng: -82.3533 },  // Set your preferred location
                zoom: 12,
                disableDefaultUI: true
            };
            map = new google.maps.Map(document.getElementById("map"), mapOptions);


        map.addListener('click', (event) => {
          const {latLng} = event;
          const lat = latLng.lat();
          const lng = latLng.lng();


          console.log("Latitude:", lat, "Longitude", lng);
        if (marker) {
          marker.setPosition(latLng);
        }else {
          marker = new google.maps.Marker({
            position: latLng,
            map: map
          });
        }
        

        });
    });
  });
</script>

<style>
    .map-container {
        position: fixed;
        bottom: 20px;
        right: 20px;
        width: 300px;
        height: 200px;
        border: 2px solid #ccc;
        border-radius: 8px;
        overflow: hidden;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        transition: width 0.3s ease, height 0.3s ease;
    }

    .map-container:hover {
        width: 500px; /* Expanded width */
        height: 400px; /* Expanded height */
    }

    #map {
        width: 100%;
        height: 100%;
    }
</style>

<div class="map-container">
    <div id="map"></div>
</div>
