<template>
    <div id="home">
        <div class="form-row">
            <div class="col-12 text-center">
                <img :src="'/images/logo.svg'" width="100" height="100">
            </div>
            <div class="col-12 text-center">
                <img class="mt-2" :src="'/images/text-logo.svg'" width="225" height="50">
            </div>
            <div class="col-12 text-center">    
                <button class="btn btn-outline-light mt-4" v-on:click="isShow = !isShow">Contact Us</button>
            </div>
        </div>

        <transition name="slide">
            <div class="form-row contact-form m-0" v-show="isShow">
                <div class="col-12 p-0">
                    <contact-form v-on:close-contact-us="close"></contact-form>
                </div>
            </div>
        </transition>

    </div>
</template>

 <script>
    export default {
        data(){
            return {
                isShow : false,
            }
        },
        methods: {
            close(){
                this.isShow = false
            }
        },
        mounted(){
//            this.$on('close-contact-us', event => {
//                console.log("testing")
//                this.isShow = false
//            });
        }
     }
 </script>