<template>
    <div class="cs_box">
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
.cs_box{
    font-size: 1.3rem;
    color: $text-color;
    position: relative;
    display: flex;
    align-items: center;
    gap: 1rem;

    & .cs_input{
        background-color: $black-color;
        border-radius: 50px;
        border: none;
        color: $text-color;
        padding-left: 3rem;
        width: 200px;
    }
    & .fa-solid{
        cursor: pointer;

        &.fa-magnifying-glass{
            position: absolute;
            left: 10px;
            font-size: 1.3rem;
        }
    }

    & img{
        width: 25px;
    }
}
</style>
