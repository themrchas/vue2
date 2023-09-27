<template>

<h3>Block: Delay is {{ delay }}</h3>
<div class="block" v-if="showBlock" @click="stopTimer">Click me</div>



</template>



<script>
 export default {
    props: ['delay'],
    data() {
        return {
           
            showBlock: false,
            reactionTime: 0,
            timerId: null
     
        }
    },
    methods: {
        stopTimer() {
            clearInterval(this.timerId);
            
            //Send action ('end') and data (this.reactionTime) to parent component.
            this.$emit('end', this.reactionTime);

        },
        startTimer() {
            this.timerId = setInterval(() => { 
                this.reactionTime += 10 ;
                console.log("Executing 'startTimer'");
            }, 10)
        }

    },
    mounted() {
        setTimeout(() => {
            this.showBlock=true;
            this.startTimer();
        }, this.delay);
    },
    updated() {
       // setTimeout(() => {this.message = "Component data was updated 3 seconds ago"}, 3000);
    },
    unmounted() {
        console.log("Component  has been unmounted");
    }

 }


</script>


<style>

    .block {
        width: 400px;
        border-radius: 20px;
        background: #0faf87;
        color: white;
        text-align: center;
        padding: 100px 0;
        margin: 40px auto;
    }




</style>