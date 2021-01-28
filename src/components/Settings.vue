<template>
  <div class="settings">
    <div
    class="cross"
    v-on:click="$emit('closeSettings', locations)"
    title="Close settings">❌</div>
    <LocationList
    :locations="locations"
     v-on:removeLocation="removeLocation"
     v-on:moveElement="moveElement"/>
    <AddLocation
    v-on:addLocation="addLocation"/>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';
import LocationList from './LocationList.vue';
import AddLocation from './AddLocation.vue';

@Component({
  components: {
    LocationList,
    AddLocation,
  },
})
export default class Settings extends Vue {
  @Prop() public locations!: string[];

  addLocation(location: string) {
    this.$emit('addLocation', location);
  }

  removeLocation(item: string) {
    this.$emit('removeLocation', item);
  }

  moveElement(data: any) {
    this.$emit('moveElement', data);
  }
}

</script>
  <style scoped lang="scss">
  .settings {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: stretch;
    .cross {
      position: absolute;
      top: -10px;
      right: 0;
      font-size: 10px;
      cursor: pointer;
    }
  }
</style>
