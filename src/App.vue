<template>
  <div class="alerts">
    <div id="redactAlert" class="success"></div>
    <div id="addAlert" class="success"></div>
  </div>
  <router-view />
</template>

<script>
export default {
  components: {
  }
}
</script>

<style lang="scss">
@import url('../src/assets/styles/style.scss');
</style>
