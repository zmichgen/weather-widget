<template>
  <draggable class="settings-list"
  v-model="draggableList"
  group="locations" @start="drag=true" @end="moveElement">
  <Location v-for="item in locations"
  :key="item" :name="item"
  v-on:removeLocation="removeLocation"/>
  </draggable>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';
import draggable from 'vuedraggable';
import Location from './Location.vue';

@Component({
  components: {
    Location,
    draggable,
  },
})
export default class LocationList extends Vue {
    @Prop() public locations!: string[];

    draggableList: string[] = [];

    mounted() {
      this.draggableList = this.locations;
    }

    removeLocation(item: string) {
      this.$emit('removeLocation', item);
    }

    moveElement(event: any) {
      const data = {
        newIndex: event.newIndex,
        oldIndex: event.oldIndex,
      };

      this.$emit('moveElement', data);
    }
}

</script>
  <style scoped lang="scss">

   .settings-list {
      display: flex;
      flex-direction:column;
      align-content: stretch;
  }
</style>
