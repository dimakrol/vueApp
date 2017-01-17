<script>
    import TopMenu from './components/TopMenu'
    export default {
        components: {
            TopMenu
        },

    }
</script>

<template>
  <div>
    <top-menu></top-menu>
    <router-view></router-view>
  </div>
</template>

<style lang="sass">
  @import './assets/css/bootstrap.css';
</style>
