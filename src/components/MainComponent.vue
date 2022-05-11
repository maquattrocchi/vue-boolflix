<template>
    <section class="container">
        <!-- <div class="row row-cols-2 row-cols-md-3 row-cols-lg-4 row-cols-xl-5">
            <div v-for="(item, index) in list" :key="index" class="col">
                <card-component :item="item"/>
            </div>
        </div> -->
        <div class="movie-box">
            <card-component :item="item" v-for="(item, index) in list" :key="index"/>
        </div>
    </section>
</template>

<script>
import CardComponent from './CardComponent.vue'
export default {
    name: 'MainComponent',
    components:{
        CardComponent,
    },
    props:{
        list: Array,
    },
}
</script>

<style lang="scss" scoped>
.movie-box{
    margin: 2rem 0;
    display: flex;
    overflow-x: auto;
    gap: 0.5rem;
}
</style>