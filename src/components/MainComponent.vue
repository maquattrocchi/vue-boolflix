<template>
    <section class="container">
        <loader-component v-if="loading"/>
        <div v-else>
            <h2>{{categoria}}</h2>
            <div class="item-box">
                <p v-if="list.length === 0">Your search for "{{research}}" did not have any matches.</p>
                <card-component :item="item" v-for="(item, index) in list" :key="index"/>
            </div>
        </div>
    </section>
</template>

<script>
import CardComponent from './CardComponent.vue'
import LoaderComponent from './LoaderComponent.vue'
export default {
    name: 'MainComponent',
    components:{
        CardComponent,
        LoaderComponent,
    },
    props:{
        list: Array,
        categoria: String,
        loading: Boolean,
        research: String,
    },
}
</script>

<style lang="scss">
@import '../style/vars';
.item-box{
    margin: 3rem 0;
    display: flex;
    box-shadow: -1px 1px 13px 5px $netflix-color;
    overflow-x: auto;
    gap: 0.5rem;

    &>p{
        font-size: 2rem;
        padding: 2rem;
        margin-bottom: 0;
        text-transform: uppercase;
    }
}
</style>