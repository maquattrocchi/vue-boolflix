<template>

    <div class="d-flex align-items-center gap-3">
        <h1>Boolflix</h1>
        <div class="dropdownd-block d-lg-none">
            <div class="menu_title" @click="dropMenu = !dropMenu">Sfoglia <i class="fa-solid fa-angle-down"></i></div>
            <ul class="cs_dropdown_menu" v-if="dropMenu">
                <li v-for="(item, index) in menu" :key="index">
                    <a :href="item.url" :class="{'selected' : item.selected}">{{item.link}}</a>
                </li>
            </ul>
        </div>
        <ul class="d-none d-lg-block">
            <li v-for="(item, index) in menu" :key="index">
                <a :href="item.url" :class="{'selected' : item.selected}">{{item.link}}</a>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name:'NavComponent',
    data(){
        return {
            menu: [
                {
                    link: 'Home',
                    url: '#',
                    selected: false,
                },
                {
                    link: 'TV Show',
                    url: '#',
                    selected: false,
                },
                {
                    link: 'Movies',
                    url: '#',
                    selected: false,
                },
                {
                    link: 'Recently Added',
                    url: '#',
                    selected: true,
                },
                {
                    link: 'My List',
                    url: '#',
                    selected: false,
                },
            ],
            dropMenu: false
        }
    }
}
</script>

<style lang="scss">
@import '../style/vars';
h1{
    text-transform: uppercase;
    color: $netflix-color;
    font-size: 3rem !important;
    margin-bottom: 0 !important;
}
.menu_title{
    font-size: 1.5rem;
    cursor: pointer;
}
.cs_dropdown_menu{
    position: absolute;
    z-index: 1000;
    min-width: 10rem;
    padding: 0.5rem 0;
    margin: 0;
    font-size: 1rem;
    text-align: left;
    list-style: none;
    background-clip: padding-box;
    border: 1px solid rgba(0, 0, 0, 0.15);
    border-radius: 0.25rem;
    background-color: $bg-color;

    & li{
        display: block;
    }
}
ul {
    padding: 0 !important;
    margin: 0 !important;

    li{
        display: inline;
        margin: 0.6rem;
        list-style: none;

        & a{
            color: $text-color;
            text-decoration: none;
            font-size: 1.3rem;

            &:hover,&.selected{
                color: $netflix-color;
            }
        }
    }
}
</style>