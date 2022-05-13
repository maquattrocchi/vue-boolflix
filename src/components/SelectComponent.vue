<template>
    <div class="text-center">
        <select class="cs_select" name="genre" id="genre" @change="mySearch" v-model="selectOption">
            <option value="">Search by genre</option>
            <option :value="genre.id" v-for="(genre, index) in allGenres" :key="index">{{genre.name}}</option>
        </select>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'SelectComponent',
    data(){
        return {
            selectOption: '',
            movieGenres: [],
            seriesGenres: [],
        }
    },
    methods:{
        mySearch(){
            this.$emit('search', this.selectOption)
        },
    },
    computed:{
        allGenres(){
            let listId = this.movieGenres.map((el) => el.id);
            return [...this.movieGenres, ...this.seriesGenres.filter((el) => !listId.includes(el.id))];
        }
    },
    mounted(){
        axios.get('https://api.themoviedb.org/3/genre/movie/list?api_key=2091b727419e6dd8af30ea95fd480178&language=it-IT').then((res)=>{
            this.movieGenres = res.data.genres
            console.log(this.movieGenres)
        }).catch((error)=>{
            console.log(error)
        })
        axios.get('https://api.themoviedb.org/3/genre/tv/list?api_key=2091b727419e6dd8af30ea95fd480178&language=it-IT').then((res)=>{
            this.seriesGenres = res.data.genres;
            console.log(this.seriesGenres)
        }).catch((error)=>{
            console.log(error)
        })
    }
}
</script>

<style lang="scss">
@import '../style/vars';

.cs_select{
    width: 500px;
    font-size: 1.3rem;
    border-radius: 20px;
    color: $text-color;
    padding: 0.5rem;
    background-color: $black-color;
    border: none;
    outline: none;
}
</style>