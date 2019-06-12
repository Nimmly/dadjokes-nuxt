<template>
    <div>
        <search-jokes v-on:search-term ="searchTerm"/>
        <Joke v-for="joke in jokes"
              :key="joke.id"
              :id="joke.id"
              :joke="joke.joke"
        />
    </div>
</template>

<script>
    import axios from 'axios';
    import Joke from '../../components/joke';
    import SearchJokes from '../../components/searchJokes';
    export default {
        components:{
            Joke,
            SearchJokes
        },
        data(){
            return {
                jokes: []
            }
        },
        head(){
            return{
                title:"List of Jokes",
                meta: [{
                    hid:'description',
                    name:'description',
                    content:"place for jokes about dads"
                }
                ]
            }
        },
        async created(){
            const config = {
                headers:{
                    Accept: 'application/json'
                }
            };

            try{
                const response = await axios.get(`https://icanhazdadjoke.com/search`,config)
                this.jokes = response.data.results;
            }catch (err) {
                console.log(err)
            }
        },
        methods:{
            async searchTerm(term){
                const config = {
                    headers:{
                        Accept: 'application/json'
                    }
                }
                try{
                    const response = await axios.get(`https://icanhazdadjoke.com/search?term=${term}`,config);
                    this.jokes = response.data.results;
                }catch(err){
                    console.log(err);
                }
            }
        }
    }
</script>

<style>

</style>