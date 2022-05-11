<template>
    <div>
        <input type="text" v-model="searchText">
        <button @click="searchWord">Cerca</button>
    </div>
</template>

<script>
export default {
    name: 'SearchComponent',
    data(){
        return{
            searchText: '',
        }
    },
    components:{
    },
    methods:{
        searchWord(){
            this.$emit('search', this.searchText);
            this.searchText = '';
        }
    }
}
</script>

<style scoped lang="scss">

</style>
