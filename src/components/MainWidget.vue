<template>
  <div class="weather-widget__main">
    <div
    class="settings__main" v-if="!settings"
    v-on:click="settings = true"
    title="Choose locations">
      ⚙
    </div>
    <div
    v-if="settings">
      <Settings
      v-on:closeSettings="closeSettings"
      v-on:addLocation="addLocation"
      v-on:removeLocation="removeLocation"
      v-on:moveElement="moveElement"
      :locations="items"/>
    </div>
    <div
    v-if="!settings && items.length">
      <LocationWheather  v-for="item in items" :key="item" :locationName="item"/>
    </div>
    <div v-if="!settings && !items.length">
      <LocationWheather  :locationName="'Add at least one location'"/>
     </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import LocationWheather from './LocationWheather.vue';
import Settings from './Settings.vue';

@Component({
  components: {
    LocationWheather,
    Settings,
  },
})
export default class MainWidget extends Vue {
  items: string[] = ['Minsk', 'London', 'Moscow', 'Kiev'];

  settings = false;

  closeSettings(items: string[]) {
    this.settings = false;
    this.items = items;
  }

  addLocation(item: string) {
    if (!this.items.includes(item)) {
      this.items.push(item);
    }
  }

  removeLocation(item: string) {
    const itemIndex = this.items.findIndex((i) => i === item);
    this.items.splice(itemIndex, 1);
  }

  moveElement(data: any) {
    const movedElement = this.items.splice(data.oldIndex, 1);
    this.items.splice(data.newIndex, 0, movedElement[0]);
  }
}
</script>
<style scoped lang="scss">

.weather-widget__main {
  position: relative;
  .settings__main {
    position: absolute;
    right: 5px;
    cursor: pointer;
  }
}
</style>
