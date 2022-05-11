<template>
    <div>
        <section>
            <ul>
                <li v-for="(item, index) in list" :key="index">
                    'IMG' : <img v-if="item.poster_path !== null" :src="'https://image.tmdb.org/t/p/w342'+item.poster_path" :alt="item.title ? item.title : item.name"> 
                    <img v-else src="../assets/img/notFoundPoster.jpg" alt="" class="poster-img"><br>

                    'TITOLO:' {{item.title ? item.title : item.name}} <br>

                    'TITOLO ORIGINALE:' {{item.original_title ? item.original_title : item.original_name}} <br> 

                    'LINGUA:' 
                    <img v-if="listLanguage.includes(item.original_language)" :src="'https://www.countryflagicons.com/FLAT/24/'+flagControl(item.original_language)+'.png'"> 
                    <img v-else src="../assets/img/notFound.png" alt="" class="flag-img"> <br>

                    'VOTO:' <i v-for="index in changeNumber(item.vote_average)"
                                :key="index"
                                class="fas fa-star">
                            </i>
                </li>
            </ul>
        </section>
    </div>
</template>

<script>

export default {
    name: 'MainComponent',
    props:{
        list: Array,
    },
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

<style lang="scss" scoped>
.flag-img{
    height: 24px;
}
.poster-img{
    height: 513px;
    width: 342px;
}
</style>