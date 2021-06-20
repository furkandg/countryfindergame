<template>
    <div>
        <div class="cardx" style="position:absolute;z-index:1000000;top:800px;left:1150px;">

            <div class="card">
                <div class="card-header" v-if="anaKisim">
                    Süre Seçiniz
                </div>
                <div class="card-body" v-if="anaKisim">

                    <div class="btn-group" role="group" aria-label="Basic example">
                        <button type="button" class="btn btn-primary text-white" v-on:click="degerim(60)">60 Saniye</button>
                        <button type="button" class="btn btn-primary text-white" v-on:click="degerim(90)">90 Saniye</button>
                        <button type="button" class="btn btn-primary text-white" v-on:click="degerim(120)">120 Saniye</button>
                    </div>
                </div>
                <button v-if="anaKisim" v-on:click="deger" class="btn btn-primary">Başla</button>


            </div>
        </div>
        <counter v-if="!anaKisim" v-bind:sure="sure" v-bind:dialog="dialog" v-on:toplamasonucu="test()" />
        <search v-if="!anaKisim" v-bind:dialog="dialog" v-bind:control="this" />
        
        


    </div>
</template>

<script>
    import counter from './counter.vue';
    import search from './search.vue';

    export default {
        props: ["map","source"],
        components: {
            counter,search
        },
        data() {
            return {
                anaKisim: true,
                _sure: 0,
                sure: 60,
                dialog:true
               
            }

        },
        computed: {
            deger() {

                this.anaKisim = !this.anaKisim
                this.sure = this._sure;

            }
           
        },
        created() {
           
        },
        mounted() {


        },
        methods: {
            test() {
             
                    this.dialog = false;
              
            },

            degerim(_deger) {
                this._sure = _deger;

            },

        },
        watch:{
            sure:function(val)
            {
              
                if(val==0)
                {
                      

                }
                
            }


        }

    };
</script>

<style>
</style>
