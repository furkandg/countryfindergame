<template>
    <div style="position:absolute;z-index:1000000;top:5px;left:0px;background-color:white" >
        <div class="p-2">
            <h3> {{ timecounter }}</h3>
        </div>


    </div>
</template>

<script>

    export default {
        props: [ "sure","dialog"],
        data() {
            return {
                timecounter: null
            }

        },
        created() {

            this.timecounter = this.sure;
        },
        mounted() {
            

        },
        methods: {
            gonder() {
                this.$emit("toplamasonucu");
            }

        },
        watch: {
            timecounter: {
                handler(value) {

                    if (value > 0) {

                        setTimeout(() => {
                            
                            this.timecounter--;
                       
                        }, 1000);
                    }
                    else if (value==0) {
                        this.gonder()
                    }

                    

                },
                immediate: true
            }

        }
    };
</script>

<style>
</style>
