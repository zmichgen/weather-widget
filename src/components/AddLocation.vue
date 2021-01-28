<template>
  <div  class="add-location">
  <input v-on:keyup.enter="addLocation"
type="text" id="text"
  v-model="value" placeholder="Enter city name"/>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';

@Component
export default class AddLocation extends Vue {
  @Prop() public name!: string[];

  value = '';

  addLocation(event: any) {
    this.$emit('addLocation', event.target.value);
    // eslint-disable-next-line no-param-reassign
    event.target.value = '';
  }
}

</script>
  <style scoped lang="scss">
  .add-location {
    padding: 10px 10px;
    background: #00000011;
    margin-bottom: 10px;
    border-radius: 25px;
      input {
        width: 80%;
        height: 100%;
        font-size: 13px;
        padding: 6px 0 4px 10px;
        border: 1px solid #cecece;
        background: #F6F6f6;
        border-radius: 8px;
      }
  }
</style>
