<template>
    <section class="container">
        <div class="item-box">
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
.item-box{
    margin: 2rem 0;
    display: flex;
    overflow-x: auto;
    gap: 0.5rem;
}
</style>