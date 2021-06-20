<template>
    <div  >
        <div class="card" v-if="dialog" style="position:absolute;z-index:1000000;top:820px;left:1150px;">
            <div class="card-header" >
                Ülke Adını Yazınız
            </div>
            <div class="card-body">
                <input class="form-control-sm rounded-0 border" type="text" v-model="yazi" />
                <button class="btn btn-primary  rounded-0" v-on:click="ara"><i class="fas fa-arrow-right"></i></button>
            </div>
            <div>
                <div class="row ml-4">
                    <div class="col-sm-5" style="background-color:forestgreen">
                        {{dogru}}
                    </div>
                    <div class="col-sm-5" style="background-color:red">
                        {{yanlis}}
                    </div>

                </div>
            </div>

        </div>
        <div v-if="!dialog"  style="position:absolute;z-index:1000000;top:800px;left:1150px;min-width:250px;">
            <div class="card">
                <div class="card-header">
                    Sonuç
                </div>
                <div class="card-body">
                    <p>Doğru Cevap:<span>{{dogru}}</span></p>
                    <p>Yanlış Cevap:<span>{{ yanlis}}</span></p>

                    <!--<div class="px-2">
        <ul>
            <li v-for="item in liste">{{item}}</li>
        </ul>
    </div>
    <p></p>-->

                </div>
            </div>
        </div>

    </div>
</template>

<script type="text/javascript" charset="UTF-8">

    
    export default {
        props: ["control","dialog"],
        data() {
            return {
                yazi: "",
                stil: "",
                dogru: 0,
                yanlis: 0,
                liste:[]
       
            }

        },
        created() {
            
            this.source=this.control.source
        },
        mounted() {
           

        },
        methods: {
            ara() {
              
                var filter = this.source.getFeatures().filter(x => x.values_.yazi.toLowerCase() == this.yazi.toLowerCase())
                if (filter.length>0) {
                    var style = new ol.style.Style({
                        stroke: new ol.style.Stroke({
                            color: 'red',
                            width: 1
                        }),
                        text: new ol.style.Text({
                            text: filter[0].values_.yazi,
                            font: 'bold 5px Arial, Verdana, Helvetica, sans-serif',
                            fill: new ol.style.Fill({
                                color: "orange"
                            })
                        }),
                        fill: new ol.style.Fill({
                            color: "blue"
                        })
                    });
                    filter[0].setStyle(style);
                    var filterSehir = this.liste.filter(x => x == this.yazi.toUpperCase())[0];
                    if (!filterSehir) {
                        this.liste.push(this.yazi.toUpperCase())
                        this.dogru++
                    }                    
                    this.control.liste.push(filter[0].values_.yazi.toLowerCase())
                }
               
                else {
                    this.yanlis++
                }
            }
        },
       
    };
</script>

<style>
</style>
