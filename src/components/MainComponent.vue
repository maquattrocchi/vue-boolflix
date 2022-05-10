<template>
    <div>
        <search-component @search="searchItem"/>
        <section>
            <ul>
                <li v-for="(movie, index) in listMovie" :key="index">'TITOLO:' {{movie.title}} 'TITOLO ORIGINALE:' {{movie.original_title}} 'LINGUA:' {{movie.original_language}} 'VOTO: {{movie.vote_average}}</li>
            </ul>
            <ul>
                <li v-for="(serie, index) in listTv" :key="index">'TITOLO:' {{serie.name}} 'TITOLO ORIGINALE:' {{serie.original_name}} 'LINGUA:' {{serie.original_language}} 'VOTO:' {{serie.vote_average}}</li>
            </ul>
        </section>
    </div>
</template>

<script>
import axios from 'axios';
import SearchComponent from './SearchComponent.vue';

export default {
    name: 'MainComponent',
    components: { 
        SearchComponent 
    },
    data(){
        return{
            search: '',
            listMovie: [],
            listTv: [],
            apiUrl: 'https://api.themoviedb.org/3/search/',
            apiKey: '2091b727419e6dd8af30ea95fd480178'
        }
    },
    methods:{
        searchItem(txt){
            this.search = txt
            console.log(this.search)
            this.setSearch()
        },
        searchFilm(paramsObj){
            return axios.get(this.apiUrl + 'movie', paramsObj);
        },
        searchTv(paramsObj){
            return axios.get(this.apiUrl + 'tv', paramsObj);
        },
        setSearch(){
            const paramsObj = {
                params: {
                    api_key: this.apiKey,
                    query: this.search,
                    language: 'it-IT'
                }
            }
            Promise.all([this.searchFilm(paramsObj), this.searchTv(paramsObj)]).then((res)=>{
                this.listMovie = res[0].data.results;
                this.listTv = res[1].data.results;
                console.log(this.listMovie)
                console.log(this.listTv)
            }).catch((error)=>{
                console.log(error)
            });
        }
    }
}
</script>

<style lang="scss" scoped>

</style>