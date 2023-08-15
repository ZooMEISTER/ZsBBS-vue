<template>
    <div>
        <img alt="Vue logo" src="../../assets/logo.png">
        <h1>MAIN</h1>
        <div>{{this.$store.state.s_token}}</div>
    </div>


</template>

<script>
import axios from 'axios'

export default {
    created(){
        //console.log(typeof(msg))
    },
    data(){
        return{
            
        }
    },
    methods:{
    


    }
}
</script>

<style>

</style>