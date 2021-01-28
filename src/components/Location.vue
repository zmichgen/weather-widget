<template>
  <div>
    <div class="widget-location">
      {{name}}
      <i v-on:click="$emit('removeLocation', name)">🗑</i>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';

@Component
export default class Location extends Vue {
    @Prop() public name!: string[];
}

</script>
  <style scoped lang="scss">
  .widget-location {
    position: relative;
      padding: 10px 20px;
      background: #00000011;
      margin-bottom: 10px;
      border-radius: 25px;
      text-align: left;
      cursor: move;
      i {
        position: absolute;
        right: 15px;
        top: 5%;
        font-size: 25px;
        cursor: pointer;
      }
  }
</style>
