<template>
    <div id="app">
        <header>
            <div class="container d-flex align-items-center justify-content-between h-100">
                <h1>Boolflix</h1>
                <search-component @search="searchItem"/>
            </div>
        </header>
        <main>
            <main-component :list="listMovie"/>
            <main-component :list="listTv"/>
        </main>
    </div>
</template>

<script>
import axios from 'axios'
import SearchComponent from './components/SearchComponent.vue'
import MainComponent from './components/MainComponent.vue'

export default {
    name: 'App',
    components: {
        SearchComponent,
        MainComponent,
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

<style lang="scss">
@import './style/general';
header{
    height: 80px;
    position: fixed;
    top: 0;
    width: 100%;

    h1{
        text-transform: uppercase;
        color: $netflix-color;
    }
}
main{
    padding-top: 80px;
}
</style>
