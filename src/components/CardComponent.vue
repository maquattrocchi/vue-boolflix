<template>
    <div class="cs_card">
        <img v-if="item.poster_path !== null" :src="srcPoster+item.poster_path" :alt="item.title ? item.title : item.name" class="img_poster">
        <img v-else src="../assets/img/notFoundPoster.jpg" alt="" class="img_poster">

        <div class="card_description">
            <!-- titolo -->
            <div>
                <span class="cs_info">Titolo:</span> 
                <span>{{title}}</span> 
            </div>
            <!-- titolo originale -->
            <div>
                <span class="cs_info">Titolo Originale: </span> 
                <span>{{originalTitle}}</span>
            </div>
            <!-- bandiera -->
            <div>
                <span class="cs_info">Lingua: </span>
                <img v-if="listLanguage.includes(flagControl)" :src="srcFlag+flagControl+'.png'"> 
                <img v-else src="../assets/img/notFound.png" alt="" class="flag-img">
            </div>
            <!-- voto -->
            <div>
                <span class="cs_info">Voto: </span>
                <span v-for="index in 5" :key="index"><i :class="index <= newVote ? 'fa-solid fa-star' : 'fa-regular fa-star'"></i></span> 
            </div>
            <!-- trama -->
            <div class="overview">
                <span class="cs_info">Overview: </span>
                <span>{{item.overview}}</span>
            </div>
            <!-- cast -->
            <div class="cast">
                <span class="cs_info">Cast: </span>
                <span class="me-2" v-for="(member, index) in cast" :key="index">{{member.name}}</span> 
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import flag from '../library.js';
export default {
    name:'CardComponent',
    props: ['item'],
    data(){
        return {
            listLanguage: [...flag],
            srcPoster: 'https://image.tmdb.org/t/p/w342',
            srcFlag: 'https://www.countryflagicons.com/FLAT/24/',
            movieCast: [],
            seriesCast: [],
        }
    },
    computed:{
        newVote(){
            return Math.round(this.item.vote_average/2)
        },
        flagControl(){
            if(this.item.original_language === 'en'){
                return 'GB'
            }else if(this.item.original_language === 'ko'){
                return 'KR'
            }else if(this.item.original_language === 'ja'){
                return 'JP'
            }
            return this.item.original_language.toUpperCase()
        },
        originalTitle(){
            return this.item.original_title ? this.item.original_title : this.item.original_name
        },
        title(){
            return this.item.title ? this.item.title : this.item.name
        },
        cast(){
            return this.item.original_title ? this.movieCast : this.seriesCast
        }
    },
    mounted(){
        if(this.item.original_title){
            axios.get('https://api.themoviedb.org/3/movie/' + this.item.id + '/credits?api_key=2091b727419e6dd8af30ea95fd480178&language=it-IT').then((res)=>{
                this.movieCast = res.data.cast;
                if (this.movieCast.length >= 5){
                    this.movieCast.length = 5
                }
            }).catch((error)=>{
                console.log(error)
            })
        }else{
            axios.get('https://api.themoviedb.org/3/tv/' + this.item.id + '/credits?api_key=2091b727419e6dd8af30ea95fd480178&language=it-IT').then((res)=>{
                this.seriesCast = res.data.cast;
                if (this.seriesCast.length >= 5){
                    this.seriesCast.length = 5
                }
            }).catch((error)=>{
                console.log(error)
            })
        }
    }
}
</script>

<style lang="scss">
@import '../style/vars';
.cs_card{
    height: 500px;
    width: 300px;
    position: relative;
    cursor: pointer;

    &:hover .card_description{
        //display: block;
        opacity: 1;
    }
    & .img_poster{
        height: 100%;
        width: 300px;
        object-fit: cover;
    }
    & .card_description{
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        height: 100%;
        background-color: rgba($bg-color, 0.8);
        color: $text-color;
        font-size: 1.1rem;
        padding: 1rem;
        //display: none;
        opacity: 0;
        transition: opacity 1s;

        & .cs_info{
            color: $netflix-color;
            margin-right: 0.5rem;
        }
        & .overview{
            text-overflow:ellipsis;
            overflow:hidden;
            display: -webkit-box !important;
            -webkit-line-clamp: 6;
            -webkit-box-orient: vertical;
            white-space: normal;
        }
        & .flag-img{
            width: 24px;
        }
    }
}
</style>