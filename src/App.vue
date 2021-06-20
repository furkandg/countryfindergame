<template>
    <div id="map" class="map">
        <MainContainer v-bind:map="map" v-bind:source="source" />
       
    </div>
 
</template>


<script>
    import MainContainer from './components/MainContainer.vue';
  

    export default {
        name: 'App',

        components: {
            MainContainer
        },
        data() {

            return {
                articles: "",
                map: "",
                source:""
            }
        },
        mounted() {
            this.map = new ol.Map({
                target: 'map',
                layers: [
                    new ol.layer.Tile({
                        source: new ol.source.OSM()
                    })
                ],
                view: new ol.View({
                    center: ol.proj.fromLonLat([10.41, 21.82]),
                    zoom: 1
                })
            });


            var style = new ol.style.Style({
                stroke: new ol.style.Stroke({
                    color: 'blue',
                    width: 1
                }),
                fill: new ol.style.Fill({
                    color: "red"
                })
            });
            this.source = new ol.source.Vector({
                url: 'http://petdefteri.com:8080/geoserver/generalrepo/ows?service=WFS&version=1.0.0&request=GetFeature&typeName=generalrepo%3Aulkeson&outputFormat=application%2Fjson',
                format: new ol.format.GeoJSON({
                })
            });

            var layer1 = new ol.layer.Vector({
                source: this.source, 
                style: style,
            });

            this.map.addLayer(layer1);
        }
    };
</script>
