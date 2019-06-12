<template>
    <div>
        {{ $route.params.id }}
        <nuxt-link to="/jokes">Back to jokes</nuxt-link>
        <h1> {{ joke }}</h1>
        <hr>
        <small>Joke ID: {{ $route.params.id }}</small>
    </div>
</template>

<script>
    import axios from 'axios';

    export default {
        data(){
            return{
                joke:{}
            };
        },
        async created(){
            const config = {
                headers:{
                    Accept: 'application/json'
                }
            };
            try{
                const response = await axios.get(`https://icanhazdadjoke.com/j/${this.$route.params.id}`,config);
                this.joke = response.data.joke
            }catch(err){
                console.log(err)
            }
        }
    }
</script>