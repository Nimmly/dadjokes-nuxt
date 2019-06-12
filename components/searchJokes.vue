<template>
    <form @submit.prevent="onSubmit">
        <input type="text" v-model="term" placeholder="Search Jokes">
        <input type="submit" value="Search jokes">
    </form>
</template>

<script>
    export default {
        name: 'SearchJokes',
        data(){
            return {
                term:''
            }
        },
        methods:{
            onSubmit(){
                this.$emit('search-term', this.term);
                this.term = '';
            }
        }

    }
</script>