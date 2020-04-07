<template>
    <div class="p-sm-4 p-3">

        <form v-if="!thankyou">
            <div class="form-row justify-content-between">
                <div class="col-auto">
                    <img :src="'/images/logo.svg'" width="36" height="36">
                </div>
                <div class="col-auto pt-1">
                    <button type="button" v-on:click.prevent="$emit('close-contact-us')">
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="18px" height="18px" style="fill: #6a6862">
                            <path d="M12,2C6.47,2,2,6.47,2,12c0,5.53,4.47,10,10,10s10-4.47,10-10C22,6.47,17.53,2,12,2z M16.707,15.293 c0.391,0.391,0.391,1.023,0,1.414C16.512,16.902,16.256,17,16,17s-0.512-0.098-0.707-0.293L12,13.414l-3.293,3.293 C8.512,16.902,8.256,17,8,17s-0.512-0.098-0.707-0.293c-0.391-0.391-0.391-1.023,0-1.414L10.586,12L7.293,8.707 c-0.391-0.391-0.391-1.023,0-1.414s1.023-0.391,1.414,0L12,10.586l3.293-3.293c0.391-0.391,1.023-0.391,1.414,0 s0.391,1.023,0,1.414L13.414,12L16.707,15.293z"/>
                        </svg>
                    </button>
                </div>
            </div>
            <div class="form-row pt-2">
                <div class="col-sm-12 pt-2">
                    <label for="name">Name</label>
                    <input v-model="name" type="text" class="form-control" id="name">
                </div>
                <div class="col-sm-12 pt-2">
                    <label for="company">Company</label>
                    <input v-model="company" type="text" class="form-control" id="company">
                </div>
                <div class="col-sm-12 pt-2">
                    <label for="email">Email Address</label>
                    <input v-model="email" type="email" class="form-control" id="email">
                </div>
                <div class="col-sm-12 pt-2">
                    <label for="phone">Phone Number</label>
                    <the-mask :mask="'(###) ###-####'" v-model="phone" type="tel" class="form-control" id="phone"></the-mask>
                </div>
                <div class="col-sm-12 pt-2">
                    <label for="message">Message</label>
                    <textarea v-model="message" type="text" class="form-control pt-2 pb-2" id="message" rows="4"></textarea>
                </div>
            </div>
            <div class="form-row">
                <div class="col-6 pt-3 pb-0">
                    <p class="mt-0 mb-0"><small>By appointment only:</small></p>
                </div>
                <div class="col-6 pt-3 pb-0">
                    <p class="mt-0 mb-0"><small>Coming Soon:</small></p>
                </div>
            </div>
            <div class="form-row">
                <div class="col-6 pt-2">
                    <p class="modal-address mb-0">159 King St<br />Charleston, SC 29401</p>
                </div>
                <div class="col-6 pt-2">
                    <p class="modal-address mb-0">2537 Broad Avenue<br />Memphis, TN 38112</p>
                </div>
            </div>
            <div class="form-row">
                <div class="col-auto pt-4">
                    <button @click="handleSubmit" type="button" class="btn btn-outline-light press">Send Message</button>
                </div>
            </div>
        </form>

        <div id="thank-you" v-else>
            <h4 class="mb-4">Thank you for contacting us.</h4>
            <p class="thank-you">Your message has been received and someone will be in touch<br /> with you as soon as possible.</p>
        </div>

    </div>
</template>

<script>
    import {TheMask} from 'vue-the-mask'

    export default {
        data(){
            return {
                name: null,
                company: null,
                email: null,
                phone: null,
                message: null,
                thankyou: false
            }
        },
        methods: {
            // closeModal() {
            //     this.$refs['contact-modal'].hide()
            // },
            handleSubmit(){
                axios.post('/api/v1/contact_us', {
                    name: this.name,
                    company: this.company,
                    email: this.email,
                    phone: this.phone,
                    message: this.message,
                })
                    .then( (response) => {
                        this.thankyou = true
                        setTimeout(() => {
                            this.$root.$emit('close-contact-us');
                            this.name = null;
                            this.company = null;
                            this.email = null;this.name = null;
                            this.message = null;
                            this.phone = null;
                            this.thankyou = false
                        }, 8000)
                    });
            }
        },
        components: {
            TheMask
        },
        mounted() {
            console.log('Component mounted.')
        }
    }
</script>