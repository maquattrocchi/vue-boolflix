<template>
    <div id="app">
        <header>
            <div class="container d-flex align-items-center justify-content-between h-100">
                <nav-component/>
                <search-component @search="searchItem"/>
            </div>
        </header>
        <main>
            <main-component :list="listMovie" :categoria="movieTitle" :loading="loading"/>
            <main-component :list="listTv" :categoria="tvTitle" :loading="loading"/>
        </main>
    </div>
</template>

<script>
import axios from 'axios'
import SearchComponent from './components/SearchComponent.vue'
import MainComponent from './components/MainComponent.vue'
import NavComponent from './components/NavComponent.vue'

export default {
    name: 'App',
    components: {
        SearchComponent,
        MainComponent,
        NavComponent,
    },
    data(){ return{
            search: '',
            listMovie: [],
            listTv: [],
            apiUrl: 'https://api.themoviedb.org/3/search/',
            apiKey: '2091b727419e6dd8af30ea95fd480178',
            loading: false,
            movieTitle: '',
            tvTitle: '',
        }
    },
    methods:{
        searchItem(txt){
            this.movieTitle = 'Movies';
            this.tvTitle = 'Series'
            this.search = txt
            const paramsObj = {
                params: {
                    api_key: this.apiKey,
                    query: this.search,
                    language: 'it-IT'
                }
            }
            console.log(this.search)
            this.setSearch(paramsObj)
        },
        searchFilm(paramsObj){
            return axios.get(this.apiUrl + 'movie', paramsObj);
        },
        searchTv(paramsObj){
            return axios.get(this.apiUrl + 'tv', paramsObj);
        },
        setSearch(paramsObj){
            this.loading= true,
            Promise.all([this.searchFilm(paramsObj), this.searchTv(paramsObj)]).then((res)=>{
                this.listMovie = res[0].data.results;
                this.listTv = res[1].data.results;
                this.loading = false;
            }).catch((error)=>{
                console.log(error)
                this.loading = false;
            });
        }
    },
    mounted(){
        this.movieTitle = 'Latest Movies'
        this.tvTitle = 'Latest Series'
        const paramsObj = {
            params: {
                api_key: this.apiKey,
                query: 'a',
                year: '2022',
                language: 'it-IT'
            }
        }
        this.setSearch(paramsObj)
    }
}
</script>

<style lang="scss">
@import './style/general';
header{
    height: 80px;
    position: fixed;
    top: 0;
    background-color: $bg-color;
    width: 100%;
    z-index: 1000;
}
main{
    padding-top: 80px;
}
</style>
