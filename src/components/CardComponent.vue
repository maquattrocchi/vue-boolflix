<template>
    <div class="cs_card">
        <img v-if="item.poster_path !== null" :src="'https://image.tmdb.org/t/p/w342'+item.poster_path" :alt="item.title ? item.title : item.name" class="img_poster">
        <img v-else src="../assets/img/notFoundPoster.jpg" alt="" class="img_poster">
        <div class="card_description">
            <div>
                <span class="cs_info">Titolo:</span> 
                {{item.title ? item.title : item.name}}
            </div>
            <div>
                <span class="cs_info">Titolo Originale:</span> 
                {{item.original_title ? item.original_title : item.original_name}}
            </div>
            <div>
                <span class="cs_info">Lingua:</span>
                <img v-if="listLanguage.includes(item.original_language)" :src="'https://www.countryflagicons.com/FLAT/24/'+flagControl(item.original_language)+'.png'"> 
                <img v-else src="../assets/img/notFound.png" alt="" class="flag-img">
            </div>
            <div>
                <span class="cs_info">Voto:</span>
                <i v-for="index in changeNumber(item.vote_average)" :key="index" class="fas fa-star"></i>
            </div>
            <div class="overview">
                <span class="cs_info">Overview</span>
                {{item.overview}}
            </div>
        </div>
    </div>
    <!-- <div class="card">
        <img v-if="item.poster_path !== null" :src="'https://image.tmdb.org/t/p/w342'+item.poster_path" :alt="item.title ? item.title : item.name" class="card-img">
        <img v-else src="../assets/img/notFoundPoster.jpg" alt="" class="poster-img">
        <div class="card-img-overlay">
            <div class="card-title">
                <span>Titolo:</span> 
                {{item.title ? item.title : item.name}}
            </div>
            <div class="card-title">
                <span>Titolo Originale:</span> 
                {{item.original_title ? item.original_title : item.original_name}}
            </div>
            <div class="card-title">
                <span>Lingua</span>
                <img v-if="listLanguage.includes(item.original_language)" :src="'https://www.countryflagicons.com/FLAT/24/'+flagControl(item.original_language)+'.png'"> 
                <img v-else src="../assets/img/notFound.png" alt="" class="flag-img">
            </div>
            <div class="card-title">
                <i v-for="index in changeNumber(item.vote_average)" :key="index" class="fas fa-star"></i>
            </div>
        </div>
    </div> -->
</template>

<script>
export default {
    name:'CardComponent',
    props: ['item'],
    data(){
        return {
            listLanguage: ['en', 'it', 'fr', 'ru', 'de', 'jp']
        }
    },
     methods: {
        changeNumber(number){
            return Math.round(number/2)
        },
        flagControl(language){
            if(language === 'en'){
                language = 'gb'
            }
            return language.toUpperCase()
        }
    },
}
</script>

<style lang="scss">
@import '../style/vars';
.cs_card{
    height: 450px;
    width: 300px;
    position: relative;
    cursor: pointer;

    &:hover .card_description{
        display: block;
    }
    .img_poster{
        height: 100%;
        width: 300px;
        object-fit: cover;
    }
    .card_description{
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        height: 100%;
        background-color: $bg-color;
        color: grey;
        font-size: 1.1rem;
        padding: 1rem;
        display: none;
        font-weight: bold;
        
        .cs_info{
            color: white;
        }
        .overview{
            text-overflow:ellipsis;
            overflow:hidden;
            display: -webkit-box !important;
            -webkit-line-clamp: 6;
            -webkit-box-orient: vertical;
            white-space: normal;
        }
        .flag-img{
            width: 24px;
        }
    }
}
// .card{

//     .poster-img{
//         width: 100%;
//         height: 100%;
//         object-fit: cover;
//     }
// }
//     .flag-img{
//         height: 24px;
//     }
    
</style>