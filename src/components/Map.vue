<template>
    <section id='mapsection'>
        <div class="container" id='map'></div>
    </section>
</template>

<script>
import "leaflet/dist/leaflet.css";
import L from "leaflet";

export default {
 name: "Map",
 props: ['marilyns'],
 data() {
   return{
     center: [52.33022, -3.766409]
   }},
 methods: {
    setupLeafletMap: function () {
        const mapDiv = L.map('map').setView(this.center, 7.5)

        L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
            maxZoom: 19,
            attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'
        }).addTo(mapDiv);

        const marilynGeoJson = this.createGeoJson();

        const markerOptions = {
            icon: L.icon({
                iconUrl: 'favicon.ico',
                iconSize: [22, 22]
            })
        }

        L.geoJSON(marilynGeoJson, {
            style: {"color": "none"},
            onEachFeature: function (feature, layer) {
                layer.bindPopup(
                    `<strong>${feature.properties.name}</strong><br>
                    Height (Metres): ${feature.properties.metres}<br>
                    Height (Feet): ${feature.properties.feet}<br>
                    Drop: ${feature.properties.drop}<br>
                    <a href="#${feature.properties.name}">Jump to table</a>`
                );
            },
            pointToLayer: function (feature, latlng) {
                return L.marker(latlng, markerOptions)
            }
        }).addTo(mapDiv);

    },

    createGeoJson: function () {
        const marilyns = JSON.parse(JSON.stringify(this.marilyns))
        const geoJson = []

        for (let [_, marilyn] of Object.entries(marilyns)) {
            geoJson.push({
                "type": "Feature",
                "properties": {
                    "name": marilyn['Name'],
                    "metres": marilyn['Metres'],
                    "feet": marilyn['Feet'],
                    "drop": marilyn['Drop']
                },
                "geometry": {
                    "type": "Point",
                    "coordinates": [marilyn['longitude'], marilyn['latitude']]
                }
            })
        }

        return geoJson
    }
 },
 mounted() {
   this.setupLeafletMap();
 },
};
</script>