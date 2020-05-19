<template>
  <div id="app">
<!--    <img src="./assets/logo.png">-->
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app {
  width: 100%;
  height: 100%;
}
.BMap_cpyCtrl {
  display: none !important;
}
.anchorBL {
  display: none !important;
}
</style>
