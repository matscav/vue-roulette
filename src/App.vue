<template>
  <div id="app">
    <h1 class="sorting-hat-title">Sombrero Seleccionador</h1>
    <BaseRoulette />
  </div>
</template>

<script>
import BaseRoulette from './components/BaseRoulette.vue';

export default {
  name: 'App',
  components: {
    BaseRoulette
  }
};
</script>

<style>
.sorting-hat-title {
  text-align: center;
  font-size: 45px;
}
</style>
