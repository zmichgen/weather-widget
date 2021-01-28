<template>
<div id="app">
  <MainWidget/>
</div>

</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import MainWidget from './components/MainWidget.vue';

@Component({
  components: {
    MainWidget,
  },
})
export default class App extends Vue {}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 200px;
}
</style>
