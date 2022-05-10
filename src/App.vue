<template>
    <div id="app">
        <main-component/>
    </div>
</template>

<script>
import MainComponent from './components/MainComponent.vue'

export default {
  name: 'App',
  components: {
    MainComponent,
  }
}
</script>

<style lang="scss">
@import './style/general'
</style>
