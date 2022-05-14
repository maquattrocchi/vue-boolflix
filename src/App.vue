<template>
    <div id="app">
        <header>
            <div class="container d-flex align-items-center justify-content-between h-100">
                <nav-component/>
                <search-component @search="setSearch"/>
            </div>
        </header>
        <main>
            <select-component @search="setSearchGenre"/>
            <main-component :list="filteredMovie" :categoria="movieTitle" :loading="loading" :research="search"/>
            <main-component :list="filteredSeries" :categoria="tvTitle" :loading="loading" :research="search"/>
        </main>
    </div>
</template>

<script>
import axios from 'axios'
import NavComponent from './components/NavComponent.vue'
import SearchComponent from './components/SearchComponent.vue'
import SelectComponent from './components/SelectComponent.vue'
import MainComponent from './components/MainComponent.vue'

export default {
    name: 'App',
    components: {
        NavComponent,
        SearchComponent,
        SelectComponent,
        MainComponent,
    },
    data(){ return{
            apiUrl: 'https://api.themoviedb.org/3/search/',
            apiKey: '2091b727419e6dd8af30ea95fd480178',
            loading: false,
            search: '',
            movieTitle: '',
            tvTitle: '',
            searchGenre: '',
            listMovie: [],
            listTv: [],
        }
    },
    methods:{
        setSearch(txt){
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
            this.searchAll(paramsObj)
        },
        setSearchGenre(txt){
            this.searchGenre = txt
            console.log(this.searchGenre)
        },
        searchFilm(paramsObj){
            return axios.get(this.apiUrl + 'movie', paramsObj);
        },
        searchTv(paramsObj){
            return axios.get(this.apiUrl + 'tv', paramsObj);
        },
        searchAll(paramsObj){
            this.loading= true,
            Promise.all([this.searchFilm(paramsObj), this.searchTv(paramsObj)]).then((res)=>{
                this.listMovie = res[0].data.results;
                this.listTv = res[1].data.results;
                this.loading = false;
                console.log(this.listMovie)
            }).catch((error)=>{
                console.log(error)
                this.loading = false;
            });
        }
    },
    computed:{
        filteredMovie(){
            if(this.searchGenre === ''){
                return this.listMovie
            }else{
                return this.listMovie.filter((element)=>{
                    if(element.genre_ids.includes(this.searchGenre)){
                        return true
                    }
                })
            }
        },
        filteredSeries(){
            if(this.searchGenre === ''){
                return this.listTv
            }else{
                return this.listTv.filter((element)=>{
                    if(element.genre_ids.includes(this.searchGenre)){
                        return true
                    }
                })
            }
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
        this.searchAll(paramsObj)
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

    &>.container>div{
        font-size: 1.3rem;
        color: $text-color;
        display: flex;
        align-items: center;
        gap: 1rem;
    }
}
main{
    padding-top: 80px;
}
</style>
