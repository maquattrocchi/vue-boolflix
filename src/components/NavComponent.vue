<template>
    <div class="d-flex align-items-center gap-3">
        <h1>Boolflix</h1>
        <ul>
            <li><a href="#" >Home</a></li>
            <li><a href="#">TV Show</a></li>
            <li><a href="#">Movies</a></li>
            <li><a href="#" class="selected">Recently Added</a></li>
            <li><a href="#">My List</a></li>
        </ul>
    </div>
</template>

<script>
export default {
    name:'NavComponent',
}
</script>

<style lang="scss">
@import '../style/vars';
h1{
    text-transform: uppercase;
    color: $netflix-color;
    font-size: 3rem !important;
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