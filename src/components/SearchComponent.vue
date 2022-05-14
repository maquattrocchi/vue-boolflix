<template>
    <div class="position-relative">
        <input class="cs_input" type="text" v-model="searchText" @keyup.enter="searchWord">
        <i @click="searchWord" class="fa-solid fa-magnifying-glass"></i>
        <i class="fa-solid fa-bell"></i>
        <img src="../assets/img/avatar.png" alt="avatar">
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

<style lang="scss">
@import '../style/vars';
    .cs_input{
        background-color: $black-color;
        border-radius: 50px;
        border: none;
        color: $text-color;
        padding-left: 3rem;
        width: 200px;
    }
    .fa-solid{
        cursor: pointer;

        &.fa-magnifying-glass{
            position: absolute;
            left: 10px;
        }
    }
    img{
        width: 25px;
        cursor: pointer;
    }
</style>
